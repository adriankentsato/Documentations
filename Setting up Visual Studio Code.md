# Setting up Visual Studio Code

Please see [Microsoft Windows Development Setup | Visual Studio Code Installation](./Windows%20Development%20Environment.md#visual-studio-code-installation) for instructions on how to intstall vscode.

## Data and tmp folders

As for the instructions on the installation of vscode, we are setting it up with portability in mind. With that, we need to add 2 folders in the `vscode` folder in order for it to become portable.

Create a `data` folder inside the `vscode` folder, then double click on the `data` folder and then create a new folder named `tmp`.

And that's it, now our installation of vscode is portable.

## Settings

Just copy these settings into your vscode's settings.json.

<details>
    <summary>settings.json</summary>

```json
{
    "workbench.sideBar.location": "right",
    "files.eol": "\n",
    "telemetry.telemetryLevel": "off",
    "git.path": "C:/SW/git/cmd/git.exe",
    "terminal.integrated.profiles.windows": {
        "PowerShell": {
            "source": "PowerShell",
            "icon": "terminal-powershell"
        },
        "Command Prompt": {
            "path": [
                "${env:windir}\\Sysnative\\cmd.exe",
                "${env:windir}\\System32\\cmd.exe"
            ],
            "args": [
                "/k",
                "C:/SW/git/bin/bash",
                "--login",
                "-i"
            ],
            "icon": "terminal-cmd"
        },
        "Git Bash": {
            "source": "Git Bash"
        }
    },
    "terminal.integrated.defaultProfile.windows": "Command Prompt",
    "editor.minimap.enabled": false
}
```
</details>

