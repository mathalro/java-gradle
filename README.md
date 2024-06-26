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

**Running a Task**

```
gradle hello
```

## Tasks

Gradle tasks are code that Gradle executes. The language used to write Gradle tasks is [Groovy](https://groovy-lang.org/). A task will have a lifecycle, properties, actions and dependencies. 


**Example**

```groovy
task MyTask {
    description "This is an example of task"
    doLast {
        println "Executing Last in MyTask"
    }
    doFirst {
        println "Executing First in MyTask"
    }
}
```

To see all tasks we can use

```bash
$ gradle tasks --all
```

**Phases**

* Initialization Phase - Used to configure multi project builds
* Configuration phase - Executed code in the task that not the action
* Execution phase - Execute the task action

**Dependencies**

We can make a task depending on another task. 

```groovy
task DependencyTask {
    description "Dependency task"
    doLast {
        println "Dependency task"
    }
}

task MyTask {
    description "This is an example of main task"
    doLast {
        println "Main task"
    }
}

MyTask.dependsOn(DependencyTask)
```

**Properties**

We can define specific properties to gradle build file, and use them as variables.

```groovy
ext.projectName = "Testing Gradle"
def projectVersion = "2.0"

task MyTask {
    description "Project $projectName"
    doLast {
        println "This is an example of task with a property: version $projectVersion"
    }
}
```

## Dependencies

It's possible to specify how we want the dependencies to behave

* mustRunAfter - If two tasks execute, one must run after the other
* shouldRunAfter - If two taks execvute, one should run after the other. It will ignore circular dependencies.
* finalizedBy - Inverted dependency. When a task run, it triggers the tasks that specify finalize by it.

## Typed Tasks

For complex and reusable tasks like: copying files, zipping files, etc. 

```groovy
task copyImages (type: Copy) {
    from 'img/src/'
    into 'img/dest/'
}
```

**Copy Task**

```groovy
def contentSpec = copySpec {
    exclude { it.file.name.startsWith('invalid') }
    from 'img/src'
}

task copyImages (type: Copy) {
    with contentSpec
    into 'img/dest/'
}
```

**Replace content**

```
task copyConfig (type: Copy) {
    include 'web.txt'
    from 'files/src'
    into 'files/dest'
    expand (
        [placeholder: 'Replaced the placeholder']
    )
}
```