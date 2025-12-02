# maven project structure 
my-project/
    |---src/
    |    |-main/
    |    |   |--java/
    |    |   |--resources/
    |    |-test/
    |    |   |--java/
    |    |   |--resources/
    |---target/
    |---pom.xml

- src/main: contains the main application code.
- src/test : contains test code.
- target : The build output directory where compiled classes and pacckaged artofacts arw palced.
- pom.cxml : The project Object model (POM) file that defines project configuration.

# POM (project Object Model ):
pom.xml structure
- the pom.xml file contain the essential project information and configuration.

'''
<project>
    <modelVersion>4.0.0</modelversion>
    <groupId>com.example</groupId>
    <artifactID>my-project</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packkaging>
    <!-- Dependencies , plugins, build Settings, repository, and more go here-->
</project>    
'''
whole
- modelverison : This is the POM model version.
- groupId : A unique identifier for your project .
- artifactId: The name of artofact (project).
- version :The project's version.
- packaging : The type of packaguinf (eg. jar , war , pom )

ex of POM with labels







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

No default ❌
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

```


