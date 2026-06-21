# Security

A Gradle build may need to access external systems (SCCS, external databases, storage systems, …) and these may require some credentials (username/password or alike).

Of course, these could be easily coded into the build script itself, but when storing the script on another location than the personal workstation, those secrets would be exposed.

One solution is to add the *Credentials* plugin (see [here](https://plugins.gradle.org/plugin/nu.studer.credentials)).

Using this plugin, you store credentials like this:
```
gradle addcredentials --key password --value ThisIsMySecretPassword!
```

Inside the Gradle script, you can access the value like this:
```
String password = credentials.forKey( 'password' )
```

The values are stored encrypted in `~/.gradle/gradle.encrypted.properties`.
