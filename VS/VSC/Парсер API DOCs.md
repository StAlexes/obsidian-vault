

```C#
using System;
using System.IO;
using System.Linq;
using System.Reflection;
using System.Text;
using System.Text.RegularExpressions;
using System.Collections.Generic;

public class ApiDumper
{
    public static void Main(string[] args)
    {
        Console.WriteLine("Генерируем умную версию API с русскими алиасами и флагами Async...");
        ExportTFlexApiToMarkdown();
        Console.WriteLine("Готово! Проверь tflex_docs_api_smart.md");
    }

    public static void ExportTFlexApiToMarkdown()
    {
        string tflexFolder = @"C:\Program Files (x86)\T-FLEX DOCs 18 (OAKrelease18)\Program";

        string[] targetAssemblies = {
            "TFlex.DOCs.Model.dll",
            "TFlex.DOCs.Model.Macros.dll",
            "TFlex.DOCs.Model.Classes.dll",
            "TFlex.DOCs.Model.References.dll",
            "TFlex.DOCs.Model.Entities.dll",
            "TFlex.DOCs.Model.UniversalPath.dll",
            "TFlex.DOCs.Model.StructuredDocuments.dll"
        };

        string[] ignoredMethods = { 
            "Equals", "GetHashCode", "GetType", "ToString", "MemberwiseClone", 
            "ReferenceEquals", "InitializeLifetimeService", "Dispose", "Clone" 
        };

        var sb = new StringBuilder();
        sb.AppendLine("# Справочник API T-FLEX DOCs (Smart Edition)");
        sb.AppendLine("> Приоритет: используй стандартные методы C# на английском языке. Пометки [RU alias] показывают русскоязычные аналоги, а [has Async] — наличие асинхронной версии метода.\n");

        foreach (var dllName in targetAssemblies)
        {
            string fullPath = Path.Combine(tflexFolder, dllName);
            if (!File.Exists(fullPath)) continue;

            try
            {
                var asm = Assembly.LoadFrom(fullPath);
                sb.AppendLine($"## {dllName}\n");

                var types = asm.GetExportedTypes()
                    .Where(t => t.IsPublic && (t.IsClass || t.IsInterface))
                    // Отсекаем UI, DTO, XML и технический шум
                    .Where(t => !t.Name.EndsWith("EventArgs") && 
                                !t.Name.EndsWith("EventHandler") && 
                                !t.Name.EndsWith("Exception") &&
                                !t.Name.EndsWith("Collection") &&
                                !t.Name.EndsWith("Description") &&
                                !t.Name.EndsWith("Dto") &&
                                !t.Name.EndsWith("Activity") &&
                                !t.Name.Contains("Xml") &&
                                !t.Name.Contains("Log") &&
                                !t.Name.Contains("Enumerator") &&
                                !t.Name.Contains("Internal") &&
                                !t.Name.StartsWith("<"))
                    .OrderBy(t => t.Name);

                foreach (var type in types)
                {
                    // --- 1. ОБРАБОТКА СВОЙСТВ ---
                    var allProps = type.GetProperties(BindingFlags.Public | BindingFlags.Instance | BindingFlags.Static | BindingFlags.DeclaredOnly).ToList();
                    var engProps = allProps.Where(p => !Regex.IsMatch(p.Name, @"\p{IsCyrillic}")).ToList();
                    var ruProps = allProps.Where(p => Regex.IsMatch(p.Name, @"\p{IsCyrillic}")).ToList();

                    var propLines = new List<string>();
                    foreach (var p in engProps)
                    {
                        // Ищем, есть ли русское свойство такого же типа
                        var ruMatch = ruProps.FirstOrDefault(r => r.PropertyType == p.PropertyType);
                        string ruNote = ruMatch != null ? $" [RU: {ruMatch.Name}]" : "";
                        propLines.Add($"{p.Name}: {p.PropertyType.Name}{ruNote}");
                    }
                    // Добавляем оставшиеся чисто русские свойства (если у них нет англ. пары)
                    foreach (var r in ruProps.Where(r => !engProps.Any(e => e.PropertyType == r.PropertyType)))
                    {
                        propLines.Add($"{r.Name}: {r.PropertyType.Name} [RU only]");
                    }

                    // --- 2. ОБРАБОТКА МЕТОДОВ ---
                    var allMethods = type.GetMethods(BindingFlags.Public | BindingFlags.Instance | BindingFlags.Static | BindingFlags.DeclaredOnly)
                        .Where(m => !m.IsSpecialName && !ignoredMethods.Contains(m.Name))
                        .ToList();

                    var engMethods = allMethods.Where(m => !Regex.IsMatch(m.Name, @"\p{IsCyrillic}") && !m.Name.EndsWith("Async"))
                        .GroupBy(m => m.Name)
                        .ToList();

                    var methodLines = new List<string>();

                    foreach (var group in engMethods)
                    {
                        string methodName = group.Key;
                        // Проверяем, существует ли Async аналог в этой же сборке
                        bool hasAsync = allMethods.Any(m => m.Name == methodName + "Async");
                        string asyncNote = hasAsync ? " [has Async]" : "";

                        // Проверяем наличие русскоязычного аналога
                        var ruMatch = allMethods.FirstOrDefault(m => Regex.IsMatch(m.Name, @"\p{IsCyrillic}") && 
                                                                     m.GetParameters().Length == group.First().GetParameters().Length);
                        string ruNote = ruMatch != null ? $" [RU: {ruMatch.Name}]" : "";

                        var best = group.OrderByDescending(m => m.GetParameters().Length).First();
                        var overloadsNote = group.Count() > 1 ? $" (+{group.Count() - 1})" : "";

                        methodLines.Add($"- `{best.ReturnType.Name} {best.Name}({string.Join(", ", best.GetParameters().Select(p => p.ParameterType.Name + " " + p.Name))}){overloadsNote}`{asyncNote}{ruNote}");
                    }

                    // Добавляем русские методы, у которых нет явных англ. аналогов
                    var soloRuMethods = allMethods.Where(m => Regex.IsMatch(m.Name, @"\p{IsCyrillic}"))
                        .GroupBy(m => m.Name);

                    foreach (var ruGroup in soloRuMethods)
                    {
                        // Если в англ списке нет метода с похожим смыслом
                        if (!methodLines.Any(line => line.Contains($"[RU: {ruGroup.Key}]")))
                        {
                            var best = ruGroup.OrderByDescending(m => m.GetParameters().Length).First();
                            methodLines.Add($"- `{best.ReturnType.Name} {best.Name}({string.Join(", ", best.GetParameters().Select(p => p.ParameterType.Name + " " + p.Name))})` [RU alternative]");
                        }
                    }

                    if (!propLines.Any() && !methodLines.Any()) continue;

                    sb.AppendLine($"### `{type.Name}`");
                    if (propLines.Any())
                    {
                        sb.AppendLine($"**Свойства:** {string.Join(", ", propLines)}");
                    }
                    if (methodLines.Any())
                    {
                        sb.AppendLine("**Методы:**");
                        foreach (var m in methodLines) sb.AppendLine(m);
                    }
                    sb.AppendLine();
                }
            }
            catch (Exception ex)
            {
                sb.AppendLine($"Ошибка: {ex.Message}\n");
            }
        }

        File.WriteAllText("tflex_docs_api_smart.md", sb.ToString(), Encoding.UTF8);
    }
}
```
