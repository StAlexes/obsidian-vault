

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

        string projectDir = @"c:\Users\Aseev\VS Code Projects\TFlexMacrosTest\TFlexMacrosTest";
        string filePath = Path.Combine(projectDir, "ClassTemp.cs");

        // 1. Выгружаем код из базы в файл
        string currentCode = macroObj["Текст программы"].ToString();
        File.WriteAllText(filePath, currentCode, System.Text.Encoding.UTF8);

        // 2. Запускаем VS Code с флагом --wait (ждем закрытия вкладки!)
        var process = Process.Start(new ProcessStartInfo
        {
            FileName = "cmd.exe",
            Arguments = $"/c code --wait \"{filePath}\"",
            CreateNoWindow = true,
            UseShellExecute = false
        });

        // 3. T-FLEX DOCs ждет, пока ты закроешь файл в VS Code
        process.WaitForExit();

        // 4. Как только вкладка закрылась — автоматически забираем код обратно!
        if (File.Exists(filePath))
        {
            string updatedCode = File.ReadAllText(filePath, System.Text.Encoding.UTF8);

            macroObj.BeginChanges();
            macroObj["Текст программы"] = updatedCode;
            macroObj.Save();

            Message("Авто-синхронизация", "Вкладка закрыта. Свежий код автоматически сохранен в T-FLEX DOCs!", null);
        }
    }
}
```