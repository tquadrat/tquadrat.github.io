# Updating the Gradle Wrapper

In most cases, a project is built using the [Gradle Wrapper](https://docs.gradle.org/current/userguide/gradle_wrapper.html). And of course, at some point the version of the wrapper needs to be updated when the Gradle version is updated.

Use the `wrapper` Gradle task to upgrade Gradle Wrapper. It not only updates the Gradle version in the `gradle-wrapper.properties` file, but it also updates the Wrapper shell script (`gradlew`) and the Gradle Wrapper jar (`gradle-wrapper.jar`).

You can run the wrapper task from the terminal, specifying the latest version
```console
./gradlew wrapper --gradle-version latest
```
or the specific version you want:
```console
./gradlew wrapper --gradle-version 8.1.1
```
