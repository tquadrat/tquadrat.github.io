# Gradle Hacks

Some solutions for problems I had with Gradle. They work for me …

* * * * *

## JavaDoc

### `doc-files` in JavaDoc

You can provide additional files for the JavaDoc documentation of your project (and only to the documentation) by creating a folder with the name `doc-files` in the respective `package` folder and copying the files there.

From the JavaDoc in your source file, your refer to these files like this: `<a href="doc-files/docFile.xyz">Link to File</a>`.

Although the `javadoc` still supports it, it does not work properly when used with Maven or Gradle.

Maven is using a special copy operation that takes care of the additional files, but for Gradle I had to create my own solution.

The first approach looked like this:

```groovy
tasks.named( 'javadoc' ) {
    mustRunAfter "jar"

    //---* Configure JavaDoc *-------------------------------------------------
    …
    doLast {
        …
    
        copy {
            from "$projectDir/src/main/java"
            into "$project.docsDir/javadoc"
            include "**/doc-files/*"
        }
    }
}
```
It worked for projects that did not define a Java 9 (Jigsaw) module. The reason is that for a module the HTML files for the documentation are kept in a folder that is named after the module.

To illustrate that, the directory trees for a project with just the class `foo.bar.Main`, first without a module, then with the module `my.module`:

| Without module | With module `my.module` |
+----------------+-------------------------+
|dd              |                         |


```groovy
tasks.named( 'javadoc' ) {
    mustRunAfter "jar"

    //---* Configure JavaDoc *-------------------------------------------------
    …
    doLast {
        …
    
        var moduleName = org.tquadrat.build.Tools.obtainModuleName( project.sourceSets.main )
        var targetDir = moduleName.map( "/%s"::formatted ).orElse( "" )
        copy {
            from "$projectDir/src/main/java"
            into "$project.docsDir/javadoc$targetDir"
            include "**/doc-files/*"
        }
    }
}
```

* * *

### Integration of a Logo into the Documentation

I want to have a logo on each page of the JavaDoc documentation for my projects, so that it looks like this:

![JavaDoc-PageHeader](JavaDoc-PageHeader.png)

To achieve this, my JavaDoc task in Gradle looks like this:

```groovy
tasks.named( 'javadoc' ) {
    String topValue = """
      <div style="overflow:auto;">
          <img src="{@docRoot}/resources/logo.jpg" 
               alt="logo"
               style="float:right;">
          <p style="font-family:sans-serif;font-size:40px;font-weight:bold;padding-left:30px;">My Library</p>      
      </div>
      """
      
    options {
        …
        addStringOption( 'top', topValue )
        …
    }

    doLast {
        copy {
            from "$projectDir/../resources/javadoc/logo.jpg"
            into "$project.docsDir/javadoc/resources"
        }
    }
}
```

The HTML code in `topValue` can be adjusted according to individual needs. Also the source location for the logo can be different.

