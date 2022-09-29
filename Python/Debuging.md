# Debugging
To debug a python file:

1. Create a folder to save your python file.
2. Open your python file and then go to **Run and Debug** (Ctrl + Shift + D).
3. In the Run and Debug side bar, click on **open a folder** to create a **.vscode** folder.
4. Select the folder where your python file is located.
5. From the Run and Debug side bar, click on **create a launch.json file**. This file will be created inside .vscode folder.

<img src="https://code.visualstudio.com/assets/docs/editor/debugging/launch-configuration.png" alt="launch_config" width="400"/>

6. Select **Python File** in the Debugging Configuration dialog that will appear.
7. Open **launch.json** in VSCode and configure it as follow:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Python: Current File",
      "type": "python",
      "request": "launch",
      "program": "${file}"
      "console": "integratedTerminal",
      "justMyCode": true,
      "args": ["file", "c:/Users/Documents/pFile.txt", "clear"]
    }
  ]
}
```

Note that arguments that have a value must be two separated entries in the args attribute.

8. From Run a Debug side bar, click on **green arrow** to start debugging (or press F5). Once a debug session starts, the **Debug toolbar** will appear on the top of the editor.

<img src="https://code.visualstudio.com/assets/docs/editor/debugging/debugging_hero.png" alt="start_debugging" width="700"/>

Run (Start Without Debugging) action is triggered with Ctrl + F5 and uses the currently selected launch configuration.