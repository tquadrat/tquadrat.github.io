# Windows Batch Files (\*.bat and \*.cmd)

## Path Handling in Windows Batch Files

In a Windows batch file, %0, %1,…, %9 are the first, second, …, tenth parameter of the command line. The first parameter is the command itself. Suppose the batch file is `test.bat` that has the following command:

```
@echo %0
```

Then the command line `test.bat` will output "`test.bat`". The command line `.\test.bat` will output "`.\test.bat`". The command line `“test.bat”` will output "`“test.bat”`". The command line `”.\test.bat”` will output "`“.\test.bat”`", and so on.

The tilde "`~`" before the digit will do something extra to the parameter: `%~0` will remove the quote marks of the first parameter if it has any. So, `“test.bat”` will output "`test.bat`", and  `“.\test.bat”` will output "`.\test.bat`".

"`~f`" will expand the parameter to the full path name. So `%~f0` may expand to "`C:\dir\test.bat`".

"`~d`" will extract the disk part of the parameter. So `test.bat` may output "`C:`".

"`~p`" will extract the path part of the parameter. So `test.bat` may output "`\dir\`".

"`~dp`" will extract both the disk part and the path part of the parameter. So `%~dp0` may expand to "`C:\dir\`". Note that even when the command in the command line does not include drive or path, `%~dp0` still expands to the drive and path, i.e., the command is first expanded to the full path name then the drive and path are extracted. Things get weird for `%~dp1`, `%~dp2`, …, if you provide a non-existing file. If the non-existing file is of the form of an absolute path, the result is the drive and path part of the file. If the non-existing file has a relative path, the relative path would be prefixed the drive/path of the script.

References:
- [Orignal Article](https://myprogrammingnotes.com/0-0-f0-dp0-bat-file.html)
- https://stackoverflow.com/questions/112055/what-does-d0-mean-in-a-windows-batch-file
- https://stackoverflow.com/questions/5034076/what-does-dp0-mean-and-how-does-it-work
