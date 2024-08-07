# JShell Startup Configuration

The Java `jshell` tool is useful for rapid prototyping simple Java code, or for testing some functionality.

On Linux, I configured the Terminal application to have a special `JShell` terminal, like shown in the screenshot below. It is from the Ubuntu terminal application, and – as you may have noticed already – in German:

![Terminal Configuration](TerminalConfiguration.png)

`JShell` starts with this command:

```bash
jshell --enable-preview --startup ~/.local/jshell.startup
```

The file `~/.local/jshell.startup` looks like this:

```Java
import static java.lang.Math.*;
import static java.lang.System.*;
import static java.nio.file.Files.*;
import static java.time.temporal.ChronoUnit.*;
import static java.util.Objects.*;
import static java.util.regex.Pattern.*;

import java.io.*;
import java.math.*;
import java.time.*;
import java.util.*;
import java.util.regex.*;

void println() { out.println(); }
void println( final Object v ) { out.println( v ); }
void printf( final String format, final Object... args ) { out.printf( format, args ); }

printf( "%nWelcome, %s, to JShell!%n%n", getProperty( "user.name" ) );
println( "Preview should be enabled!" );
{
var startupFile = new File( "/home/tquadrat/.local/jshell.startup" ).getCanonicalFile().getAbsoluteFile();
printf( "The startup options were loaded from '%s'.%n%n-----%n", startupFile.getAbsolutePath() );
lines( startupFile.toPath() ).filter( line -> line.startsWith( "import" ) ).forEach( out::println );
}
println( "-----\n" );
```
Basically, it can contain any arbitrary Java code that will be executed when JShell comes up.
