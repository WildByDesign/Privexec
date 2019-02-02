# AppContainer Launcher
## AppContainer and LPAC (Less Privileged AppContainer) Launcher with Capabilities


## Screenshot:
![](https://raw.githubusercontent.com/WildByDesign/Privexec/master/AppContainer%20Launcher.png)


## Release Details:

Second release. This is a fork of Privexec aimed at narrowing down the scope to just AppContainer and LPAC with some minor GUI enhancements.

Changes since last release:

- Regular AppContainer is default (therefore 2 choices for AppContainer type now)
- LPAC (Less Privileged AppContainer can be enabled via checkbox)
- AppxManifest button to import/parse Capabilities from AppxManifest files
- Allow changing AppContainer Name field
- Unique SIDs based upon AppContainer Name
- File, Folder and Registry ACL permissions (may require Admin)
- Process Startup Directory (can be empty)
- Output box shows launched process' AppContainer SID, AppContainer Folder, Name, etc.

**Source code changes are included within the 7z archive.**


All credit goes to Force Charlie (https://github.com/fcharlie)

Original Privexec: https://github.com/M2Team/Privexec


## LPAC (Less Privileged AppContainer) Details:

## Important Capabilities for LPAC (minimum)

- lpacCom
- lpacAppExperience
- registryRead


## Event Viewer

Applications and Services Logs > Microsoft > Windows > Security-LessPrivilegedAppContainer > Operational

* some activity, but not much detail yet. Likely more detail in future Windows releases


## LPAC File System Access

LPAC is essentially Default Deny AppContainer.  You need to give it permissions via capabilities and more.

Some example "icacls" commands:

```
icacls D:\* /grant *S-1-15-2-2:(OI)(CI)(RX) /T
```

S-1-15-2-2 = ALL RESTRICTED APPLICATION PACKAGES = LPAC

(RX) gives Read & Execute access.
(M) gives Modify access.
(F) gives Full access.


## Identifying LPAC Processes

PowerShell users can utilize James Forshaw's NtObjectManager (https://www.powershellgallery.com/packages/NtObjectManager/) excellent tool to identify LPAC. The Get-NtProcessMitigations Cmdlet will differentiate between regular AppContainer and LPAC (Less Privileged AppContainer) in the output.

Process Hacker (latest Nightly builds) can identify LPAC as well. On the Token tab, go to Advanced to bring up the Token Properties and go to the Attributes tab. LPAC can be identified with the WIN://NOALLAPPPKG security attribute.

Also, James Forshaw's TokenViewer program which is part of Google's sandbox-attacksurface-analysis-tools (https://github.com/googleprojectzero/sandbox-attacksurface-analysis-tools) can also idenify LPAC via the WIN://NOALLAPPPKG security attribute and is also fantastic with regard to viewing Capabilities and such.


(more details to update later)


## LICENSE

This project use MIT License, and JSON use [https://github.com/nlohmann/json](https://github.com/nlohmann/json) , some API use NSudo, but rewrite it.
