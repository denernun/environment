### fonts
```text
Caskaydia Cove Nerd Font
https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/CascadiaCode.zip?WT.mc_id=-blog-scottha
```
### install 
```text
winget install JanDeDobbeleer.OhMyPosh -s winget
Install-Module -Name Terminal-Icons -Repository PSGallery
```
### config
```text
code $PROFILE
oh-my-posh --init --shell pwsh --config ~\ohmyposh.omp.json | Invoke-Expression
Import-Module -Name Terminal-Icons
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
          "background": "#6272a4",
          "foreground": "#ffffff",
          "leading_diamond": "\ue0b6",
          "style": "diamond",
          "template": "{{ .UserName }} "
        },
        {
          "type": "path",
          "style": "powerline",
          "powerline_symbol": "\ue0b0",
          "background": "#bd93f9",
          "foreground": "#ffffff",
          "properties": {
            "style": "folder"
          },
          "template": " {{ .Path }} "
        },
        {
          "type": "git",
          "style": "powerline",
          "powerline_symbol": "\ue0b0",
          "invert_powerline": false,
          "background": "#ffb86c",
          "foreground": "#ffffff",
          "leading_diamond": "",
          "trailing_diamond": "",
          "properties": {
            "branch_icon": "",
            "fetch_status": true,
            "fetch_stash_count": true,
            "fetch_upstream_icon": true
          },
          "template": " \u279c ({{ .UpstreamIcon }}{{ .HEAD }}{{ if gt .StashCount 0 }} \uf692 {{ .StashCount }}{{ end }}) "
        },
        {
          "type": "time",
          "style": "diamond",
          "background": "#ff79c6",
          "foreground": "#ffffff",
          "properties": {
            "time_format": "15:04"
          },
          "template": " \u2665 {{ .CurrentDate | date .Format }} ",
          "trailing_diamond": "\ue0b0"
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
        },
        {
          "type": "sysinfo",
          "style": "powerline",
          "powerline_symbol": "",
          "foreground": "#ffffff",
          "background": "#8f43f3",
          "template": "  {{ round .PhysicalPercentUsed .Precision }}% ",
          "properties": {
            "precision": 2
          }
        }
      ],
      "type": "rprompt"
    }
  ],
  "final_space": true,
  "version": 2
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
