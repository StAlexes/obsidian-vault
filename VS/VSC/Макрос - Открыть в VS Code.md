

```C#
using System;
using System.IO;
using System.Diagnostics;
using TFlex.DOCs.Model.Macros;

public class Macro : MacroProvider
{
    public Macro(MacroContext context) : base(context) { }

    public override void Run()
    {
        var macroObj = CurrentObject;
        if (macroObj == null)
        {
            Message("Внимание", "Сначала выделите макрос в списке справочника!", null);
            return;
        }

        // 1. Папка и путь к конфигурационному JSON-файлу настроек пользователя
        string appDataDir = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.ApplicationData), "TFlexDocs_VsCodeBridge");
        string settingsFile = Path.Combine(appDataDir, "settings.json");

        string projectDir = "";

        // 2. Проверяем, есть ли уже файл настроек
        if (File.Exists(settingsFile))
        {
            try
            {
                // Читаем путь из JSON (ищем строку "projectDir": "...")
                string jsonText = File.ReadAllText(settingsFile, System.Text.Encoding.UTF8);
                projectDir = ExtractProjectDirFromJson(jsonText);
            }
            catch
            {
                projectDir = ""; // При ошибке чтения спросим путь заново
            }
        }

        // 3. Если настройки еще не созданы или папка не существует — показываем инструкцию и настраиваем
        if (string.IsNullOrEmpty(projectDir) || !Directory.Exists(projectDir))
        {
            string welcomeMsg = 
                "Для работы с этой функцией на вашем компьютере должен быть установлен VS Code " +
                "с предварительно настроенным проектом для разработки под T-FLEX DOCs.\n\n" +
                "Если проект уже подготовлен, нажмите «Да» и выберите папку расположения вашего проекта в VS Code.\n\n" +
                $"Ваши настройки будут сохранены в файл:\n{settingsFile}\n\n" +
                "Продолжить настройку?";

            bool agree = Question(welcomeMsg);
            if (!agree)
            {
                return; // Пользователь отказался или еще не настроил VS Code
            }

            // Открываем диалог выбора папки
            var folderDialog = CreateOpenFolderDialog("Укажите папку проекта в VS Code");
            if (!folderDialog.Show() || string.IsNullOrEmpty(folderDialog.DirectoryName))
            {
                Message("Отмена", "Папка не была выбрана. Настройка отменена.", null);
                return;
            }

            projectDir = folderDialog.DirectoryName;

            // Сохраняем путь в аккуратный JSON-файл
            Directory.CreateDirectory(appDataDir);
            string jsonContent = "{\n  \"projectDir\": \"" + projectDir.Replace("\\", "\\\\") + "\"\n}";
            File.WriteAllText(settingsFile, jsonContent, System.Text.Encoding.UTF8);
        }

        // 4. Путь к файлу ClassTemp.cs в выбранном проекте
        string filePath = Path.Combine(projectDir, "ClassTemp.cs");

        // 5. Выгружаем код из поля «Текст программы» в файл
        string currentCode = macroObj["Текст программы"].ToString();
        File.WriteAllText(filePath, currentCode, System.Text.Encoding.UTF8);

        // 6. Запускаем VS Code с флагом --wait (ждем закрытия вкладки)
        var process = Process.Start(new ProcessStartInfo
        {
            FileName = "cmd.exe",
            Arguments = $"/c code --wait \"{filePath}\"",
            CreateNoWindow = true,
            UseShellExecute = false
        });

        // 7. Ждем закрытия файла в VS Code
        process.WaitForExit();

        // 8. Автоматически сохраняем изменения обратно в базу DOCs
        if (File.Exists(filePath))
        {
            string updatedCode = File.ReadAllText(filePath, System.Text.Encoding.UTF8);

            macroObj.BeginChanges();
            macroObj["Текст программы"] = updatedCode;
            macroObj.Save();

            Message("Авто-синхронизация", "Вкладка закрыта. Код успешно обновлен в базе T-FLEX DOCs!", null);
        }
    }

    // Вспомогательный метод парсинга JSON без внешних библиотек
    private string ExtractProjectDirFromJson(string json)
    {
        int keyIndex = json.IndexOf("\"projectDir\"");
        if (keyIndex == -1) return "";

        int colonIndex = json.IndexOf(':', keyIndex);
        if (colonIndex == -1) return "";

        int firstQuote = json.IndexOf('"', colonIndex + 1);
        if (firstQuote == -1) return "";

        int secondQuote = json.IndexOf('"', firstQuote + 1);
        if (secondQuote == -1) return "";

        string path = json.Substring(firstQuote + 1, secondQuote - firstQuote - 1);
        return path.Replace("\\\\", "\\");
    }
}
```