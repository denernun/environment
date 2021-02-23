```code
{
  "$schema": "https://aka.ms/terminal-profiles-schema",
  "defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
  "copyOnSelect": true,
  "copyFormatting": false,
  "initialPosition": "400,50",
  "initialCols": 140,
  "initialRows": 40,
  "theme": "dark",
  "confirmCloseAllTabs": false,
  "tabWidthMode": "compact",
  "wordDelimiters": " ./\\()\"'-:,.;<>~!@#$%^&*|+=[]{}~?\u2502",
  "profiles": {
    "defaults": {
      "acrylicOpacity": 0.5,
      "backgroundImageOpacity": 0.5,
      "closeOnExit": true,
      "colorScheme": "Dracula",
      "cursorColor": "#FFFFFF",
      "cursorShape": "bar",
      "fontFace": "Fira Code",
      "fontSize": 10,
      "historySize": 9001,
      "padding": "0, 0, 0, 0",
      "snapOnInput": false,
      "useAcrylic": false
    },
    "list": [
      {
        "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
        "hidden": false,
        "name": "PowerShell",
        "source": "Windows.Terminal.PowershellCore"
      },
      {
        "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
        "hidden": false,
        "name": "Command",
        "commandline": "cmd.exe"
      },
      {
        "guid": "{07b52e3e-de2c-5db4-bd2d-ba144ed6c273}",
        "hidden": false,
        "name": "Ubuntu",
        "source": "Windows.Terminal.Wsl"
      },
      {
        "guid": "{73225108-7633-47ae-80c1-5d00111ef646}",
        "hidden": false,
        "name": "Git Bash",
        "commandline": "C:\\Program Files\\Git\\bin\\bash.exe -login -i",
        "startingDirectory": "%USERPROFILE%",
        "icon": "C:\\Program Files\\Git\\mingw64\\share\\git\\git-for-windows.ico"
      },
      {
        "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
        "hidden": false,
        "name": "PowerShell",
        "commandline": "powershell.exe",
        "colorScheme": "Campbell Powershell"
      },
      {
        "guid": "{fc912aec-fe4e-4667-b7cd-9f4fd2c162de}",
        "hidden": false,
        "name": "PowerShell Admin",
        "commandline": "powershell.exe Start-Process -Verb RunAs cmd.exe '/c start wt.exe'",
        "colorScheme": "Campbell Powershell"
      },
      {
        "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
        "hidden": true,
        "name": "Azure",
        "source": "Windows.Terminal.Azure"
      }
    ]
  },
  "schemes": [
    {
      "name": "Dracula",
      "background": "#272935",
      "black": "#21222C",
      "blue": "#BD93F9",
      "cyan": "#8BE9FD",
      "foreground": "#F8F8F2",
      "green": "#50FA7B",
      "purple": "#FF79C6",
      "red": "#FF5555",
      "white": "#F8F8F2",
      "yellow": "#FFB86C",
      "brightBlack": "#6272A4",
      "brightBlue": "#D6ACFF",
      "brightCyan": "#A4FFFF",
      "brightGreen": "#69FF94",
      "brightPurple": "#FF92DF",
      "brightRed": "#FF6E6E",
      "brightWhite": "#F8F8F2",
      "brightYellow": "#FFFFA5"
    },
    {
      "name": "Builtin Pastel Dark",
      "black": "#4f4f4f",
      "red": "#ff6c60",
      "green": "#a8ff60",
      "yellow": "#ffffb6",
      "blue": "#96cbfe",
      "purple": "#ff73fd",
      "cyan": "#c6c5fe",
      "white": "#eeeeee",
      "brightBlack": "#7c7c7c",
      "brightRed": "#ffb6b0",
      "brightGreen": "#ceffac",
      "brightYellow": "#ffffcc",
      "brightBlue": "#b5dcff",
      "brightPurple": "#ff9cfe",
      "brightCyan": "#dfdffe",
      "brightWhite": "#ffffff",
      "background": "#000000",
      "foreground": "#bbbbbb"
    },
    {
      "name": "Campbell Powershell",
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
      "purple": "#881798",
      "red": "#C50F1F",
      "selectionBackground": "#FFFFFF",
      "white": "#CCCCCC",
      "yellow": "#C19C00"
    },
    {
      "name": "Andromeda",
      "black": "#000000",
      "red": "#cd3131",
      "green": "#05bc79",
      "yellow": "#e5e512",
      "blue": "#2472c8",
      "purple": "#bc3fbc",
      "cyan": "#0fa8cd",
      "white": "#e5e5e5",
      "brightBlack": "#666666",
      "brightRed": "#cd3131",
      "brightGreen": "#05bc79",
      "brightYellow": "#e5e512",
      "brightBlue": "#2472c8",
      "brightPurple": "#bc3fbc",
      "brightCyan": "#0fa8cd",
      "brightWhite": "#e5e5e5",
      "background": "#262a33",
      "foreground": "#e5e5e5"
    },
    {
      "name": "Argonaut",
      "black": "#232323",
      "red": "#ff000f",
      "green": "#8ce10b",
      "yellow": "#ffb900",
      "blue": "#008df8",
      "purple": "#6d43a6",
      "cyan": "#00d8eb",
      "white": "#ffffff",
      "brightBlack": "#444444",
      "brightRed": "#ff2740",
      "brightGreen": "#abe15b",
      "brightYellow": "#ffd242",
      "brightBlue": "#0092ff",
      "brightPurple": "#9a5feb",
      "brightCyan": "#67fff0",
      "brightWhite": "#ffffff",
      "background": "#0e1019",
      "foreground": "#fffaf4"
    },
    {
      "name": "BlulocoDark",
      "black": "#4a505d",
      "red": "#f81141",
      "green": "#23974a",
      "yellow": "#fd7e57",
      "blue": "#285bff",
      "purple": "#8c62fd",
      "cyan": "#366f9a",
      "white": "#ccd5e5",
      "brightBlack": "#61697a",
      "brightRed": "#fc4a6d",
      "brightGreen": "#37bd58",
      "brightYellow": "#f6be48",
      "brightBlue": "#199ffd",
      "brightPurple": "#fc58f6",
      "brightCyan": "#50acae",
      "brightWhite": "#ffffff",
      "background": "#1e2127",
      "foreground": "#abb2bf"
    },
    {
      "name": "Breeze",
      "black": "#31363b",
      "red": "#ed1515",
      "green": "#11d116",
      "yellow": "#f67400",
      "blue": "#1d99f3",
      "purple": "#9b59b6",
      "cyan": "#1abc9c",
      "white": "#eff0f1",
      "brightBlack": "#7f8c8d",
      "brightRed": "#c0392b",
      "brightGreen": "#1cdc9a",
      "brightYellow": "#fdbc4b",
      "brightBlue": "#3daee9",
      "brightPurple": "#8e44ad",
      "brightCyan": "#16a085",
      "brightWhite": "#fcfcfc",
      "background": "#31363b",
      "foreground": "#eff0f1"
    },
    {
      "name": "Bright Lights",
      "black": "#191919",
      "red": "#ff355b",
      "green": "#b7e876",
      "yellow": "#ffc251",
      "blue": "#76d4ff",
      "purple": "#ba76e7",
      "cyan": "#6cbfb5",
      "white": "#c2c8d7",
      "brightBlack": "#191919",
      "brightRed": "#ff355b",
      "brightGreen": "#b7e876",
      "brightYellow": "#ffc251",
      "brightBlue": "#76d5ff",
      "brightPurple": "#ba76e7",
      "brightCyan": "#6cbfb5",
      "brightWhite": "#c2c8d7",
      "background": "#191919",
      "foreground": "#b3c9d7"
    },
    {
      "name": "Dark+",
      "black": "#000000",
      "red": "#cd3131",
      "green": "#0dbc79",
      "yellow": "#e5e510",
      "blue": "#2472c8",
      "purple": "#bc3fbc",
      "cyan": "#11a8cd",
      "white": "#e5e5e5",
      "brightBlack": "#666666",
      "brightRed": "#f14c4c",
      "brightGreen": "#23d18b",
      "brightYellow": "#f5f543",
      "brightBlue": "#3b8eea",
      "brightPurple": "#d670d6",
      "brightCyan": "#29b8db",
      "brightWhite": "#e5e5e5",
      "background": "#0e0e0e",
      "foreground": "#cccccc"
    },
    {
      "name": "Monokai Vivid",
      "black": "#121212",
      "red": "#fa2934",
      "green": "#98e123",
      "yellow": "#fff30a",
      "blue": "#0443ff",
      "purple": "#f800f8",
      "cyan": "#01b6ed",
      "white": "#ffffff",
      "brightBlack": "#838383",
      "brightRed": "#f6669d",
      "brightGreen": "#b1e05f",
      "brightYellow": "#fff26d",
      "brightBlue": "#0443ff",
      "brightPurple": "#f200f6",
      "brightCyan": "#51ceff",
      "brightWhite": "#ffffff",
      "background": "#121212",
      "foreground": "#f9f9f9"
    },
    {
      "name": "Nocturnal Winter",
      "black": "#4d4d4d",
      "red": "#f12d52",
      "green": "#09cd7e",
      "yellow": "#f5f17a",
      "blue": "#3182e0",
      "purple": "#ff2b6d",
      "cyan": "#09c87a",
      "white": "#fcfcfc",
      "brightBlack": "#808080",
      "brightRed": "#f16d86",
      "brightGreen": "#0ae78d",
      "brightYellow": "#fffc67",
      "brightBlue": "#6096ff",
      "brightPurple": "#ff78a2",
      "brightCyan": "#0ae78d",
      "brightWhite": "#ffffff",
      "background": "#0d0d17",
      "foreground": "#e6e5e5"
    },
    {
      "name": "OneStar",
      "black": "#000000",
      "red": "#d13b3b",
      "green": "#0dbc79",
      "yellow": "#dfdf44",
      "blue": "#2472c8",
      "purple": "#c42cc4",
      "cyan": "#33a0bb",
      "white": "#f1f1f1",
      "brightBlack": "#666666",
      "brightRed": "#fa4b4b",
      "brightGreen": "#23d18b",
      "brightYellow": "#fcfc5c",
      "brightBlue": "#3b8eea",
      "brightPurple": "#d861d8",
      "brightCyan": "#29b8db",
      "brightWhite": "#fafafa",
      "background": "#0e0e0e",
      "foreground": "#e4e4e4"
    },
    {
      "name": "synthwave-everything",
      "black": "#fefefe",
      "red": "#f97e72",
      "green": "#72f1b8",
      "yellow": "#fede5d",
      "blue": "#6d77b3",
      "purple": "#c792ea",
      "cyan": "#f772e0",
      "white": "#fefefe",
      "brightBlack": "#fefefe",
      "brightRed": "#f88414",
      "brightGreen": "#72f1b8",
      "brightYellow": "#fff951",
      "brightBlue": "#36f9f6",
      "brightPurple": "#e1acff",
      "brightCyan": "#f92aad",
      "brightWhite": "#fefefe",
      "background": "#2a2139",
      "foreground": "#f0eff1"
    },
    {
      "name": "Ubuntu",
      "black": "#2e3436",
      "red": "#cc0000",
      "green": "#4e9a06",
      "yellow": "#c4a000",
      "blue": "#3465a4",
      "purple": "#75507b",
      "cyan": "#06989a",
      "white": "#d3d7cf",
      "brightBlack": "#555753",
      "brightRed": "#ef2929",
      "brightGreen": "#8ae234",
      "brightYellow": "#fce94f",
      "brightBlue": "#729fcf",
      "brightPurple": "#ad7fa8",
      "brightCyan": "#34e2e2",
      "brightWhite": "#eeeeec",
      "background": "#300a24",
      "foreground": "#eeeeec"
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
      "command": {
        "action": "splitPane",
        "split": "auto",
        "splitMode": "duplicate"
      },
      "keys": "ctrl+shift+a"
    },
    {
      "command": "find",
      "keys": "ctrl+shift+f"
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
    },
    {
      "command": {
        "action": "newTab",
        "index": 5
      },
      "keys": "ctrl+0"
    },
    {
      "command": {
        "action": "closeTab"
      },
      "keys": "ctrl+q"
    }
  ]
}
```
