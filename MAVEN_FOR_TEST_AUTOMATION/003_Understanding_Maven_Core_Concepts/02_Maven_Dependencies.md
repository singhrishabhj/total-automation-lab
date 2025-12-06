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

