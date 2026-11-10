## 📜Base Group policy Object

| GPO | Setting | Path |
| --- | --- | --- |
| GPO-Sales | Block Control Panel | User Config > Policies > Administrative Templates > Control Panel > Prohibit access to Control Panel and PC settings |
| | Block USB | User Config > Policies > Administrative Templates > System > Removable Storage Access > All Removable Storage classes: Deny all access |
| | Block Command Prompt | User Config > Policies > Administrative Templates > System > Prevent access to the command prompt |
| GPO-Accounting | Everything in Sales, plus: |
|  | Block registry tools | User Config > Policies > Administrative Templates > System > Prevent access to registry editing tools |
|  | Locked screensaver after 300 seconds | User Config > Policies > Administrative Templates > Control Panel > Personalization (enable the screen saver, set the timeout, and turn on password protection) |
| GPO-Executive | USB read-only | User Config > Policies > Administrative Templates > System > Removable Storage Access > All Removable Storage: Deny write access |
|  | Locked screensaver after 300 seconds | User Config > Policies > Administrative Templates > Control Panel > Personalization (enable the screen saver, set the timeout, and turn on password protection) |
| GPO-Workstation | Screen lock after 600 seconds | Computer Config > Policies > Windows Settings > Security Settings > Local Policies > Security Options > Interactive logon: Machine inactivity limit |
| | Firewall on | Computer Config > Policies > Windows Settings > Security Settings > Windows Defender Firewall with Advanced Security (set each profile to On) | 
| GPO-IT | No restrictions | |

# Force Policy Refresh & Audit GPOs

- Run gpupdate /force in CMD/PowerShell to fetch and apply the latest policies.

- Run gpresult /r to verify linked GPOs show under Applied Group Policy Objects.
