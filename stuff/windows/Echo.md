# Some fun with the `echo` Command

 - ["echo" Output without Line Feed](#echo-output-without-line-feed)

* * * * *
 
## "echo" Output without Line Feed

The command `echo` will always cause a linefeed, no matter if used within a batch file or directly from the command line. The command itself does not provide a flag to avoid that.

An alternative would be the command sequence

```bat
set /P =<output> < nul
```

`<output>` is here the text that should be written.

Basically, this work, also when writing to a file:

```bat
set /P =<output> < nul >> file
```

But there are still some caveats:

  - Leading and trailing blanks are cut of from the output text if it is not wrapped into double quotes.
  - Quoting the text will only preserve trailing blanks 
  