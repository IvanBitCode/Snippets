# Measure Elapsed Time

```cs
using System.Diagnostics

var watch = new Stopwatch();
watch.Start()
/* Consuming time process */
watch.stop();

double minutes = ((double)(watch.ElapsedMilliseconds / 1000)) / 60;
Console.Writeline($"It took {minutes:0.00} minutes");
```