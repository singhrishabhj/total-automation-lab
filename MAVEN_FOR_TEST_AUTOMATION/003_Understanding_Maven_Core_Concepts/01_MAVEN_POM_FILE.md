# Maven Tutorial Notes

---

## Maven Project Structure

```

my-project/
├── src/
│   ├── main/
│   │   ├── java/
│   │   └── resources/
│   └── test/
│       ├── java/
│       └── resources/
├── target/
└── pom.xml

````

### Folder Explanation

- **src/main** : Contains the main application code.  
- **src/test** : Contains test code.  
- **target** : The build output directory where compiled classes and packaged artifacts are placed.  
- **pom.xml** : The Project Object Model (POM) file that defines project configuration.  

---

## POM (Project Object Model)

### pom.xml Structure

The `pom.xml` file contains the essential project information and configuration.

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>my-project</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>

    <!-- Dependencies, plugins, build settings, repositories, and more go here -->

</project>
````

---

### POM Tags Explanation

* **modelVersion** : This is the POM model version.
* **groupId** : A unique identifier for your project (company or package name).
* **artifactId** : The artifact (project) name.
* **version** : The project version.
* **packaging** : The type of packaging (e.g. `jar`, `war`, `pom`).

---

## Example POM with Dependencies

Below is a sample `pom.xml` file with dependencies added:

```xml
<project>
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>demo-app</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>

    <dependencies>

        <!-- Spring Core Dependency -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>5.3.30</version>
        </dependency>

        <!-- JUnit Dependency -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>

    </dependencies>
</project>
```

---

## What is a Dependency?

A **dependency** is an external library or framework that your project requires.

Examples:

* Spring → Backend framework
* JUnit → Testing framework
* MySQL Connector → Database connection

Maven automatically downloads the required libraries and manages versions.

---

## Dependency Tags Explanation

### `<dependencies>`

Container for all dependencies.

### `<dependency>`

Defines a single library.

### `<groupId>`

Company or organization name of the library.

### `<artifactId>`

Library name.

### `<version>`

Specific library version.

### `<scope>`

Controls how the library is used.

Common scopes:

* `compile` (default) – Used during compile and runtime
* `test` – Used only in testing
* `provided` – Provided by the environment (e.g. Tomcat)
* `runtime` – Used only at runtime

---

## Default and Predefined Values

### POM Defaults

#### `<packaging>`

Default: `jar` (if not defined)

---

#### `<modelVersion>`

No default 
Must be defined and usually always:

```
4.0.0
```

---

#### `<groupId>`, `<artifactId>`, `<version>`

No defaults 
Mandatory fields.

---

### Dependency Defaults

#### `<scope>`

Default value: `compile`

---

#### `<version>`

No default (x)
Version must be defined unless managed elsewhere.

---

## What Happens If You Miss Required Values?

| Field        | Result                |
| ------------ | --------------------- |
| modelVersion | Build fails           |
| groupId      | Build fails           |
| artifactId   | Build fails           |
| version      | Build fails           |
| packaging    | Defaults to `jar`     |
| scope        | Defaults to `compile` |

---

## Summary

* Maven follows a fixed directory structure.
* `pom.xml` controls dependency management and build logic.
* Dependencies are external libraries.
* Default packaging is `jar`.
* Default dependency scope is `compile`.
* Mandatory fields must always be declared.

---
---
---

## POM.xml 

There is a lots of information that can be added inside `pom.xml`.
Below are the important parts we are continuing with:

1. Project Metadata
2. Dependencies
3. Build Plugins
4. Profiles
5. Repositories
6. Other Sections

---

## 1. Project Metadata

This section contains the **basic identity** of the project.

### groupId

* Refers to the organization or project folder structure.
* Written in reverse domain format.
* Uniquely identifies your project group.

**Example:**

```
com.techwave
org.apache
io.github.sample
```

---

### artifactId

* Defines the name of the project/module.
* The final JAR/WAR file uses this name.

**Example:**

```
user-auth
inventory-service
payment-gateway
```

---

### version

* Declares the version of the project.
* `SNAPSHOT` indicates development stage.

**Example:**

```
1.0-SNAPSHOT
2.5.0
0.0.1
```

---

### packaging

* Defines what type of file Maven will build.

**Examples:**

```
jar  → Java application
war  → Web application
pom  → Parent project
ear  → Enterprise project
```

---

### Combined Example

```
groupId: com.techwave
artifactId: user-auth
version: 1.0-SNAPSHOT
packaging: jar
```

#### Meaning:

This is a Java JAR project named **user-auth** owned by **Techwave** with version `1.0-SNAPSHOT` (development version).

---

## 2. Dependencies

Dependencies are the **external libraries** required by the project.

We usually add:

* JARs
* Libraries
* Frameworks

#### Example:

If you are working on an **automation project** as a Test Engineer and using **Selenium WebDriver**, you:

1. Get Selenium’s `groupId`, `artifactId` and `version`
2. Add them inside `<dependencies>` in `pom.xml`
3. Maven downloads the related JARs automatically.

A dependency contains:

```
groupId
artifactId
version
scope (optional)
```

---

## 3. Build Plugins

Build plugins control the **execution and build behavior** of the project.

* They work based on lifecycle phases and goals.
* Different features are added using different plugins.

### Example:

If you want to compile with a **specific Java version**, you use:

```
maven-compiler-plugin
```

Other plugins:

* Surefire Plugin → run test cases
* Shade Plugin → create fat JAR
* Clean Plugin → clean build files

---

## 4. Profiles

Profiles allow changing behavior based on **environment** using the same code.

Example:

* Dev URL for Development
* Different DB for Testing
* Live API for Production

Profiles make application **environment-aware**.

#### Types:

```
Development
Testing
Production
```

---

## 5. Repositories

Repositories define where **dependencies are downloaded from**.

By default:

* Maven uses **Central Repository** (from Super POM)

If needed, we can:

* Add private repositories
* Hosting servers
* Custom company repos

---

## 6. Other Sections

#### Dependency Management

Used for:

* Multi-module projects
* Central version control
* Parent-child POM design

#### Properties

Used to:

* Store version numbers
* Avoid repetition
* Improve maintainability

---

## Summary

* `pom.xml` controls project configuration in Maven.
* **Project Metadata** defines project identity.
* **Dependencies** bring required libraries.
* **Build Plugins** manage build and execution.
* **Profiles** allow environment-specific behavior.
* **Repositories** decide where Maven downloads libraries from.
* **Dependency Management & Properties** increase maintainability and control.

---
---
---

# POM.xml (Continuation – Sample File Explained)

Below is a **sample `pom.xml` file** with comments to understand how each section works.

---

# Sample `pom.xml` with Explanation

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!-- Root element for every Maven project -->
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                             https://maven.apache.org/xsd/maven-4.0.0.xsd">

    <!-- Defines Maven POM model version -->
    <modelVersion>4.0.0</modelVersion>

    <!-- Organization / project group -->
    <groupId>com.example</groupId>

    <!-- Project name -->
    <artifactId>simple-demo</artifactId>

    <!-- Project version -->
    <version>1.0-SNAPSHOT</version>

    <!-- Output file type -->
    <packaging>jar</packaging>

    <!-- Human readable project name -->
    <name>Simple Demo Maven Project</name>

    <!-- Short project description -->
    <description>A simple Maven project example with clear comments.</description>


    <!-- Build configuration -->
    <build>
        <plugins>

            <!-- Compiler plugin -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.10.1</version>

                <!-- Java version configuration -->
                <configuration>
                    <source>17</source>
                    <target>17</target>
                </configuration>

            </plugin>

        </plugins>
    </build>


    <!-- Dependencies -->
    <dependencies>

        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>5.9.3</version>

            <!-- Available only during testing -->
            <scope>test</scope>
        </dependency>

    </dependencies>

</project>
```

---

# Notes on POM Elements

## Required Elements

These four fields **uniquely identify a Maven project**:

1. **modelVersion**

   * Specifies the POM schema version.
   * Almost always `4.0.0`.

2. **groupId**

   * Identifies the organization or package structure.
   * Uses reverse domain format.

3. **artifactId**

   * Name of the project.
   * Becomes the output file name.

4. **version**

   * Project version.
   * `SNAPSHOT` → development version
   * Without SNAPSHOT → stable release

---

## Common Optional Elements

1. **packaging**

   * Defines the output format (jar / war / pom / ear)

2. **name**

   * Readable project title.

3. **description**

   * Informational purpose only.

4. **build**

   * Manages compile process and build behavior.

5. **dependencies**

   * Defines external libraries used.

---

# How Maven Uses pom.xml

1. Maven reads `pom.xml`.
2. Downloads required dependencies.
3. Applies plugins and configurations.
4. Builds the project.
5. Generates output file.

---

# Output Naming Convention

Given:

```
groupId: com.example
artifactId: simple-demo
version: 1.0-SNAPSHOT
packaging: jar
```

Output will be:

```
simple-demo-1.0-SNAPSHOT.jar
```

---

# Summary

* `pom.xml` is the main configuration file in Maven.
* `<groupId>`, `<artifactId>`, `<version>`, `<modelVersion>` uniquely identify the project.
* `<dependencies>` manages libraries.
* `<build>` controls compilation and packaging.
* `<plugins>` provide extended functionality.
* `<packaging>` decides output format.
* Maven automatically downloads and manages libraries.

---

---

# SUPER POM
- a base model , where all the model implicitly inherited from a SuperPOM






