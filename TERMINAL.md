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
```
### config
```text
code $PROFILE

Import-Module -Name Terminal-Icons
oh-my-posh --init --shell pwsh --config ~\ohmyposh.omp.json | Invoke-Expression
Set-PSReadlineKeyHandler -Key Tab -Function MenuComplete
Set-PSReadlineKeyHandler -Key UpArrow -Function HistorySearchBackward
Set-PSReadlineKeyHandler -Key DownArrow -Function HistorySearchForward
Set-PSReadLineOption -PredictionSource History
Set-Alias g git
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

