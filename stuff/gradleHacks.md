# Gradle Hacks

Some solutions for problems I had with Gradle. They work for me …

## JavaDoc

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

