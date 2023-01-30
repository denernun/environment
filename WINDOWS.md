### disable windows defender
```text
gpedit.msc
  user configuration
    administrative templates
      windows components
        microsoft defender antivirus
          turn off microsoft defender antivirus
            enabled
          allow antimalware service to remain running always
            disabled
          real time protection
            turn off real-time protection
              enabled
task scheduler
  task scheduler library
    microsoft
      windows
        windows defender
          windows defender cache maintenance
            disable
          windows defender cleanup
            disable
          windows defender scheduled scan
            disable
          windows defender verification
            disable
gpupdate/force
```
### disable program compatibility assistant
```text
gpedit.msc
  user configuration
    administrative templates
      windows components
        application compatibility
          turn off program compatibility assistant
            enabled
gpupdate/force            
```
