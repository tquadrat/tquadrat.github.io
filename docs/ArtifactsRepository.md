# Artifacts Repository
You can pull the artifacts of my projects from my repository:

- [tquadrat's Archiva Repository](http://www.tquadrat.org/archiva/)

You do not need any credentials to pull something, but currently (as of 2026-05-13) no one else than me publishes to this repository.

Given that my stuff reaches some decent maturity level at some time in a distant future, I may consider to push the artifacts to Maven Central (or another public repository) then.

## Gradle

If you want to make my repository available in your Gradle build, add these lines:

```groovy
repositories {
    //---* Use MavenCentral for other dependencies *---------------------------
    mavenCentral {
        content {
            excludeGroupByRegex "org\\.tquadrat.*"
        }
    }

    //---* tquadrat's repository *---------------------------------------------
    maven {
        name "tquadratReleases"
        url "http://www.tquadrat.org/archiva/repository/releases/"
        content {
            includeGroupByRegex "org\\.tquadrat.*"
        }
        mavenContent {
            releasesOnly()
        }
        allowInsecureProtocol true
    }
    maven {
        name "tquadratSnapshots"
        url "http://www.tquadrat.org/archiva/repository/snapshots/"
        content {
            includeGroupByRegex "org\\.tquadrat.*"
        }
        mavenContent {
            snapshotsOnly()
        }
        allowInsecureProtocol true
    }
}

```

## Maven

If you are using Maven, add the following lines to your `pom.xml` to get access to the artifacts of my projects in your build:

```xml
…

<repositories>
    …
    <repository>
        <id>tquadrat.org.releases</id>
        <name>tquadrat Release Repository</name>
        <url>http://www.tquadrat.org/archiva/repository/releases/</url>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
        </snapshots>
    </repository>
    <repository>
        <id>tquadrat.org.snapshots</id>
        <name>tquadrat Snapshots Repository</name>
        <url>http://www.tquadrat.org/archiva/repository/snapshots/</url>
        <releases>
            <enabled>false</enabled>
        </releases>
        <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
        </snapshots>
    </repository>
    …
</repositories>

…
```
