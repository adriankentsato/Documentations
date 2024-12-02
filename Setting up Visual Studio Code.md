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
    "workbench.startupEditor": "none",
    "workbench.sideBar.location": "right",
    "files.eol": "\n",
    "telemetry.telemetryLevel": "off",
    "editor.rulers": [80, 120],
    "editor.tabSize": 4,
    "git.path": "C:/SW/git/cmd/git.exe",
    "editor.minimap.enabled": false,
    "editor.wordWrap": "on",
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
            "args": [],
            "icon": "terminal-cmd"
        },
        "Git Bash": {
            "source": "Git Bash"
        },
        "MINGW": {
            "path": [
                "${env:windir}\\Sysnative\\cmd.exe",
                "${env:windir}\\System32\\cmd.exe"
            ],
            "args": [
                "/k",
                "C:/SW/msys/msys2_shell.cmd",
                "-defterm",
                "-here",
                "-no-start",
                "-mingw64"
            ],
            "icon": "terminal-cmd"
        },
    },
    "terminal.integrated.defaultProfile.windows": "MINGW",
    "editor.minimap.enabled": false,
    "editor.stickyScroll.enabled": false,
    "gitlens.telemetry.enabled": false,
    "gitlens.views.scm.grouped.views": {
        "commits": false,
        "branches": true,
        "remotes": true,
        "stashes": false,
        "tags": true,
        "worktrees": true,
        "contributors": true,
        "repositories": true,
        "searchAndCompare": true,
        "launchpad": true
    },
    "java.configuration.runtimes": [
        {
            "name": "JavaSE-23",
            "default": true,
            "path": "c:/sw/jdk-23.0.1"
        }
    ],
    "java.jdt.ls.java.home": "c:/sw/jdk-23.0.1"
}
```
</details>

