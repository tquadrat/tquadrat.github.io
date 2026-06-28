# Windows Start Script Generation

Gradle creates start scripts for a Java application and adds them to the distribution(s). At default, this will be a UNIX/Linux shell script and a Windows batch file (`*.bat`).

When your project has a certain amount of dependencies, the generated Windows batch file may contain lines likes these:

```bat
set CLASSPATH=%APP_HOME%\\lib\\hadoop-common-3.5.0.jar;%APP_HOME%\\lib\\hadoop-mapreduce-client-core-3.5.0.jar;%APP_HOME%\\lib\\hadoop-yarn-client-3.5.0.jar;%APP_HOME%\\lib\\hadoop-yarn-common-3.5.0.jar;%APP_HOME%\\lib\\parquet-hadoop-1.17.1.jar;%APP_HOME%\\lib\\jersey-hk2-2.46.jar;%APP_HOME%\\lib\\hadoop-auth-3.5.0.jar;%APP_HOME%\\lib\\hadoop-hdfs-client-3.5.0.jar;%APP_HOME%\\lib\\parquet-column-1.17.1.jar;%APP_HOME%\\lib\\parquet-encoding-1.17.1.jar;%APP_HOME%\\lib\\parquet-common-1.17.1.jar;%APP_HOME%\\lib\\slf4j-reload4j-1.7.36.jar;%APP_HOME%\\lib\\metrics-core-3.2.4.jar;%APP_HOME%\\lib\\kerb-util-2.0.3.jar;%APP_HOME%\\lib\\kerb-crypto-2.0.3.jar;%APP_HOME%\\lib\\kerb-core-2.0.3.jar;%APP_HOME%\\lib\\kerby-pkix-2.0.3.jar;%APP_HOME%\\lib\\kerby-config-2.0.3.jar;%APP_HOME%\\lib\\listenablefuture-9999.0-empty-to-avoid-conflict-with-guava.jar;%APP_HOME%\\lib\\hadoop-yarn-api-3.5.0.jar;%APP_HOME%\\lib\\hadoop-shaded-protobuf_3_25-1.5.0.jar;%APP_HOME%\\lib\\hadoop-annotations-3.5.0.jar;%APP_HOME%\\lib\\hadoop-shaded-guava-1.5.0.jar;%APP_HOME%\\lib\\commons-math3-3.6.1.jar;%APP_HOME%\\lib\\jakarta.servlet.jsp-api-2.3.6.jar;%APP_HOME%\\lib\\jersey-container-servlet-2.46.jar;%APP_HOME%\\lib\\jersey-container-servlet-core-2.46.jar;%APP_HOME%\\lib\\jersey-server-2.46.jar;%APP_HOME%\\lib\\jersey-client-2.46.jar;%APP_HOME%\\lib\\jersey-common-2.46.jar;%APP_HOME%\\lib\\reload4j-1.2.22.jar;%APP_HOME%\\lib\\re2j-1.1.jar;%APP_HOME%\\lib\\jsch-0.1.55.jar;%APP_HOME%\\lib\\curator-recipes-5.2.0.jar;%APP_HOME%\\lib\\curator-framework-5.2.0.jar;%APP_HOME%\\lib\\curator-client-5.2.0.jar;%APP_HOME%\\lib\\jsr305-3.0.2.jar;%APP_HOME%\\lib\\zookeeper-3.8.6.jar;%APP_HOME%\\lib\\snappy-java-1.1.10.7.jar;%APP_HOME%\\lib\\parquet-format-structures-1.17.1.jar;%APP_HOME%\\lib\\parquet-jackson-1.17.1.jar;%APP_HOME%\\lib\\aircompressor-2.0.2.jar;%APP_HOME%\\lib\\commons-pool-1.6.jar;%APP_HOME%\\lib\\hk2-locator-2.6.1.jar;%APP_HOME%\\lib\\hk2-api-2.6.1.jar;%APP_HOME%\\lib\\hk2-utils-2.6.1.jar;%APP_HOME%\\lib\\jakarta.inject-2.6.1.jar;%APP_HOME%\\lib\\javax.servlet-api-3.1.0.jar;%APP_HOME%\\lib\\zookeeper-jute-3.8.6.jar;%APP_HOME%\\lib\\audience-annotations-0.12.0.jar;%APP_HOME%\\lib\\jline-3.9.0.jar;%APP_HOME%\\lib\\jettison-1.5.4.jar;%APP_HOME%\\lib\\osgi-resource-locator-1.0.3.jar;%APP_HOME%\\lib\\aopalliance-repackaged-2.6.1.jar;%APP_HOME%\\lib\\kerby-asn1-2.0.3.jar;%APP_HOME%\\lib\\kerby-util-2.0.3.jar;%APP_HOME%\\lib\\javax.inject-1.jar;%APP_HOME%\\lib\\aopalliance-1.0.jar;%APP_HOME%\\lib\\jaxb-api-2.2.12.jar

set MODULE_PATH=%APP_HOME%\\lib\\org.guardian.ast.Extractor-1.0-SNAPSHOT.jar;%APP_HOME%\\lib\\org.tquadrat.foundation.config-0.25.11.jar;%APP_HOME%\\lib\\org.tquadrat.foundation.jsonbuilder-0.25.11.jar;%APP_HOME%\\lib\\org.tquadrat.foundation.xml-0.25.11.jar;%APP_HOME%\\lib\\org.guardian.ast.ParquetSupport-1.0-SNAPSHOT.jar;%APP_HOME%\\lib\\org.tquadrat.foundation.i18n-0.25.11.jar;%APP_HOME%\\lib\\org.tquadrat.foundation.inifile-0.25.11.jar;%APP_HOME%\\lib\\org.tquadrat.foundation.util-0.25.11.jar;%APP_HOME%\\lib\\log4j-layout-template-json-2.26.0.jar;%APP_HOME%\\lib\\log4j-slf4j2-impl-2.26.0.jar;%APP_HOME%\\lib\\log4j-core-2.26.0.jar;%APP_HOME%\\lib\\javaparser-symbol-solver-core-3.28.0.jar;%APP_HOME%\\lib\\javaparser-core-serialization-3.28.0.jar;%APP_HOME%\\lib\\parsson-1.1.7.jar;%APP_HOME%\\lib\\woodstox-core-5.4.0.jar;%APP_HOME%\\lib\\stax2-api-4.2.1.jar;%APP_HOME%\\lib\\commons-configuration2-2.10.1.jar;%APP_HOME%\\lib\\avro-1.11.5.jar;%APP_HOME%\\lib\\commons-compress-1.26.2.jar;%APP_HOME%\\lib\\zstd-jni-1.5.7-3.jar;%APP_HOME%\\lib\\org.eclipse.jgit-7.6.0.202603022253-r.jar;%APP_HOME%\\lib\\org.tquadrat.foundation.base-0.25.11.jar;%APP_HOME%\\lib\\log4j-api-2.26.0.jar;%APP_HOME%\\lib\\javaparser-core-3.28.0.jar;%APP_HOME%\\lib\\javassist-3.30.2-GA.jar;%APP_HOME%\\lib\\guice-servlet-5.1.0.jar;%APP_HOME%\\lib\\guice-5.1.0.jar;%APP_HOME%\\lib\\guava-33.5.0-jre.jar;%APP_HOME%\\lib\\checker-qual-3.53.0.jar;%APP_HOME%\\lib\\junit-platform-engine-1.14.2.jar;%APP_HOME%\\lib\\junit-jupiter-api-5.14.2.jar;%APP_HOME%\\lib\\junit-platform-commons-1.14.2.jar;%APP_HOME%\\lib\\junit-jupiter-engine-5.14.2.jar;%APP_HOME%\\lib\\jakarta.json-api-2.1.3.jar;%APP_HOME%\\lib\\commons-text-1.14.0.jar;%APP_HOME%\\lib\\commons-lang3-3.18.0.jar;%APP_HOME%\\lib\\httpclient-4.5.13.jar;%APP_HOME%\\lib\\commons-logging-1.3.0.jar;%APP_HOME%\\lib\\commons-codec-1.21.0.jar;%APP_HOME%\\lib\\commons-io-2.16.1.jar;%APP_HOME%\\lib\\JavaEWAH-1.2.3.jar;%APP_HOME%\\lib\\dnsjava-3.6.1.jar;%APP_HOME%\\lib\\slf4j-api-2.0.17.jar;%APP_HOME%\\lib\\apiguardian-api-1.1.2.jar;%APP_HOME%\\lib\\failureaccess-1.0.3.jar;%APP_HOME%\\lib\\jspecify-1.0.0.jar;%APP_HOME%\\lib\\error_prone_annotations-2.41.0.jar;%APP_HOME%\\lib\\j2objc-annotations-3.1.jar;%APP_HOME%\\lib\\commons-cli-1.9.0.jar;%APP_HOME%\\lib\\commons-net-3.9.0.jar;%APP_HOME%\\lib\\commons-collections4-4.4.jar;%APP_HOME%\\lib\\jakarta.ws.rs-api-2.1.6.jar;%APP_HOME%\\lib\\jaxb-runtime-2.3.9.jar;%APP_HOME%\\lib\\jakarta.xml.bind-api-2.3.3.jar;%APP_HOME%\\lib\\jackson-jaxrs-json-provider-2.18.6.jar;%APP_HOME%\\lib\\jackson-jaxrs-base-2.18.6.jar;%APP_HOME%\\lib\\jackson-databind-2.18.6.jar;%APP_HOME%\\lib\\jackson-core-2.18.6.jar;%APP_HOME%\\lib\\jackson-annotations-2.18.6.jar;%APP_HOME%\\lib\\jackson-module-jaxb-annotations-2.18.6.jar;%APP_HOME%\\lib\\jakarta.activation-api-1.2.2.jar;%APP_HOME%\\lib\\jetty-webapp-9.4.58.v20250814.jar;%APP_HOME%\\lib\\jetty-servlet-9.4.58.v20250814.jar;%APP_HOME%\\lib\\jetty-security-9.4.58.v20250814.jar;%APP_HOME%\\lib\\jetty-server-9.4.58.v20250814.jar;%APP_HOME%\\lib\\websocket-client-9.4.58.v20250814.jar;%APP_HOME%\\lib\\jetty-client-9.4.58.v20250814.jar;%APP_HOME%\\lib\\jetty-http-9.4.58.v20250814.jar;%APP_HOME%\\lib\\websocket-common-9.4.58.v20250814.jar;%APP_HOME%\\lib\\jetty-io-9.4.58.v20250814.jar;%APP_HOME%\\lib\\jetty-util-ajax-9.4.58.v20250814.jar;%APP_HOME%\\lib\\jetty-xml-9.4.58.v20250814.jar;%APP_HOME%\\lib\\jetty-util-9.4.58.v20250814.jar;%APP_HOME%\\lib\\gson-2.9.0.jar;%APP_HOME%\\lib\\netty-all-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-resolver-dns-native-macos-4.1.130.Final-osx-x86_64.jar;%APP_HOME%\\lib\\netty-resolver-dns-native-macos-4.1.130.Final-osx-aarch_64.jar;%APP_HOME%\\lib\\netty-resolver-dns-classes-macos-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-resolver-dns-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-handler-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-transport-native-epoll-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-transport-native-epoll-4.1.130.Final-linux-x86_64.jar;%APP_HOME%\\lib\\netty-transport-native-epoll-4.1.130.Final-linux-aarch_64.jar;%APP_HOME%\\lib\\netty-transport-native-epoll-4.1.130.Final-linux-riscv64.jar;%APP_HOME%\\lib\\bcprov-jdk18on-1.82.jar;%APP_HOME%\\lib\\jts-core-1.20.0.jar;%APP_HOME%\\lib\\opentest4j-1.3.0.jar;%APP_HOME%\\lib\\httpcore-4.4.13.jar;%APP_HOME%\\lib\\jakarta.annotation-api-1.3.5.jar;%APP_HOME%\\lib\\jakarta.validation-api-2.0.2.jar;%APP_HOME%\\lib\\nimbus-jose-jwt-10.4.jar;%APP_HOME%\\lib\\netty-transport-classes-epoll-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-transport-native-kqueue-4.1.130.Final-osx-x86_64.jar;%APP_HOME%\\lib\\netty-transport-native-kqueue-4.1.130.Final-osx-aarch_64.jar;%APP_HOME%\\lib\\netty-transport-classes-kqueue-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-transport-native-unix-common-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-codec-dns-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-codec-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-transport-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-resolver-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-buffer-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-common-4.1.130.Final.jar;%APP_HOME%\\lib\\txw2-2.3.9.jar;%APP_HOME%\\lib\\istack-commons-runtime-3.0.12.jar;%APP_HOME%\\lib\\jakarta.activation-1.2.2.jar;%APP_HOME%\\lib\\jakarta.servlet-api-4.0.4.jar;%APP_HOME%\\lib\\failsafe-2.4.4.jar;%APP_HOME%\\lib\\netty-codec-haproxy-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-codec-http-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-codec-http2-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-codec-memcache-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-codec-mqtt-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-codec-redis-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-codec-smtp-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-codec-socks-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-codec-stomp-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-handler-proxy-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-transport-rxtx-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-transport-sctp-4.1.130.Final.jar;%APP_HOME%\\lib\\netty-transport-udt-4.1.130.Final.jar;%APP_HOME%\\lib\\javax.annotation-api-1.3.2.jar;%APP_HOME%\\lib\\websocket-api-9.4.58.v20250814.jar
```

When `%APP_HOME%` expands to an absolute path name, the second line may have far more than 7000 characters; together with the about 3000 characters from the first line, this would result in a length for the startup command line for the application of far above 8191 characters – this is the hard limit for a command line in Windows.

```bat
@rem which allows us to clear the local environment before executing the java command
endlocal & "%JAVA_EXE%" %DEFAULT_JVM_OPTS% %JAVA_OPTS% %ORG_GUARDIAN_AST_EXTRACTOR_OPTS%  -classpath "%CLASSPATH%" --module-path "%APP_HOME%lib*" --module org.guardian.ast/org.guardian.ast.Extractor %* & call :exitWithErrorLevel
```

The developers of Java (and those for several other tools) are aware of this problem and introduced a feature to circumvent this limitation. For `java`, `javac` and `javadoc`, this looks like this:

```bat
java @options
javac @options
javadoc @options
```

where `options` is the (relative or fully-qualified) name of a file that contains the command line arguments for the respective command. 

This can be mixed with directly provided arguments, and even more than one file is possible. See [`java` Command-Line Argument Files](https://docs.oracle.com/en/java/javase/25/docs/specs/man/java.html#java-command-line-argument-files) for the details.

You can tweak Gradle to build a Windows Start Script that uses Command-Line Argument Files like this:

```groovy
tasks.named('startScripts') {
        /*
         * We overwrite the default generator for the Windows start script.
         * The generated start script will create a parameter file with the
         * MODULE_PATH and the CLASSPATH settings and use that, to circumvent
         * the line length limitations for Windows batch files.
         */
    windowsStartScriptGenerator = new ScriptGenerator() {
        @Override
        void generateScript( final JavaAppStartScriptGenerationDetails details, final Writer destination ) {

            var defaultJVMOpts = details.getDefaultJvmOpts().stream().collect( Collectors.joining( " " ) )
            var mainClassName = details.getApplicationName()
            var moduleEntryPoint = application.mainModule.get() + "/" + application.mainClass.get()

            var classpath = new StringJoiner( "\n", "set /P =\"-classpath \" > %OPTIONS_FILE% < nul\n", "\necho. >> %OPTIONS_FILE%\n" )
            for( final var s : details.classpath )
            {
                classpath.add( "set /P =\"%APP_HOME%/" + s + ";\" >> %OPTIONS_FILE% < nul" )
            }

            var modulepath = new StringJoiner( "\n", "set /P =\"--module-path \" >> %OPTIONS_FILE% < nul\n", "\necho. >> %OPTIONS_FILE%\n" )
            for( final var s : details.modulePath )
            {
                modulepath.add( "set /P =\"%APP_HOME%/" + s + ";\" >> %OPTIONS_FILE% < nul" )
            }

            destination << """\
@if "%DEBUG%"=="" @echo off
@rem Set local scope for the variables, and ensure extensions are enabled
setlocal EnableExtensions

@rem ##########################################################################
@rem
@rem  $mainClassName startup script for Windows
@rem
@rem ##########################################################################

set DIRNAME=%~dp0
if "%DIRNAME%"=="" set DIRNAME=.
@rem This is normally unused
set APP_BASE_NAME=%~n0
set APP_HOME=%DIRNAME%..
set OPTIONS_FILE=%DIRNAME%/options

@rem Resolve any "." and ".." in APP_HOME to make it shorter.
for %%i in ("%APP_HOME%") do set APP_HOME=%%~fi

@rem Add default JVM options here. You can also use JAVA_OPTS to pass JVM options to this script.
set DEFAULT_JVM_OPTS=$defaultJVMOpts

@rem Find java.exe
if defined JAVA_HOME goto findJavaFromJavaHome

set JAVA_EXE=java.exe
%JAVA_EXE% -version >NUL 2>&1
if %ERRORLEVEL% equ 0 goto execute

echo. 1>&2
echo ERROR: JAVA_HOME is not set and no 'java' command could be found in your PATH. 1>&2
echo. 1>&2
echo Please set the JAVA_HOME variable in your environment to match the 1>&2
echo location of your Java installation. 1>&2

"%COMSPEC%" /c exit 1

:findJavaFromJavaHome
set JAVA_HOME=%JAVA_HOME:"=%
set JAVA_EXE=%JAVA_HOME%/bin/java.exe

if exist "%JAVA_EXE%" goto execute

echo. 1>&2
echo ERROR: JAVA_HOME is set to an invalid directory: %JAVA_HOME% 1>&2
echo. 1>&2
echo Please set the JAVA_HOME variable in your environment to match the 1>&2
echo location of your Java installation. 1>&2

"%COMSPEC%" /c exit 1

:execute
@rem Setup the command line

$classpath

$modulepath

@rem Execute $mainClassName
@rem endlocal doesn't take effect until after the line is parsed and variables are expanded
@rem which allows us to clear the local environment before executing the java command
endlocal & "%JAVA_EXE%" %DEFAULT_JVM_OPTS% %JAVA_OPTS% "@%OPTIONS_FILE%" --module $moduleEntryPoint %* & call :exitWithErrorLevel

:exitWithErrorLevel
@rem Use "%COMSPEC%" /c exit to allow operators to work properly in scripts
"%COMSPEC%" /c exit %ERRORLEVEL%
"""
        }
    }
}
```

More details on how to create your own start scripts can be found [here](https://docs.gradle.org/current/dsl/org.gradle.jvm.application.tasks.CreateStartScripts.html).
