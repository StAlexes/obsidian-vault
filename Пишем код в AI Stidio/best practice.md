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


---

## 6. Архитектура связей (`LinkGroupBuilder`) и запрет системных символов

* **Уникальность физического имени таблицы (`TableName`)**:
* Свойство `TableName` задает физическое имя связующей таблицы в БД SQL Server.
* **Правило**: `TableName` обязано быть **глобально уникальным** по всей схеме T-FLEX DOCs. Если два разных справочника используют одинаковое имя (например, `"LinkToChemElements"`), платформа выдает фатальный сбой: `Таблица с именем "..." уже существует. [Код ошибки #012]`.
* **Решение**: Всегда использовать префикс контекста: `"Link_Warehouse_ChemElements"`, `"Link_TaskCharge_Warehouse"`, `"Link_MeltingTask_Materials"`.


* **Видимость связей для подчиненных списков (1:N / `TableOneToMany`)**:
* Строки списков (`TableOneToMany`) не являются самостоятельными сущностями верхнего уровня.
* Включать для них видимость в целевом справочнике (`LinkVisibility.Anywhere` / флаг «Показывать связь в справочнике Б») технически противопоказано: это перегружает карточки классификаторов тысячами строчных ссылок.
* **Правило**: Для связей из таблиц $1:N$ видимость выставляется строго **`LinkVisibility.MasterOnly`**.


* **Исключение служебных символов (`<->`, `->`) в интерфейсе**:
* При создании двусторонней связи с видимостью `Anywhere` ядро DOCs автоматически генерирует обратную проекцию с системным маркером `<->` перед именем.
* **Правило**: Чтобы символы `<->` не попадали в наименование связи:
1. Использовать `LinkVisibility.MasterOnly` для подчиненных строк и справочников-библиотек.
2. Явно заполнять свойства `MasterName` и `SlaveName` чистыми строками предметной области.
3. Не отключать свойство `DoubleDirection` (оно отвечает за функциональность двусторонних выборок в БД, а не за текст интерфейса).




* **Конструктор связи для дочерних типов списка**:
* При создании связи для типа объекта **списка объектов** $1:N$ конструктор `new LinkGroupBuilder(...)` вызывается не для базового класса справочника, а для **типа объекта списка объектов**:
```csharp
ClassObject itemClass = chargeGroup.Classes.Find(chargeListName);
var link = new LinkGroupBuilder(chargeGroup, itemClass)
{
    Name = "Партия со склада",
    MasterName = "Партия со склада",
    SlaveName = "Списания в плавки",
    LinkVisibility = LinkVisibility.MasterOnly,
    LinkType = LinkType.ManyToOne,
    SlaveGroup = targetRef.ParameterGroup,
    TableName = "Link_TaskCharge_Warehouse"
};
link.Save();

```





---

## 7. Параметры со списками значений (`ValueList`)

* **Ограничения `ParameterInfoBuilder**`:
* Свойство `IsNewValueList` доступно **только для чтения** (`get`). Попытка присвоения вызывает ошибку компиляции `CS0200`.
* Свойство `ParameterValueList.Values` имеет уровень доступа `internal`/`protected`. Обращение напрямую вызывает ошибку `CS0122`.
* Класс `ListValue` не имеет конструкторов с 2 или 3 строковыми аргументами и требует передавать ссылку на владельца `ParameterValueList`.


* **Проблема состояния транзакции при активации**:
* Ручное добавление элементов в `ParameterValueList` на этапе низкоуровневого билдера часто оставляет внутреннее состояние группы невалидным, что приводит к исключению `InvalidOperationException: Операция является недопустимой из-за текущего состояния объекта` при последующем вызове `refBuilder.Activate()`.
* Попытка модифицировать `param.ValueList.AddValue(...)` после активации справочника выбрасывает `NotSupportedException` («Указанный метод не поддерживается»).


* **Best Practice**:
* При программной генерации метаданных перечисления задаются как строковые параметры (`ParameterType.NVarChar`).
* Если список значений строго необходим в метаданных, он настраивается через подключение справочника-классификатора либо через пользовательский интерфейс DOCs после чистой активации структуры.



---

## 8. Поиск параметров в иерархии групп (`ParameterGroup`)

* **Разделение корневых и табличных параметров**:
* Свойство `reference.ParameterGroup.Parameters` содержит параметры **только системной корневой таблицы**.
* Пользовательские параметры группы 1:1 («Свойства объекта») физически находятся в дочерней таблице `reference.ParameterGroup.OneToOneTables[0].Parameters`.
* Попытка прямого вызова `reference.ParameterGroup.Parameters.Find("ПользовательскийПараметр")` возвращает `null` и приводит к исключению «Параметр не найден».


* **Безопасные паттерны поиска**:
* Через фасад:
```csharp
ParameterInfo pi = reference.ParameterGroup.OneToOneParameters.FindByName("ИмяПараметра");

```


* Через обход всех групп 1:1:
```csharp
ParameterInfo pi = null;
foreach (ParameterGroup g in reference.ParameterGroup.OneToOneTables)
{
    pi = g.Parameters.Find("ИмяПараметра");
    if (pi != null) break;
}

```





---

## 9. Жизненный цикл объектов и пакетное сохранение

* **Создание объекта (`CreateReferenceObject`)**:
* Метод `reference.CreateReferenceObject(targetClass)` возвращает объект, который **уже находится в режиме редактирования (`Changing == true`)**.
* **Запрещено** вызывать `obj.BeginChanges()` сразу после создания нового объекта.


* **Пакетная фиксация изменений (`Reference.EndChanges`)**:
* Метод `Reference.EndChanges(IEnumerable<ReferenceObject> objects)` ожидает, что каждый объект коллекции **находится в режиме редактирования**.
* **Критическая ошибка**: если в цикле для каждого объекта вызвать `obj.EndChanges()`, а затем передать список в `Reference.EndChanges(list)`, платформа выбросит `System.ArgumentException: Объект '...' не находится в режиме редактирования`.
* **Правильный паттерн пакетного изменения**:
```csharp
List<ReferenceObject> modified = new List<ReferenceObject>();
foreach (ReferenceObject obj in objectsToUpdate)
{
    obj.BeginChanges(false);
    obj[piTarget].Value = newValue;
    // obj.EndChanges() ЗДЕСЬ НЕ ВЫЗЫВАЕТСЯ!
    modified.Add(obj);
}
// Единая транзакция сохранения
Reference.EndChanges(modified);

```





---

## 10. Установка связей через макроязык

* Свойство `ParameterGroup.Links` является внутренним (`internal`).
* В макросах привязка связанного объекта выполняется через высокоуровневый интерфейс объекта:
```csharp
// По имени связи
объект.СвязанныйОбъект["Марка сплава"] = materialObject;
// Либо через SetLinkedObject по сохраненному Guid связи
normObj.SetLinkedObject(linkGuid, targetObject);

```