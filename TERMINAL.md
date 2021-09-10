```json
{
  "$schema": "https://aka.ms/terminal-profiles-schema",
  "actions": [
    {
      "command": {
        "action": "copy",
        "singleLine": false
      },
      "keys": "ctrl+c"
    },
    {
      "command": "paste",
      "keys": "ctrl+v"
    },
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
        "action": "openSettings",
        "target": "settingsUI"
      },
      "keys": "ctrl+shift+s"
    },
    {
      "command": {
        "action": "closeTab"
      },
      "keys": "ctrl+q"
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
        "action": "newTab",
        "index": 1
      },
      "keys": "ctrl+2"
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
        "action": "newTab",
        "index": 4
      },
      "keys": "ctrl+5"
    }
  ],
  "confirmCloseAllTabs": false,
  "copyFormatting": "none",
  "copyOnSelect": true,
  "defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
  "initialCols": 140,
  "initialPosition": "400,50",
  "initialRows": 44,
  "launchMode": "default",
  "profiles": {
    "defaults": {
      "colorScheme": "Dracula",
      "font": {
        "face": "CaskaydiaCove NF"
      }
    },
    "list": [
      {
        "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
        "hidden": false,
        "icon": "ms-appx:///ProfileIcons/{61c54bbd-c2c6-5271-96e7-009a87ff44bf}.png",
        "name": "PowerShell",
        "source": "Windows.Terminal.PowershellCore",
        "tabTitle": "PWSH"
      },
      {
        "commandline": "powershell Start-Process -Verb RunAs cmd.exe '/c start wt.exe'",
        "guid": "{fc912aec-fe4e-4667-b7cd-9f4fd2c162de}",
        "hidden": false,
        "icon": "ms-appx:///ProfileIcons/{61c54bbd-c2c6-5271-96e7-009a87ff44bf}.png",
        "name": "PowerShell Admin",
        "tabTitle": "PWSH Admin"
      },
      {
        "commandline": "cmd.exe",
        "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
        "hidden": false,
        "name": "Command",
        "tabTitle": "CMD"
      },
      {
        "guid": "{2c4de342-38b7-51cf-b940-2309a097f518}",
        "hidden": false,
        "name": "Ubuntu",
        "source": "Windows.Terminal.Wsl"
      },
      {
        "commandline": "ssh ubuntu@vm-apps-aws.softclass.com.br -o StrictHostKeyChecking=no",
        "guid": "{6e71fbe8-9b70-47a1-9e08-91426e5415e1}",
        "hidden": false,
        "name": "AWS",
        "tabTitle": "AWS"
      },
      {
        "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
        "hidden": true,
        "name": "Azure",
        "source": "Windows.Terminal.Azure"
      },
      {
        "colorScheme": "Campbell Powershell",
        "commandline": "powershell.exe",
        "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
        "hidden": true,
        "name": "PowerShell",
        "tabTitle": "PWSH"
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
      "background": "#272935",
      "black": "#21222C",
      "blue": "#BD93F9",
      "brightBlack": "#6272A4",
      "brightBlue": "#D6ACFF",
      "brightCyan": "#A4FFFF",
      "brightGreen": "#69FF94",
      "brightPurple": "#FF92DF",
      "brightRed": "#FF6E6E",
      "brightWhite": "#F8F8F2",
      "brightYellow": "#FFFFA5",
      "cursorColor": "#FFFFFF",
      "cyan": "#8BE9FD",
      "foreground": "#F8F8F2",
      "green": "#50FA7B",
      "name": "Dracula",
      "purple": "#FF79C6",
      "red": "#FF5555",
      "selectionBackground": "#FFFFFF",
      "white": "#F8F8F2",
      "yellow": "#FFB86C"
    }
  ],
  "showTabsInTitlebar": false,
  "startOnUserLogin": true,
  "tabWidthMode": "titleLength",
  "theme": "dark",
  "wordDelimiters": " ./\\()\"'-:,.;<>~!@#$%^&*|+=[]{}~?\u2502"
}
```
