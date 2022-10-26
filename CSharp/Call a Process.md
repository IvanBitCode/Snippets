# Call a Process

```cs
private static void StartProcess(string command)
{
    Process proc = new Process();
    proc.StartInfo.UseShellExecute = false; // To set RedirectStandardOutput to true
    proc.StartInfo.RedirectStandardOutput = true;
    proc.StartInfo.RedirectStandardError = true;
    proc.StartInfo.CreateNoWindow = true; // Do not open the terminal
    proc.StartInfo.FileName = "cmd.exe";
    proc.StartInfo.Arguments = $"/c {command}";
    proc.OutputDataReceived += Proc_OutputDataReceived;
    proc.ErrorDataReceived += Proc_OutputDataReceived;
    proc.Start();
    proc.BeginOutputReadLine();
    proc.BeginErrorReadLine();
    proc.WaitForExit();
    proc.Close();
}
```

Define the event handlers:
```cs
private void Proc_OutputDataReceived(object sender, DataReceivedEventArgs e)
{
    if (!string.IsNullOrEmpty(e.Data))
        Console.WriteLine(e.Data)
}
```