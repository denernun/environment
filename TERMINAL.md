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

Set-Alias g git
# Import the Chocolatey Profile that contains the necessary code to enable
# tab-completions to function for `choco`.
# Be aware that if you are missing these lines from your profile, tab completion
# for `choco` will not function.
# See https://ch0.co/tab-completion for details.
$ChocolateyProfile = "$env:ChocolateyInstall\helpers\chocolateyProfile.psm1"
if (Test-Path($ChocolateyProfile)) {
  Import-Module "$ChocolateyProfile"
}
```
### ohmyposh.omp.json
```json
{
  "$schema": "https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/schema.json",
  "blocks": [
    {
      "alignment": "left",
      "segments": [
        {
          "type": "session",
          "foreground": "#ffffff",
          "background": "#cc3802",
          "leading_diamond": "\ue0b6",
          "style": "diamond",
          "template": "{{ .UserName }} "
        },
        {
          "type": "path",
          "style": "powerline",
          "powerline_symbol": "\ue0b0",
          "foreground": "#ffffff",
          "background": "#047e84",
          "properties": {
            "style": "folder"
          },
          "template": " {{ .Path }} "
        },
        {
          "type": "git",
          "style": "powerline",
          "powerline_symbol": "",
          "foreground": "#193549",
          "background": "#ffeb3b",
          "background_templates": [
            "{{ if or (.Working.Changed) (.Staging.Changed) }}#FFEB3B{{ end }}",
            "{{ if and (gt .Ahead 0) (gt .Behind 0) }}#FFCC80{{ end }}",
            "{{ if gt .Ahead 0 }}#B388FF{{ end }}",
            "{{ if gt .Behind 0 }}#B388FB{{ end }}"
          ],
          "template": "{{ .UpstreamIcon }}{{ .HEAD }}{{if .BranchStatus }} {{ .BranchStatus }}{{ end }}{{ if .Working.Changed }} \uF044 {{ .Working.String }}{{ end }}{{ if and (.Working.Changed) (.Staging.Changed) }} |{{ end }}{{ if .Staging.Changed }} \uF046 {{ .Staging.String }}{{ end }}{{ if gt .StashCount 0 }}  {{ .StashCount }}{{ end }}",
          "properties": {
            "fetch_status": true,
            "fetch_stash_count": true,
            "fetch_upstream_icon": true
          }
        }
      ],
      "type": "prompt"
    },
    {
      "alignment": "right",
      "segments": [
        {
          "type": "angular",
          "style": "powerline",
          "powerline_symbol": "",
          "foreground": "#ffffff",
          "background": "#dd0031",
          "template": "  {{ .Full }} "
        },
        {
          "type": "node",
          "style": "powerline",
          "powerline_symbol": "\ue0b0",
          "foreground": "#ffffff",
          "background": "#6ca35e",
          "template": " \ue718 {{ if .PackageManagerIcon }}{{ .PackageManagerIcon }} {{ end }}{{ .Full }} "
        }
      ],
      "type": "rprompt"
    }
  ],
  "final_space": true,
  "version": 2
}
```
### terminal.omp.json
```json
{
  "$help": "https://aka.ms/terminal-documentation",
  "$schema": "https://aka.ms/terminal-profiles-schema",
  "actions": [
    {
      "command": "find",
      "keys": "ctrl+shift+f"
    },
    {
      "command": {
        "action": "splitPane",
        "split": "auto",
        "splitMode": "duplicate"
      },
      "keys": "ctrl+shift+a"
    },
    {
      "command": {
        "action": "newTab",
        "index": 1
      },
      "keys": "ctrl+2"
    },
    {
      "command": "paste",
      "keys": "ctrl+v"
    },
    {
      "command": {
        "action": "copy",
        "singleLine": false
      },
      "keys": "ctrl+c"
    },
    {
      "command": {
        "action": "newTab",
        "index": 2
      },
      "keys": "ctrl+3"
    },
    {
      "command": {
        "action": "newTab",
        "index": 3
      },
      "keys": "ctrl+4"
    },
    {
      "command": {
        "action": "openSettings",
        "target": "settingsUI"
      },
      "keys": "ctrl+shift+s"
    },
    {
      "command": {
        "action": "newTab",
        "index": 0
      },
      "keys": "ctrl+1"
    },
    {
      "command": {
        "action": "closeTab"
      },
      "keys": "ctrl+q"
    }
  ],
  "alwaysShowNotificationIcon": false,
  "confirmCloseAllTabs": false,
  "copyFormatting": "none",
  "copyOnSelect": true,
  "defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
  "firstWindowPreference": "defaultProfile",
  "focusFollowMouse": true,
  "initialCols": 140,
  "initialPosition": "400,50",
  "initialRows": 36,
  "launchMode": "default",
  "minimizeToNotificationArea": false,
  "newTabMenu": [
    {
      "type": "remainingProfiles"
    }
  ],
  "profiles": {
    "defaults": {
      "colorScheme": "Dracula",
      "elevate": true,
      "font": {
        "face": "MesloLGM NF",
        "size": 11.0
      }
    },
    "list": [
      {
        "elevate": true,
        "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
        "hidden": false,
        "icon": "ms-appx:///ProfileIcons/{61c54bbd-c2c6-5271-96e7-009a87ff44bf}.png",
        "name": "PWSH",
        "source": "Windows.Terminal.PowershellCore",
        "tabTitle": "PWSH",
        "tabColor": "#0614da",
        "useAcrylic": true,
        "useAtlasEngine": true
      },
      {
        "elevate": true,
        "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
        "hidden": false,
        "icon": "ms-appx:///ProfileIcons/{0caa0dad-35be-5f56-a8ff-afceeeaa6101}.png",
        "name": "CMD",
        "tabTitle": "CMD",
        "tabColor": "#18b320",
        "useAcrylic": true,
        "useAtlasEngine": true
      },
      {
        "colorScheme": "Ubuntu",
        "commandline": "C:\\WINDOWS\\system32\\wsl.exe -d Ubuntu",
        "guid": "{871d25db-4454-4805-824a-c08d776c03e7}",
        "hidden": false,
        "icon": "ms-appx:///ProfileIcons/{9acb9455-ca41-5af7-950f-6bca1bc9722f}.png",
        "name": "WSL",
        "startingDirectory": "~",
        "tabTitle": "WSL",
        "tabColor": "#ad157d"
      },
      {
        "guid": "{690b1101-25f1-574b-a7bc-e22760b35aa3}",
        "hidden": true,
        "name": "Developer Command Prompt for VS 2022",
        "source": "Windows.Terminal.VisualStudio"
      },
      {
        "guid": "{96e174d1-77cc-5740-a2f7-945e715ef083}",
        "hidden": true,
        "name": "Developer PowerShell for VS 2022",
        "source": "Windows.Terminal.VisualStudio"
      },
      {
        "elevate": true,
        "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
        "hidden": true,
        "name": "PowerShell"
      },
      {
        "guid": "{16208362-94fc-5b1f-a491-5b2624d5ab56}",
        "hidden": true,
        "name": "Visual Studio Debug Console",
        "source": "VSDebugConsole"
      }
    ]
  },
  "schemes": [
    {
      "background": "#0C0C0C",
      "black": "#0C0C0C",
      "blue": "#0037DA",
      "brightBlack": "#767676",
      "brightBlue": "#3B78FF",
      "brightCyan": "#61D6D6",
      "brightGreen": "#16C60C",
      "brightPurple": "#B4009E",
      "brightRed": "#E74856",
      "brightWhite": "#F2F2F2",
      "brightYellow": "#F9F1A5",
      "cursorColor": "#FFFFFF",
      "cyan": "#3A96DD",
      "foreground": "#CCCCCC",
      "green": "#13A10E",
      "name": "Campbell",
      "purple": "#881798",
      "red": "#C50F1F",
      "selectionBackground": "#FFFFFF",
      "white": "#CCCCCC",
      "yellow": "#C19C00"
    },
    {
      "background": "#012456",
      "black": "#0C0C0C",
      "blue": "#0037DA",
      "brightBlack": "#767676",
      "brightBlue": "#3B78FF",
      "brightCyan": "#61D6D6",
      "brightGreen": "#16C60C",
      "brightPurple": "#B4009E",
      "brightRed": "#E74856",
      "brightWhite": "#F2F2F2",
      "brightYellow": "#F9F1A5",
      "cursorColor": "#FFFFFF",
      "cyan": "#3A96DD",
      "foreground": "#CCCCCC",
      "green": "#13A10E",
      "name": "Campbell Powershell",
      "purple": "#881798",
      "red": "#C50F1F",
      "selectionBackground": "#FFFFFF",
      "white": "#CCCCCC",
      "yellow": "#C19C00"
    },
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
      "background": "#282C34",
      "black": "#282C34",
      "blue": "#61AFEF",
      "brightBlack": "#5A6374",
      "brightBlue": "#61AFEF",
      "brightCyan": "#56B6C2",
      "brightGreen": "#98C379",
      "brightPurple": "#C678DD",
      "brightRed": "#E06C75",
      "brightWhite": "#DCDFE4",
      "brightYellow": "#E5C07B",
      "cursorColor": "#FFFFFF",
      "cyan": "#56B6C2",
      "foreground": "#DCDFE4",
      "green": "#98C379",
      "name": "One Half Dark",
      "purple": "#C678DD",
      "red": "#E06C75",
      "selectionBackground": "#FFFFFF",
      "white": "#DCDFE4",
      "yellow": "#E5C07B"
    },
    {
      "background": "#FAFAFA",
      "black": "#383A42",
      "blue": "#0184BC",
      "brightBlack": "#4F525D",
      "brightBlue": "#61AFEF",
      "brightCyan": "#56B5C1",
      "brightGreen": "#98C379",
      "brightPurple": "#C577DD",
      "brightRed": "#DF6C75",
      "brightWhite": "#FFFFFF",
      "brightYellow": "#E4C07A",
      "cursorColor": "#4F525D",
      "cyan": "#0997B3",
      "foreground": "#383A42",
      "green": "#50A14F",
      "name": "One Half Light",
      "purple": "#A626A4",
      "red": "#E45649",
      "selectionBackground": "#FFFFFF",
      "white": "#FAFAFA",
      "yellow": "#C18301"
    },
    {
      "background": "#002B36",
      "black": "#002B36",
      "blue": "#268BD2",
      "brightBlack": "#073642",
      "brightBlue": "#839496",
      "brightCyan": "#93A1A1",
      "brightGreen": "#586E75",
      "brightPurple": "#6C71C4",
      "brightRed": "#CB4B16",
      "brightWhite": "#FDF6E3",
      "brightYellow": "#657B83",
      "cursorColor": "#FFFFFF",
      "cyan": "#2AA198",
      "foreground": "#839496",
      "green": "#859900",
      "name": "Solarized Dark",
      "purple": "#D33682",
      "red": "#DC322F",
      "selectionBackground": "#FFFFFF",
      "white": "#EEE8D5",
      "yellow": "#B58900"
    },
    {
      "background": "#FDF6E3",
      "black": "#002B36",
      "blue": "#268BD2",
      "brightBlack": "#073642",
      "brightBlue": "#839496",
      "brightCyan": "#93A1A1",
      "brightGreen": "#586E75",
      "brightPurple": "#6C71C4",
      "brightRed": "#CB4B16",
      "brightWhite": "#FDF6E3",
      "brightYellow": "#657B83",
      "cursorColor": "#002B36",
      "cyan": "#2AA198",
      "foreground": "#657B83",
      "green": "#859900",
      "name": "Solarized Light",
      "purple": "#D33682",
      "red": "#DC322F",
      "selectionBackground": "#FFFFFF",
      "white": "#EEE8D5",
      "yellow": "#B58900"
    },
    {
      "background": "#000000",
      "black": "#000000",
      "blue": "#3465A4",
      "brightBlack": "#555753",
      "brightBlue": "#729FCF",
      "brightCyan": "#34E2E2",
      "brightGreen": "#8AE234",
      "brightPurple": "#AD7FA8",
      "brightRed": "#EF2929",
      "brightWhite": "#EEEEEC",
      "brightYellow": "#FCE94F",
      "cursorColor": "#FFFFFF",
      "cyan": "#06989A",
      "foreground": "#D3D7CF",
      "green": "#4E9A06",
      "name": "Tango Dark",
      "purple": "#75507B",
      "red": "#CC0000",
      "selectionBackground": "#FFFFFF",
      "white": "#D3D7CF",
      "yellow": "#C4A000"
    },
    {
      "background": "#FFFFFF",
      "black": "#000000",
      "blue": "#3465A4",
      "brightBlack": "#555753",
      "brightBlue": "#729FCF",
      "brightCyan": "#34E2E2",
      "brightGreen": "#8AE234",
      "brightPurple": "#AD7FA8",
      "brightRed": "#EF2929",
      "brightWhite": "#EEEEEC",
      "brightYellow": "#FCE94F",
      "cursorColor": "#000000",
      "cyan": "#06989A",
      "foreground": "#555753",
      "green": "#4E9A06",
      "name": "Tango Light",
      "purple": "#75507B",
      "red": "#CC0000",
      "selectionBackground": "#FFFFFF",
      "white": "#D3D7CF",
      "yellow": "#C4A000"
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
    },
    {
      "background": "#000000",
      "black": "#000000",
      "blue": "#000080",
      "brightBlack": "#808080",
      "brightBlue": "#0000FF",
      "brightCyan": "#00FFFF",
      "brightGreen": "#00FF00",
      "brightPurple": "#FF00FF",
      "brightRed": "#FF0000",
      "brightWhite": "#FFFFFF",
      "brightYellow": "#FFFF00",
      "cursorColor": "#FFFFFF",
      "cyan": "#008080",
      "foreground": "#C0C0C0",
      "green": "#008000",
      "name": "Vintage",
      "purple": "#800080",
      "red": "#800000",
      "selectionBackground": "#FFFFFF",
      "white": "#C0C0C0",
      "yellow": "#808000"
    }
  ],
  "showTabsInTitlebar": false,
  "startOnUserLogin": false,
  "tabWidthMode": "titleLength",
  "theme": "dark",
  "themes": [],
  "wordDelimiters": " ./\\()\"'-:,.;<>~!@#$%^&*|+=[]{}~?\u2502"
}
```
### scoop
```text
PowerShell Admin
irm get.scoop.sh -outfile 'install.ps1'
.\install.ps1 -RunAsAdmin
Path
C:\Users\dener\scoop\shims
```
### z
```text
Install-Module -Name Z -Force  -AllowClobber
```
### zsh
```text
sudo apt install zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
nano .zshrc
theme (af-magic)
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
nano .zshrc
plugins (zsh-autosuggestions)
```

