# Gradle

Build automation tool for multi-language software development. It controls the development process in the tasks of compilation and packaging to testing, deployment and publishing. Supports Java, C/C++ and JavaScript.

Grade has a declarative language, which express intent, being a very maintanable approach.

## Comparing Gradle to Ant and Maven

* Ant provides XML Build Script, which specify everything that we need. 
* Maven has more conventions than Ant and it is extensible. Also written in XML and harder to maintain.

## Installing Gradle

* https://gradle.org

## Gradle Builds

* Gradle has a build file, typically build.gradle
* The file contains taks, plugins and dependencies. 

**Task Example**

```groovy
task hello {
    doLast {
        println "Hello, Gradle"
    }
}
```

**Running Task**

```
gradle hello
```