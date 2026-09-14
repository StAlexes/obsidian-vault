
## ЧАСТЬ 1. Что это за инструмент и зачем он нужен

* **Вайбкодинг** — подход к разработке, при котором рутину (написание бойлерплейта, поиск API, синтаксис C#) берет на себя нейросеть (AI-агент), а разработчик формулирует задачи на естественном языке и контролирует результат.
* **T-FLEX DOCs** — конфигурируемая PLM/PDM-система. Вся её бизнес-логика (справочники, типы объектов, параметры, связи 1:N / 1:1, списки объектов) хранится в базе данных и имеет уникальные идентификаторы (**GUID**).
* **«Каталог метаданных по запросу» (`SchemaFetcher`)** — консольная утилита внутри проекта, которая подключается к живому серверу DOCs, опрашивает структуру выбранного справочника и генерирует два файла:
  1. `Schemas/<Имя>.schema.md` — топология справочника на человеческом языке для контекста ИИ-агента.
  2. `Schemas/<Имя>.guids.cs` — готовый C#-класс со статическими константами GUID для вставки в макрос.
* **Мост «T-FLEX DOCs ↔ VS Code»** — сервисный макрос внутри DOCs, который передает код макроса в файл `ClassTemp.cs` и по закрытию вкладки в VS Code автоматически возвращает обновленный код обратно в систему.

---

## ЧАСТЬ 2. Предварительные системные требования (установка на компьютер)

Все действия выполняются под учетной записью с правами администратора на рабочей станции Windows.

### Шаг 1. Установка базового ПО
1. **Установи Visual Studio Code:**
   * Скачай дистрибутив с официального сайта `code.visualstudio.com` (User Installer x64).
   * При установке отметь галочки: *«Добавить действие "Открыть с помощью Code" в контекстное меню»* и *«Добавить в PATH»*.
2. **Установи .NET SDK (версия 8.0 или 9.0/10.0):**
   * Скачай установщик с `dotnet.microsoft.com/download`.
   * Он необходим для работы движка VS Code и утилиты `dotnet CLI`.
3. **Установи .NET Framework 4.7.2 Developer Pack:**
   * Скачай именно **Developer Pack** (не Runtime!) со страницы `dotnet.microsoft.com/download/dotnet-framework/net472`.
   * Он содержит эталонные библиотеки (Reference Assemblies) для сборки проектов под T-FLEX DOCs 18.
4. **Убедись, что клиент T-FLEX DOCs 18 установлен:**
   * Стандартный путь: `C:\Program Files (x86)\T-FLEX DOCs 18 (18ReleaseOAK)\Program`.

---

## ЧАСТЬ 3. Настройка расширений VS Code

1. Открой **VS Code**.
2. Перейди в раздел расширений (нажми `Ctrl` + `Shift` + `X` или иконку четырех кубиков на левой панели).
3. Установи следующие модули (вводи название в строку поиска и нажимай **Install**):
   * **C#** (автор: *Microsoft*) — базовая поддержка языка C# и отладчик CLR.
   * **C# Dev Kit** (автор: *Microsoft*) — поддержка решений `.sln` и проектов `.csproj`.
   * **Cline** (автор: *Cline*) — автономный AI-агент для вайбкодинга.
   * **Russian Language Pack** (автор: *Microsoft*) — русификация интерфейса (по желанию).
4. Если в нижней панели VS Code загорится ошибка `Error acquiring .NET!`:
   * Открой настройки (`Ctrl` + `,`), найди пункт `dotnet.dotnetPath` и укажи: `C:\Program Files\dotnet\dotnet.exe`.
   * Перезапусти VS Code.

---

## ЧАСТЬ 4. Развертывание рабочего проекта `DOCs_Macros`

1. Создай на диске рабочую папку (например, `C:\Projects\DOCs_Macros`).
2. Открой эту папку в VS Code через меню **«Файл» → «Открыть папку...»**.
3. В корне папки создай следующие 4 ключевых файла:

### 1. Файл проекта: `DOCs_Macros.csproj`
```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net472</TargetFramework>
    <OutputType>Exe</OutputType>
    <LangVersion>latest</LangVersion>
    <Nullable>disable</Nullable>
    <NoWarn>$(NoWarn);MSB3246;MSB3243;MSB3277</NoWarn>
    <TFlexPath>C:\Program Files (x86)\T-FLEX DOCs 18 (18ReleaseOAK)\Program</TFlexPath>
  </PropertyGroup>

  <ItemGroup>
    <Reference Include="Microsoft.CSharp" />
    <Reference Include="$(TFlexPath)\*.dll" Exclude="$(TFlexPath)\Interop.SolidEdgeConstants.dll">
      <Private>False</Private>
    </Reference>
  </ItemGroup>

  <Target Name="StopRunningDocsMacros" BeforeTargets="PrepareForBuild">
    <Exec Command="powershell -NoProfile -ExecutionPolicy Bypass -Command &quot;Get-Process -Name 'DOCs_Macros' -ErrorAction SilentlyContinue | Where-Object { $_.Path -like '*\DOCs_Macros\bin\Debug\net472\DOCs_Macros.exe' } | Stop-Process -Force; exit 0&quot;" />
  </Target>

</Project>
```
*(Проверь: путь в теге `<TFlexPath>` должен строго указывать на папку `Program` твоего установленного клиента DOCs).*

### 2. Конфигурация зависимостей: `App.config`
```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <runtime>
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
      <probing privatePath="C:\Program Files (x86)\T-FLEX DOCs 18 (18ReleaseOAK)\Program" />
    </assemblyBinding>
  </runtime>
</configuration>
```

### 3. Точка входа: `Program.cs`
```csharp
using System;
using System.IO;
using System.Reflection;

public class Program
{
    private static readonly string TFlexFolder = @"C:\Program Files (x86)\T-FLEX DOCs 18 (18ReleaseOAK)\Program";

    public static void Main(string[] args)
    {
        if (Directory.Exists(TFlexFolder))
        {
            Directory.SetCurrentDirectory(TFlexFolder);
        }

        AppDomain.CurrentDomain.AssemblyResolve += (sender, resolveArgs) =>
        {
            try
            {
                string simpleName = new AssemblyName(resolveArgs.Name).Name;
                string targetPath = Path.Combine(TFlexFolder, simpleName + ".dll");

                if (File.Exists(targetPath))
                {
                    return Assembly.LoadFrom(targetPath);
                }
            }
            catch { }
            return null;
        };

        Run();
    }

    private static void Run()
    {
        SchemaFetcher.Fetch();
    }
}
```

### 4. Утилита выгрузки: `SchemaFetcher.cs`
Помести в корень проекта оттестированный файл `SchemaFetcher.cs`, который обращается к серверу DOCs через механизм рефлексии.

---

## ЧАСТЬ 5. Настройка отладчика и системных правил для AI

### 1. Настройка отладки (`.vscode/launch.json`)
Создай в проекте папку `.vscode`, а внутри неё файл `launch.json`:
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Прикрепиться к T-FLEX DOCs (.NET Framework)",
      "type": "clr",
      "request": "attach",
      "processId": "${command:pickProcess}"
    }
  ]
}
```
*(Параметр `"type": "clr"` критически важен: именно он перехватывает отладку внутри классического .NET Framework 4.7.2).*

### 2. Системные правила для агента Cline (`.clinerules`)
В корне проекта создай файл `.clinerules`:
```text
Всегда общайся и отвечай исключительно на русском языке.
Ты — ведущий инженер-разработчик макросов для платформы T-FLEX DOCs 18 (C#, .NET Framework 4.7.2).

ПРАВИЛА ОФОРМЛЕНИЯ МАКРОСОВ:
1. МАКРОС — ЭТО "ВЕЩЬ В СЕБЕ":
   - Макрос должен быть полностью автономен и оформлен единым файлом без ссылок на внешние классы проекта.
   - Все используемые GUID справочников, типов, связей и списков объектов объявляются внутри класса макроса в виде вложенного статического класса `Guids`.

2. СТАНДАРТ СТРУКТУРЫ:
   using System;
   using TFlex.DOCs.Model.Macros;

   public class Macro : MacroProvider
   {
       public static class Guids
       {
           /// <summary>Описание сущности</summary>
           public static readonly Guid ИмяСущности = new Guid("...");
       }

       public Macro(MacroContext context) : base(context) { }

       public override void Run()
       {
           // Точка останова для отладчика VS Code:
           System.Diagnostics.Debugger.Break();

           // Основной код
       }
   }

3. РАБОТА С СХЕМАМИ ДАННЫХ:
   - Бери названия типов, связей, списков объектов и параметров ИСКЛЮЧИТЕЛЬНО из файлов в папке `Schemas/*.schema.md` и `Schemas/*.guids.cs`.
   - Запрещено придумывать методы и GUID.
   - Обязательно проверяй объекты и параметры на null перед разыменованием.
```

---

## ЧАСТЬ 6. Пошаговый регламент работы (Как пользоваться решением)

### Этап 1. Выгрузка схемы справочника из базы данных
1. В VS Code нажми `Ctrl` + `~` (открой терминал).
2. Выполни команду запуска:
   ```powershell
   dotnet run --project .\DOCs_Macros.csproj
   ```
3. При первом запуске утилита спросит адрес сервера (например, `http://srv-docs:8080`). Адрес сохранится локально в `%AppData%` и больше запрашиваться не будет.
4. Введи свой логин и пароль от T-FLEX DOCs.
5. Утилита выведет пронумерованный список справочников системы. Введи номер нужного справочника (например, `Номенклатура и изделия`) и нажми `Enter`.
6. В папке проекта `Schemas/` мгновенно появятся два файла:
   * `Номенклатура_и_изделия.schema.md` — топология для ИИ.
   * `Номенклатура_и_изделия.guids.cs` — константы GUID.

### Этап 2. Получение кода макроса из T-FLEX DOCs
1. В интерфейсе клиента T-FLEX DOCs найди целевой макрос.
2. Запусти служебный макрос **«Открыть в VS Code»** (наш мост).
   * *При первом запуске он вежливо попросит указать папку проекта VS Code (`C:\Projects\DOCs_Macros`) и сохранит путь в `settings.json`.*
3. Макрос выгрузит исходный код в файл **`ClassTemp.cs`** и откроет его в VS Code.

### Этап 3. Вайбкодинг макроса
1. Открой чат **Cline** (значок робота слева) или Copilot Chat.
2. Поставь задачу агенту, сославшись на схему:
   > *«Изучи файл `Schemas/Номенклатура_и_изделия.schema.md`. Доработай макрос в `ClassTemp.cs`: добавь проверку на наличие связи со спецификацией. Используй константы GUID из файла `Schemas/Номенклатура_и_изделия.guids.cs` и объяви их во вложенном классе `Guids`»*.
3. Агент изучит реальную структуру базы и напишет точный, компилируемый код.
4. Проверь компиляцию: нажми **`Ctrl` + `Shift` + `B`**. В окне вывода должно быть: `Сборка успешно завершена. Ошибок: 0`.

### Этап 4. Живая отладка в VS Code
1. В начале метода `Run()` в `ClassTemp.cs` убедись, что стоит строчка:  
   `System.Diagnostics.Debugger.Break();`
2. Нажми **`F5`** (в списке процессов выбери `TFlexDOCs.exe`).
3. В клиенте T-FLEX DOCs нажми кнопку запуска макроса.
4. Выполнение моментально замрёт, VS Code подсветит строку жёлтым маркером. Нажимай **`F10`** (шаг) и **`F11`** (шаг внутрь) для проверки значений переменных реальной базы.
5. Нажми `Shift` + `F5`, чтобы отключить отладчик.

### Этап 5. Возврат кода в T-FLEX DOCs
1. Нажми **`Ctrl` + `S`** (сохрани файл `ClassTemp.cs`).
2. **Закрой вкладку `ClassTemp.cs` в VS Code** (нажми `Ctrl` + `W` или крестик).
3. Мост T-FLEX DOCs (работавший с ключом `--wait`) автоматически зафиксирует закрытие вкладки, прочитает измененный файл с диска и запишет свежий код в базу данных.