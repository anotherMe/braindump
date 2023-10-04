
# Maven

In the context of Apache Maven, "goals" and "phases" are key concepts that help manage and automate the build and project lifecycle. Here's a short explanation of these terms:

## Goals

   **What:** Maven goals are specific tasks or actions that you want to execute during the build process. These tasks can be as simple as compiling source code or as complex as packaging and deploying a project.

   **How:** Goals are executed using the `mvn` command followed by the goal's name. For example, to compile your project, you'd run `mvn compile`, and to package it into a JAR file, you'd run `mvn package`.

## Phases

   **What:** Phases represent different stages in the Maven build lifecycle. Each phase consists of one or more goals. There are several predefined phases in Maven, such as "compile," "test," "package," "install," and "deploy."

   **How:** You don't directly execute phases; instead, you execute goals bound to specific phases. For instance, when you run `mvn compile`, it executes the goals associated with the "compile" phase.

## Lifecycle

   **What:** A lifecycle is a predefined sequence of phases that define the overall build process for a Maven project. The default Maven lifecycle includes three main phases: "clean," "default," and "site."
   
   **How:** You can trigger a lifecycle by running `mvn` followed by a lifecycle's name. For example, `mvn clean` executes the "clean" lifecycle, which cleans the project, and `mvn package` executes the "default" lifecycle, which compiles, tests, and packages the project.

## Plugins

   **What:** Maven uses plugins to execute goals and phases. Plugins provide the implementation for various build tasks. Maven itself is built around a core set of plugins, and you can use or create custom plugins for your project's specific needs.

In summary, Maven goals are individual tasks you want to perform, phases represent stages of the build process, and lifecycles define the overall sequence of phases. Plugins are the underlying tools that execute goals and contribute to the build lifecycle. Understanding these concepts is crucial for effectively managing and automating your Java or other Maven-based projects.


# Cookbook

## List the goals of a specific phase

Maven provides a command to list the goals that will be executed for a specific phase.

For example, to list the goals for the *package* phase:

  mvn help:describe -Dcmd=package

For reference, see the [Maven Help Plugin](https://maven.apache.org/plugins/maven-help-plugin/)


## Search and replace of strings using Velocity

( [Stackoverflow](https://stackoverflow.com/questions/2196394/full-search-and-replace-of-strings-in-source-files-when-copying-resources) )


## Compiling Sources Using A Different JDK
( [reference](https://maven.apache.org/plugins/maven-compiler-plugin/examples/compile-using-different-jdk.html) )

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <configuration>
        <verbose>true</verbose>
        <fork>true</fork>
        <executable>${JAVA_11_HOME}/bin/javac</executable>
        <compilerVersion>11</compilerVersion>
    </configuration>
</plugin>
```

Dove la variabile **JAVA_11_HOME** deve essere definita nel file `settings.xml` ( su Window$, lo trovi sul percorso `C:\Users\IL_TUO_UTENTE\.m2\` ):

```xml
<settings>

    ...

    <profiles>
        <profile>
            <id>compiler</id>
            <properties>
                <JAVA_11_HOME>C:\opt\jdk-11</JAVA_11_HOME>
            </properties>
        </profile>
    </profiles>
    <activeProfiles>
        <activeProfile>compiler</activeProfile>
    </activeProfiles>

</settings>
```
