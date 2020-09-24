```code
{
  // global settings https://aka.ms/terminal-global-settings
  // profiles settings https://aka.ms/terminal-profile-settings
  // color schemes https://aka.ms/terminal-color-schemes
  // about selection https://aka.ms/terminal-selection
  // actions and keybindings https://aka.ms/terminal-keybindings
  // about panes https://aka.ms/terminal-panes
  "$schema": "https://aka.ms/terminal-profiles-schema",
  "defaultProfile": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
  "copyOnSelect": true,
  "copyFormatting": false,
  "initialCols": 140,
  "initialRows": 35,
  "theme": "dark",
  "showTabsInTitlebar": true,
  "showTerminalTitleInTitlebar": false,
  "tabWidthMode": "compact",
  "wordDelimiters": " ./\\()\"'-:,.;<>~!@#$%^&*|+=[]{}~?\u2502",
  "profiles": {
    "defaults": {
      "acrylicOpacity": 0.75,
      "backgroundImageOpacity": 0.1,
      "closeOnExit": true,
      "colorScheme": "One Half Dark",
      "cursorColor": "#FFFFFF",
      "cursorShape": "bar",
      "fontFace": "MesloLGS NF",
      "fontSize": 13,
      "historySize": 9001,
      "padding": "0, 0, 0, 0",
      "snapOnInput": true,
      "useAcrylic": false
    },
    "list": [
      {
        "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
        "name": "PowerShell",
        "commandline": "powershell.exe",
        "hidden": false
      },
      {
        "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
        "name": "Command",
        "commandline": "cmd.exe",
        "hidden": false
      },
      {
        "guid": "{c6eaf9f4-32a7-5fdc-b5cf-066e8a4b1e40}",
        "name": "Ubuntu",
        "hidden": false,
        "source": "Windows.Terminal.Wsl",
        "icon": "ms-appx:///ProfileIcons/{9acb9455-ca41-5af7-950f-6bca1bc9722f}.png"
      },
      {
        "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
        "name": "Azure",
        "hidden": true,
        "source": "Windows.Terminal.Azure"
      }
    ]
  },
  "schemes": [
    {
      "background": "#0c0c0c",
      "black": "#0C0C0C",
      "blue": "#1170b5",
      "brightBlack": "#5A6374",
      "brightBlue": "#61AFEF",
      "brightCyan": "#56B6C2",
      "brightGreen": "#98C379",
      "brightPurple": "#C678DD",
      "brightRed": "#E06C75",
      "brightWhite": "#DCDFE4",
      "brightYellow": "#E5C07B",
      "cyan": "#56B6C2",
      "foreground": "#DCDFE4",
      "green": "#98C379",
      "name": "One Half Dark",
      "purple": "#C678DD",
      "red": "#E06C75",
      "white": "#DCDFE4",
      "yellow": "#E5C07B"
    }
  ],
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
      "keys": "alt+shift+d"
    }
  ]
}
```
