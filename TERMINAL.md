### fonts
```text
oh-my-posh font install

Caskaydia Cove Nerd Font
https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/CascadiaCode.zip?WT.mc_id=-blog-scottha
```
### install 
```text
Set-ExecutionPolicy Unrestricted
winget install JanDeDobbeleer.OhMyPosh -s winget
(Get-Command oh-my-posh).Source
Install-Module -Name Terminal-Icons -Repository PSGallery
https://www.powershellgallery.com/packages?q=PSReadLine
Install-Module -Name PSReadLine -AllowPrerelease
```
### config
```text
code $PROFILE

Import-Module -Name Terminal-Icons
oh-my-posh --init --shell pwsh --config C:\Users\dener\OneDrive\ohmyposh.omp.json | Invoke-Expression

Import-Module PSReadLine
Set-PSReadLineOption -EditMode Windows
Set-PSReadLineOption -PredictionSource History
Set-PSReadLineOption -PredictionViewStyle ListView
Set-PSReadLineOption -Colors @{ InlinePrediction = '#8A0303'}
Set-PSReadLineOption -Colors @{ InlinePrediction = '#2F7004'}
Set-PSReadLineOption -Colors @{ InlinePrediction = "$([char]0x1b)[36;7;238m"}
Set-PSReadlineKeyHandler -Key Tab -Function MenuComplete
Set-PSReadlineKeyHandler -Key UpArrow -Function HistorySearchBackward
Set-PSReadlineKeyHandler -Key DownArrow -Function HistorySearchForward
```
### ohmyposh.omp.json
```json
{
  "$schema": "https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/schema.json",
  "blocks": [
    {
      "type": "prompt",
      "alignment": "left",
      "segments": [
        {
          "properties": {
            "cache_duration": "none"
          },
          "leading_diamond": "\ue0b6",
          "template": "{{ .UserName }} ",
          "foreground": "#ffffff",
          "background": "#cc3802",
          "type": "session",
          "style": "diamond"
        },
        {
          "properties": {
            "cache_duration": "none",
            "style": "folder"
          },
          "template": " {{ .Path }} ",
          "foreground": "#ffffff",
          "powerline_symbol": "\ue0b0",
          "background": "#047e84",
          "type": "path",
          "style": "powerline"
        },
        {
          "properties": {
            "cache_duration": "none",
            "fetch_stash_count": true,
            "fetch_status": true,
            "fetch_upstream_icon": true
          },
          "template": "{{ .UpstreamIcon }}{{ .HEAD }}{{if .BranchStatus }} {{ .BranchStatus }}{{ end }}{{ if .Working.Changed }} \uf044 {{ .Working.String }}{{ end }}{{ if and (.Working.Changed) (.Staging.Changed) }} |{{ end }}{{ if .Staging.Changed }} \uf046 {{ .Staging.String }}{{ end }}{{ if gt .StashCount 0 }} \uf692 {{ .StashCount }}{{ end }}",
          "foreground": "#193549",
          "powerline_symbol": "\ue0b0",
          "background": "#ffeb3b",
          "type": "git",
          "style": "powerline",
          "background_templates": [
            "{{ if or (.Working.Changed) (.Staging.Changed) }}#FFEB3B{{ end }}",
            "{{ if and (gt .Ahead 0) (gt .Behind 0) }}#FFCC80{{ end }}",
            "{{ if gt .Ahead 0 }}#B388FF{{ end }}",
            "{{ if gt .Behind 0 }}#B388FB{{ end }}"
          ]
        }
      ]
    },
    {
      "type": "rprompt",
      "alignment": "right",
      "segments": [
      ]
    }
  ],
  "version": 3,
  "final_space": true
}
```
### terminal.json
```json
{
    "$help": "https://aka.ms/terminal-documentation",
    "$schema": "https://aka.ms/terminal-profiles-schema",
    "actions": 
    [
        {
            "command": 
            {
                "action": "splitPane",
                "split": "auto",
                "splitMode": "duplicate"
            },
            "id": "User.splitPane.A6751878"
        },
        {
            "command": "find",
            "id": "User.find"
        },
        {
            "command": 
            {
                "action": "newTab",
                "index": 1
            },
            "id": "User.newTab.1FA5EB5"
        },
        {
            "command": 
            {
                "action": "newTab",
                "index": 2
            },
            "id": "User.newTab.CCE909E3"
        },
        {
            "command": 
            {
                "action": "openSettings",
                "target": "settingsUI"
            },
            "id": "User.openSettings.6CD791B"
        },
        {
            "command": "paste",
            "id": "User.paste"
        },
        {
            "command": 
            {
                "action": "copy",
                "singleLine": false
            },
            "id": "User.copy.644BA8F2"
        },
        {
            "command": 
            {
                "action": "newTab",
                "index": 3
            },
            "id": "User.newTab.F4C304FB"
        },
        {
            "command": 
            {
                "action": "closeTab"
            },
            "id": "User.closeTab.0"
        },
        {
            "command": 
            {
                "action": "newTab",
                "index": 0
            },
            "id": "User.newTab.7975BEED"
        }
    ],
    "alwaysShowNotificationIcon": false,
    "compatibility.allowHeadless": true,
    "confirmCloseAllTabs": false,
    "copyFormatting": "none",
    "copyOnSelect": true,
    "defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
    "firstWindowPreference": "defaultProfile",
    "focusFollowMouse": true,
    "initialCols": 140,
    "initialPosition": "400,50",
    "initialRows": 36,
    "keybindings": 
    [
        {
            "id": "User.paste",
            "keys": "ctrl+v"
        },
        {
            "id": "User.find",
            "keys": "ctrl+shift+f"
        },
        {
            "id": "User.openSettings.6CD791B",
            "keys": "ctrl+shift+s"
        },
        {
            "id": "User.splitPane.A6751878",
            "keys": "ctrl+shift+a"
        },
        {
            "id": "User.newTab.1FA5EB5",
            "keys": "ctrl+2"
        },
        {
            "id": "User.newTab.F4C304FB",
            "keys": "ctrl+4"
        },
        {
            "id": "User.newTab.CCE909E3",
            "keys": "ctrl+3"
        },
        {
            "id": "User.copy.644BA8F2",
            "keys": "ctrl+c"
        },
        {
            "id": "User.newTab.7975BEED",
            "keys": "ctrl+1"
        },
        {
            "id": "User.closeTab.0",
            "keys": "ctrl+q"
        }
    ],
    "launchMode": "default",
    "minimizeToNotificationArea": false,
    "newTabMenu": 
    [
        {
            "type": "remainingProfiles"
        }
    ],
    "profiles": 
    {
        "defaults": 
        {
            "colorScheme": "Tango Dark",
            "elevate": true,
            "experimental.rightClickContextMenu": true,
            "font": 
            {
                "face": "MesloLGM NF",
                "size": 11
            }
        },
        "list": 
        [
            {
                "elevate": true,
                "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
                "hidden": false,
                "icon": "ms-appx:///ProfileIcons/{61c54bbd-c2c6-5271-96e7-009a87ff44bf}.png",
                "name": "PWSH",
                "opacity": 100,
                "source": "Windows.Terminal.PowershellCore",
                "tabColor": "#0614DA",
                "tabTitle": "PWSH",
                "useAcrylic": true
            },
            {
                "elevate": true,
                "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
                "hidden": false,
                "icon": "ms-appx:///ProfileIcons/{0caa0dad-35be-5f56-a8ff-afceeeaa6101}.png",
                "name": "CMD",
                "tabColor": "#18B320",
                "tabTitle": "CMD",
                "useAcrylic": true
            },
            {
                "guid": "{963ff2f7-6aed-5ce3-9d91-90d99571f53a}",
                "hidden": false,
                "name": "WSL",
                "source": "Windows.Terminal.Wsl"
            },
            {
                "guid": "{1cbbff2f-9a13-5774-9eb8-757b093b6b60}",
                "hidden": true,
                "name": "Developer Command Prompt for VS 2019",
                "source": "Windows.Terminal.VisualStudio"
            },
            {
                "guid": "{f61d197f-c9d1-504f-aa09-1bcd9384ccf2}",
                "hidden": true,
                "name": "Developer PowerShell for VS 2019",
                "source": "Windows.Terminal.VisualStudio"
            },
            {
                "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
                "hidden": true,
                "name": "Windows PowerShell"
            }
        ]
    },
    "schemes": 
    [
        {
            "background": "#282A36",
            "black": "#21222C",
            "blue": "#BD93F9",
            "brightBlack": "#6272A4",
            "brightBlue": "#D6ACFF",
            "brightCyan": "#A4FFFF",
            "brightGreen": "#69FF94",
            "brightPurple": "#FF92DF",
            "brightRed": "#FF6E6E",
            "brightWhite": "#FFFFFF",
            "brightYellow": "#FFFFA5",
            "cursorColor": "#F8F8F2",
            "cyan": "#8BE9FD",
            "foreground": "#F8F8F2",
            "green": "#50FA7B",
            "name": "Dracula",
            "purple": "#FF79C6",
            "red": "#FF5555",
            "selectionBackground": "#44475A",
            "white": "#F8F8F2",
            "yellow": "#F1FA8C"
        },
        {
            "background": "#300A24",
            "black": "#171421",
            "blue": "#0037DA",
            "brightBlack": "#767676",
            "brightBlue": "#08458F",
            "brightCyan": "#2C9FB3",
            "brightGreen": "#26A269",
            "brightPurple": "#A347BA",
            "brightRed": "#C01C28",
            "brightWhite": "#F2F2F2",
            "brightYellow": "#A2734C",
            "cursorColor": "#FFFFFF",
            "cyan": "#3A96DD",
            "foreground": "#FFFFFF",
            "green": "#26A269",
            "name": "Ubuntu",
            "purple": "#881798",
            "red": "#C21A23",
            "selectionBackground": "#FFFFFF",
            "white": "#CCCCCC",
            "yellow": "#A2734C"
        },
        {
            "background": "#300A24",
            "black": "#171421",
            "blue": "#0037DA",
            "brightBlack": "#767676",
            "brightBlue": "#08458F",
            "brightCyan": "#2C9FB3",
            "brightGreen": "#26A269",
            "brightPurple": "#A347BA",
            "brightRed": "#C01C28",
            "brightWhite": "#F2F2F2",
            "brightYellow": "#A2734C",
            "cursorColor": "#FFFFFF",
            "cyan": "#3A96DD",
            "foreground": "#FFFFFF",
            "green": "#26A269",
            "name": "Ubuntu-ColorScheme",
            "purple": "#881798",
            "red": "#C21A23",
            "selectionBackground": "#FFFFFF",
            "white": "#CCCCCC",
            "yellow": "#A2734C"
        }
    ],
    "showTabsInTitlebar": false,
    "startOnUserLogin": false,
    "tabWidthMode": "titleLength",
    "theme": "dark",
    "themes": [],
    "windowingBehavior": "useNew",
    "wordDelimiters": " ./\\()\"'-:,.;<>~!@#$%^&*|+=[]{}~?\u2502"
}
```
