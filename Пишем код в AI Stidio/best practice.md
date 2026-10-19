# Руководство разработчика макросов T-FLEX DOCs 18: Архитектура метаданных и работа с объектами

## 1. Строители метаданных (Metadata Builders)

* **Где находятся**: Пространство имен `TFlex.DOCs.Model.Structure.Builders`.


* **Автоматическое поведение ядра**:
* При создании справочника конструктором `new ReferenceBuilder(targetFolder) { Name = refName }` и последующем `Save()` платформа **автоматически** генерирует базовый тип объекта (с тем же именем) и системный строковый параметр **«Наименование»**.


* **Запрещено** создавать тип или параметр «Наименование» заново через `new` — это приведёт к дублям!


* **Правильный путь**: найти автосозданный тип через `refBuilder.ParameterGroup.Classes.Find(refName)` и переименовать его с помощью `new ClassObjectBuilder(defaultClass)`.




* **Группы параметров 1:1 (`TableOneToOne`)**:
* Платформа не создает пользовательскую группу 1:1 автоматически. Её **необходимо явно создать**:
```csharp
var groupBuilder = new ParameterGroupBuilder(ParameterGroupType.TableOneToOne, refBuilder.ParameterGroup, targetClass) { Name = "Свойства объекта" };
groupBuilder.Save();
var paramGroup = groupBuilder.ParameterGroup;

```




* **Типы параметров (`ParameterType`)**:
* `ParameterType` — это **ссылочный класс**, а не `enum`.


* Строки Юникод: строго **`ParameterType.NVarChar`** (а не `UnicodeText` или `String`).


* Дробные числа: **`ParameterType.Real`** (а не `Double`).


* Целые числа: **`ParameterType.Int`**.


* Дата и время: **`ParameterType.DateTime`**.




* **Коллекция типов `ClassTree**`:
* `refBuilder.ParameterGroup.Classes` имеет тип `ClassTree` и **не реализует LINQ-перечислитель напрямую**.


* Вызовы `.First()`, `.Where()` падают с `CS1061`. Поиск типов выполняется строго через **`.Find("ИмяТипа")`** или свойства `RootClasses`.





---

## 2. Поиск и адресация параметров (`ParameterInfo`)

* **Локализация параметров**:
* Свойство `reference.ParameterGroup.Parameters` содержит параметры **только корневой таблицы** (системные поля).


* Пользовательские параметры лежат в подчиненных группах 1:1: `reference.ParameterGroup.OneToOneTables[i].Parameters`.


* Для безопасного поиска параметра по всей структуре справочника:
```csharp
ParameterInfo pi = reference.ParameterGroup.OneToOneParameters.FindByName("ИмяПараметра");

```


или перебором всех групп из `reference.ParameterGroup.OneToOneTables`.




* **Спецсимволы в именах**:
* Параметры с запятыми, точками или спецсимволами (например, *«Атомная масса, а.е.м.»*) при обращении через строковый макроязык могут вызывать ошибки поиска. Доступ к ним должен осуществляться напрямую через объект **`ParameterInfo`**:
```csharp
referenceObject[piParam].Value = 12.34;

```





---

## 3. Жизненный цикл объектов и сохранение в БД

### 3.1. Создание новых объектов

* При создании объекта через низкоуровневый API:
```csharp
ReferenceObject obj = reference.CreateReferenceObject(targetClass);

```


**Объект УЖЕ находится в режиме редактирования (`Changing == true`)**!


* **Запрещено** вызывать `obj.BeginChanges()` сразу после `CreateReferenceObject()`.


* Нарушение парности вызовов `BeginChanges()` / `EndChanges()` блокирует фиксацию объекта в БД.





### 3.2. Редактирование существующих объектов

* **Одиночное сохранение**:
```csharp
obj.BeginChanges(false);
obj[pi].Value = value;
obj.EndChanges(); // Фиксация в БД

```


* **Пакетное сохранение (Bulk Update)**:
* В цикле вызывается только `BeginChanges(false)` и заполнение параметров.
* Индивидуальный `obj.EndChanges()` **НЕ вызывается** внутри цикла!


* По завершении цикла вызывается единая точка фиксации:
```csharp
Reference.EndChanges(listOfModifiedObjects);

```


* *Пояснение ошибки*: если вызвать `obj.EndChanges()` в цикле, а затем передать список в `Reference.EndChanges()`, платформа выбросит исключение `ArgumentException: Объект не находится в режиме редактирования`.





---

## 4. Методы UI и оповещения пользователя

* **Контекст `MacroProvider**`:
* Методы `Сообщение(...)` и `Ошибка(...)` принадлежат базовому классу **`MacroProvider`** (а не `MacroContext`)!


* **Правильно**:
```csharp
Сообщение("Заголовок", "Текст {0}", arg);
Ошибка("Текст ошибки");

```


* **Неправильно**: `Context.Сообщение(...)`, `Context.Ошибка(...)` (вызывает `CS1061`).


* Вымышленных методов вроде `Предупреждение` или `Warning` в платформе **нет**.




* **Обновление интерфейса**:
* После пакетного создания или изменения объектов обязательно вызывать:
```csharp
Context.RefreshReferenceWindow(); // или ОбновитьОкноСправочника();

```


чтобы изменения сразу отобразились в клиентском приложении DOCs.