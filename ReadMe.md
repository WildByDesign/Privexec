# LPAC Sandbox Launcher
## Less Privileged AppContainer Sandbox Launcher


## Screenshot:
![](https://raw.githubusercontent.com/WildByDesign/Privexec/master/LPAC%20Launcher.png)


## Details:

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
