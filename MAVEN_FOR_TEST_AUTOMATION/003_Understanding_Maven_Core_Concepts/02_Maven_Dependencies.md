# Understanding Maven Dependencies

## What are Dependencies?

Dependencies are **external libraries or frameworks** that your project needs to function properly.

Examples:

* Apache Commons
* Selenium WebDriver
* JUnit / TestNG
* Java Faker

Maven manages these libraries and their versions automatically, so you do not need to download JAR files manually.

---

## How Dependencies Work in Maven

### 1. Declaration

You declare dependencies inside the `pom.xml` file under the `<dependencies>` section.

### 2. Resolution

Maven automatically:

* Downloads required libraries from repositories
* Adds them to your project’s classpath

### 3. Scope

Scope defines **when** the dependency is used.

Common scopes:

* `compile` – default, used in build and run
* `test` – only for testing
* `runtime` – needed at runtime
* `provided` – provided by server/environment

---

## Example Use Case

* For fake data → **Java Faker**
* For UI automation → **Selenium WebDriver**
* For automation testing → **JUnit / TestNG**

Instead of manually downloading JARs, we just add dependencies in `pom.xml` and Maven handles everything.

---

## Example Dependency Declaration

```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.16.0</version>
</dependency>
```

---

## Key Points

### Transitive Dependencies

Maven also downloads dependencies **of your dependency automatically**.

### Centralized Management

All library versions are managed in one place – `pom.xml`.

---

## Benefits of Using Maven Dependencies

* Simplifies project setup
* Automatic downloads
* Consistent versions across environments
* Easy upgrades and maintenance
* No manual JAR handling

---

# Maven Significance in Dependency Management

Let’s understand Maven by comparing:

## Without Maven (Manual JAR Handling)

* Download JAR files manually
* Add them to classpath
* Handle version conflicts yourself
* Time-consuming and error-prone

### Sample Java Code (Manual JAR Setup)

```java
package io.learn;

import org.apache.commons.lang3.StringUtils;

public class Sample {
    public static void main(String[] args) {
        System.out.println(StringUtils.isNumeric("Rishabh"));
        System.out.println(StringUtils.isNumeric("9088765"));
    }
}
```

Manual setup works, but:

* Takes more time
* Configuration is difficult
* Updates are manual
* Hard to maintain

---

## With Maven

Maven handles:

* Downloading dependencies
* Project structure
* Version management

All you need is the `pom.xml`.

---

## Sample pom.xml (Using Maven)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <groupId>org.rishabh.maven</groupId>
    <artifactId>Project1</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>25</maven.compiler.source>
        <maven.compiler.target>25</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>

        <!-- JUnit for Testing -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>3.8.1</version>
            <scope>test</scope>
        </dependency>

        <!-- Apache Commons -->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-lang3</artifactId>
            <version>3.19.0</version>
        </dependency>

    </dependencies>

</project>
```

---

## Final Understanding

Maven follows **Convention over Configuration**.

Instead of:

* Creating folders manually
* Downloading JARs
* Managing versions

You only write:

* `pom.xml`
* Add dependencies
* Let Maven handle everything

Maven manages:

* Dependencies
* Plugins
* Packaging
* Builds
* Project structure

---

## Transitive Dependencies

Transitive dependencies are **indirect dependencies** that are downloaded automatically by Maven.

You do **not** explicitly add them in the `pom.xml` file.
When you add one dependency, Maven automatically downloads the **dependencies of that dependency**.

In short:

> Dependency → has its own dependencies → Maven downloads all of them.

---

### Example

If you add this dependency:

```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.19.0</version>
</dependency>
```

Internally, `commons-lang3` may depend on other libraries.

Maven will:

* Detect those internal dependencies
* Download them automatically
* Add them to your project classpath

You don’t need to:

* Search for them
* Add them manually
* Configure them

---

### Why Transitive Dependencies Matter

Without transitive dependency handling:

* You would need to manually find every required library
* Version conflicts would be common
* Builds could easily break

With Maven:

* Everything is resolved automatically
* Dependency chain is handled properly
* Builds become stable

---

## Centralized Dependency Management

Maven manages **all dependencies from a single place** → `pom.xml`.

This is called **centralized dependency management**.

Instead of:

* Managing JAR files in different folders
* Adding libraries manually
* Mixing versions

You only update:

```xml
<dependencies>
    ...
</dependencies>
```

Maven takes care of:

* Downloading correct versions
* Resolving conflicts
* Tracking dependency hierarchy
* Updating project classpath

---

### Benefits of Centralized Dependency Management

* Single source of truth (pom.xml)
* Easy to upgrade libraries
* Less configuration errors
* Cleaner project structure
* Better maintainability
* Version consistency

---

## Common Dependency Scopes

| Scope      | Description                          | Available Classpaths      | Use Case                 | Example Library |
| ---------- | ------------------------------------ | ------------------------- | ------------------------ | --------------- |
| `compile`  | Default scope. Available everywhere  | Compile, Runtime, Test    | Core project libraries   | commons-lang3   |
| `provided` | Provided by server or runtime        | Compile, Test             | Servlet API, Tomcat      | servlet-api     |
| `runtime`  | Not required to compile              | Runtime, Test             | JDBC drivers             | mysql-connector |
| `test`     | Used only for testing                | Test only                 | Unit testing frameworks  | junit, testng   |
| `system`   | Provided manually                    | Compile, Test             | External local JAR files | custom-lib.jar  |
| `import`   | Used to import dependency management | DependencyManagement only | BOM management           | Spring Boot BOM |

---

## Explanation of Each Scope

### 1. Compile (Default)

* Used in all phases
* Automatically included
* Needed to run and compile the application

Example:

```xml
<scope>compile</scope>
```

---

### 2. Provided

* Available during compile
* Not included in final build
* Expected from environment (e.g., server)

Example:

```xml
<scope>provided</scope>
```

Used for:

* Servlet API
* JSP libraries
* Tomcat classes

---

### 3. Runtime

* Not needed while compiling
* Required when application runs

Example:

```xml
<scope>runtime</scope>
```

Used for:

* Database drivers
* Runtime engines

---

### 4. Test

* Only for test cases
* Not available in production code

Example:

```xml
<scope>test</scope>
```

Used for:

* JUnit
* TestNG
* Mockito

---

### 5. System

* JAR must be provided manually
* Not downloaded by Maven
* Hardcoded path required

Example:

```xml
<scope>system</scope>
<systemPath>${project.basedir}/libs/custom.jar</systemPath>
```

Not recommended unless necessary.

---

### 6. Import

* Used inside `dependencyManagement`
* Imports group of dependencies (BOM file)

Example:

```xml
<scope>import</scope>
```

Used in:

* Spring Boot BOM
* Cloud dependencies

---

## Summary

| Scope    | When Used          |
| -------- | ------------------ |
| compile  | All phases         |
| provided | Compile + Test     |
| runtime  | Runtime only       |
| test     | Test phase only    |
| system   | Local machine only |
| import   | Version management |

---

## Final Note

Choosing the correct scope:

* Improves build speed
* Avoids conflicts
* Reduces jar size
* Increases project stability

---

