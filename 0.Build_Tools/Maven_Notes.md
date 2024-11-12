# Introduction to Maven

- [Maven Official Website](https://maven.apache.org/)

**Apache Maven** is a build automation and project management tool primarily used for Java projects. It simplifies the build process by providing a uniform build system, dependency management, and project information.

## Why Maven?

- **Standardization**: Maven provides a standardized project structure and build lifecycle, which makes it easier to understand and manage projects.
- **Dependency Management**: Automatically handles project dependencies and transitive dependencies, reducing manual configuration.
- **Extensibility**: Supports various plugins and integrations to extend its functionality for tasks like testing, packaging, and deployment.

## Basic History

- **2004**: Maven was initially released by the Apache Software Foundation, following the success of Apache Ant, a previous build tool that lacked standardized project structure.
- **2005**: Maven 2 introduced significant improvements, including a new project object model (POM) and better support for dependency management.
- **2014**: Maven 3 was released with enhanced performance and improved support for multi-module projects.

Maven has since become a widely adopted tool in the Java ecosystem, valued for its consistency and ease of managing complex projects.

## Maven Build Lifecycle

The **Maven Build Lifecycle** is a sequence of phases that define the steps required to build and manage a project. Each phase represents a stage in the build process and is executed in a specific order. 

## Key Phases

1. **`validate`**: Validates the project structure and configuration.
2. **`compile`**: Compiles the source code.
3. **`test`**: Runs tests on the compiled code.
4. **`package`**: Packages the compiled code into a distributable format, such as JAR or WAR.
5. **`verify`**: Runs additional checks to ensure the package is valid and meets quality standards.
6. **`install`**: Installs the package into the local repository for use as a dependency in other projects.
7. **`deploy`**: Copies the package to a remote repository for sharing with other developers or projects.

The default lifecycle in Maven is **`default`**, but there are also **`clean`** and **`site`** lifecycles for cleaning and site generation tasks, respectively.

Each phase can be bound to specific plugins that perform tasks related to that phase.

---

# Steps to Install Apache Maven

To install Apache Maven on your system, follow these steps:

## Prerequisites

1. **Java Development Kit (JDK)**
   - Ensure that JDK is installed on your system. Maven requires JDK 8 or later.
   - Verify installation by running:
     ```bash
     java -version
     ```

## Installation Steps

### 1. Download Maven

1. Visit the [Apache Maven Download Page](https://maven.apache.org/download.cgi).
2. Download the latest version of the binary zip archive (e.g., `apache-maven-x.x.x-bin.zip`).

### 2. Extract the Archive

1. Extract the downloaded zip file to a directory of your choice.
   ```bash
   unzip apache-maven-x.x.x-bin.zip
   ```

### 3. Set Environment Variables

1. **Linux/MacOS**
   - Open or create the file `~/.bashrc` or `~/.zshrc` and add the following lines:
     ```bash
     export M2_HOME=/path/to/apache-maven-x.x.x
     export M2=$M2_HOME/bin
     export PATH=$M2:$PATH
     ```
   - Reload the configuration:
     ```bash
     source ~/.bashrc
     ```
   
2. **Windows**
   - Open the System Properties (Right-click on My Computer > Properties > Advanced system settings).
   - Click on **Environment Variables**.
   - Add a new **System Variable**:
     - **Variable name**: `M2_HOME`
     - **Variable value**: `C:\path\to\apache-maven-x.x.x`
   - Edit the `Path` variable and add `%M2_HOME%\bin`.

### 4. Verify Installation

1. Open a new terminal or command prompt.
2. Run the following command to check Maven version:
   ```bash
   mvn -version
   ```
   This should display the Maven version and other relevant details if installed correctly.

You have now successfully installed Apache Maven on your system.

---

# Creating a New Maven Project from Terminal

To create a new Maven project using the terminal, follow these steps:

## Steps to Create a New Maven Project

### 1. Open Terminal

- Open your terminal or command prompt.

### 2. Navigate to the Desired Directory

- Change to the directory where you want to create your Maven project:
  ```bash
  cd /path/to/your/directory
  ```

### 3. Run Maven Command

- Use the following Maven command to generate a new project:
  ```bash
  mvn archetype:generate -DgroupId=com.example -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
  ```

- Here is what each parameter means :

  - **`archetype:generate`**: This specifies the goal of maven, in this case the goal is to generate a maven project.
  - **`-DgroupId`**: Specifies the group ID for your project (e.g., `com.example`). (Typically follows a reverse domain name notation)
  - **`-DartifactId`**: Specifies the artifact ID (name) for your project (e.g., `my-app`).
  - **`-DarchetypeArtifactId`**: Defines the archetype to use (e.g., `maven-archetype-quickstart` for a simple Java project).
  - **`-DinteractiveMode=false`**: Runs the command in non-interactive mode, using the provided parameters without prompting for additional input.
  

### 4. Navigate to the Project Directory

- Change to the newly created project directory:
  ```bash
  cd my-app
  ```

### 5. Build the Project

- Run the Maven build command to compile and package the project:
  ```bash
  mvn package
  ```

### 6. Verify the Project

- Check the `target` directory for the generated `.jar` file:
  ```bash
  ls target
  ```

You have now successfully created and built a new Maven project!

---

# Maven Dependency Resolution

Maven resolves dependencies through a structured process:

1. **Project Object Model (POM) Analysis**
   - Reads the `pom.xml` file to identify required dependencies and their versions.

2. **Local Repository Check**
   - Looks in the local repository (`~/.m2/repository`) to see if the dependencies are already present.

3. **Remote Repository Lookup**
   - Queries remote repositories (e.g., Maven Central) if dependencies are not found locally.

4. **Dependency Resolution**
   - Downloads required dependencies and their transitive dependencies to the local repository.

5. **ClassPath Assembly**
   - Assembles dependencies into the project's classpath for compilation and runtime.

This process ensures that all necessary dependencies are correctly managed and available for your project.

---

# Maven Scope Tags in `pom.xml`

Maven uses scope tags in the `pom.xml` file to manage the visibility and lifetime of dependencies. Here’s a breakdown of the different scope tags:

## 1. **compile**

- **Description**: Default scope if no other scope is specified.
- **Visibility**: Available in all classpaths (compile, test, runtime).
- **Usage**: Used for dependencies that are required for compiling, running, and testing the project.

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>example-lib</artifactId>
    <version>1.0.0</version>
    <scope>compile</scope>
</dependency>
```

## 2. **provided**

- **Description**: The dependency is provided by the runtime environment and does not need to be packaged with the application.
- **Visibility**: Available at compile-time and test-time but not included in the runtime classpath.
- **Usage**: Used for dependencies that are provided by the container or runtime (e.g., servlet API).

```xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
    <scope>provided</scope>
</dependency>
```

## 3. **runtime**

- **Description**: The dependency is required at runtime but not at compile-time.
- **Visibility**: Available in the runtime and test classpaths, but not in the compile classpath.
- **Usage**: Used for libraries that are needed for execution but not for compiling the code.

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>example-runtime-lib</artifactId>
    <version>1.0.0</version>
    <scope>runtime</scope>
</dependency>
```

## 4. **test**

- **Description**: The dependency is only needed for compiling and running tests.
- **Visibility**: Available only in the test classpath.
- **Usage**: Used for testing libraries and frameworks (e.g., JUnit).

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>
```

## 5. **system**

- **Description**: The dependency is provided by the system and should be referenced from a specific location.
- **Visibility**: Available at compile-time and runtime but not in the Maven repository.
- **Usage**: Typically used for system-specific dependencies, requires an explicit path.

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>example-system-lib</artifactId>
    <version>1.0.0</version>
    <scope>system</scope>
    <systemPath>${project.basedir}/lib/example-system-lib.jar</systemPath>
</dependency>
```

## 6. **import**

- **Description**: Special scope used only in `<dependencyManagement>` sections to import dependency management from other POMs.
- **Usage**: Allows importing dependency management information from another POM.

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-framework-bom</artifactId>
            <version>5.3.8</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

These scopes help control how dependencies are included in your build process, ensuring the right dependencies are available at the right time.

---

# Maven `<exclusions>` Tag in `pom.xml`

The `<exclusions>` tag in Maven is used to prevent specific transitive dependencies from being included in your project. This is particularly useful when you want to avoid conflicts or unnecessary dependencies that come along with a primary dependency.

## **Purpose**

- **Avoid Conflicts**: Prevent version conflicts by excluding a transitive dependency that may be included with a library you are using.
- **Reduce Size**: Minimize the size of your build by excluding unneeded dependencies.
- **Prevent Redundancy**: Avoid including duplicate libraries that are already provided by other dependencies.

## **Usage**

The `<exclusions>` tag is used within a `<dependency>` section to specify which transitive dependencies should be excluded.

### **Example**

Suppose you are using `library-a` which transitively depends on `library-b`. However, you want to exclude `library-b` from being included in your project.

```xml
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>library-a</artifactId>
        <version>1.0.0</version>
        <exclusions>
            <exclusion>
                <groupId>com.example</groupId>
                <artifactId>library-b</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
</dependencies>
```

In this example:
- `library-b` will not be included in the final build, even though `library-a` depends on it.

## **Syntax**

```xml
<dependency>
    <groupId>dependency-group-id</groupId>
    <artifactId>dependency-artifact-id</artifactId>
    <version>dependency-version</version>
    <exclusions>
        <exclusion>
            <groupId>excluded-dependency-group-id</groupId>
            <artifactId>excluded-dependency-artifact-id</artifactId>
        </exclusion>
        <!-- Additional exclusions can be added here -->
    </exclusions>
</dependency>
```

## **Key Points**

- **Multiple Exclusions**: You can exclude multiple dependencies by adding multiple `<exclusion>` elements within the `<exclusions>` tag.
- **Scope of Exclusions**: Exclusions apply to the specific dependency in which they are defined, affecting only its transitive dependencies.

Using the `<exclusions>` tag helps maintain a clean and manageable dependency tree, ensuring that only the necessary libraries are included in your project.

---

# Maven Clean Lifecycle

The Maven Clean Lifecycle is designed to remove files generated at build time and to prepare a clean slate for subsequent builds. This lifecycle helps ensure that builds start from a clean state, avoiding potential issues from leftover files or artifacts.

## **Lifecycle Phases**

The Clean Lifecycle consists of three main phases:

### **1. `pre-clean`**

- **Description**: This phase is executed before the actual cleaning process begins.
- **Purpose**: Used for any tasks that need to be performed before cleaning, such as backup or preparation tasks.

```xml
<phase>pre-clean</phase>
```

### **2. `clean`**

- **Description**: This is the core phase where the build output directory (`target` by default) is deleted.
- **Purpose**: Removes all files and directories generated by previous builds to ensure that the new build starts from a clean state.

```xml
<phase>clean</phase>
```

### **3. `post-clean`**

- **Description**: This phase is executed after the cleaning process is complete.
- **Purpose**: Used for tasks that need to occur after cleaning, such as restoring or validating post-clean status.

```xml
<phase>post-clean</phase>
```

## **Execution**

To execute the Clean Lifecycle, use the following Maven command:

```sh
mvn clean
```

This command will run all phases of the Clean Lifecycle in sequence: `pre-clean`, `clean`, and `post-clean`.

## **Common Goals**

- **Deleting Artifacts**: Ensures that the `target` directory and any other build artifacts are removed.
- **Avoiding Build Issues**: Prevents potential issues caused by stale files or outdated artifacts from previous builds.

## **Configuration**

While the Clean Lifecycle itself cannot be customized beyond its predefined phases, you can configure the plugins bound to these phases in your `pom.xml`. For example, you might use the Maven Clean Plugin to customize the cleaning process.

### **Example Configuration**

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-clean-plugin</artifactId>
            <version>3.2.0</version>
            <configuration>
                <!-- Custom configuration here -->
                <filesets>
                    <fileset>
                        <directory>${basedir}/temp</directory>
                        <includes>
                            <include>**/*.tmp</include>
                        </includes>
                    </fileset>
                </filesets>
            </configuration>
        </plugin>
    </plugins>
</build>
```

In this example, the Maven Clean Plugin is configured to delete files with a `.tmp` extension from the `temp` directory.

## **Key Points**

- **Purpose**: The Clean Lifecycle is essential for maintaining a consistent build environment by removing old artifacts and ensuring that builds are performed on a clean slate.
- **Usage**: Typically invoked before other build lifecycles like `compile` or `package` to ensure no residual files affect the build process.

Using the Clean Lifecycle effectively helps manage build cleanliness and prevent issues related to leftover build artifacts.

---

# Maven Site Lifecycle

The Maven Site Lifecycle is used to generate a project site, which includes documentation, reports, and other project-related information. This lifecycle helps create a comprehensive and well-organized project site, which can be useful for sharing information with stakeholders.

## **Lifecycle Phases**

The Site Lifecycle consists of the following main phases:

### **1. `pre-site`**

- **Description**: This phase is executed before the actual site generation process begins.
- **Purpose**: Allows for tasks that need to be performed before generating the site, such as preparing files or configurations.

```xml
<phase>pre-site</phase>
```

### **2. `site`**

- **Description**: This is the core phase where the site is generated.
- **Purpose**: Creates the site content, including project reports and documentation, usually in the `target/site` directory.

```xml
<phase>site</phase>
```

### **3. `post-site`**

- **Description**: This phase is executed after the site generation process is complete.
- **Purpose**: Used for tasks that need to occur after site generation, such as additional processing or packaging of the generated site.

```xml
<phase>post-site</phase>
```

### **4. `site-deploy`**

- **Description**: This phase is used to deploy the generated site to a web server or repository.
- **Purpose**: Deploys the site to a specified location, such as an HTTP server or a file system, to make it publicly available.

```xml
<phase>site-deploy</phase>
```

## **Execution**

To execute the Site Lifecycle, use the following Maven command:

```sh
mvn site
```

This command will run the phases `pre-site`, `site`, and `post-site` in sequence, but not `site-deploy`. To deploy the site, use:

```sh
mvn site-deploy
```

## **Common Goals**

- **Documentation**: Generates project documentation, including Javadoc, dependency reports, and other useful information.
- **Reports**: Creates various reports such as test coverage, code quality, and other metrics related to the project.
- **Deployment**: Optionally deploys the generated site to a web server or repository for access by users and stakeholders.

## **Configuration**

You can configure the site generation process and the Maven Site Plugin in your `pom.xml`. For example, you might customize the reports and documentation generated by specifying plugins and their configurations.

### **Example Configuration**

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-site-plugin</artifactId>
            <version>3.12.1</version>
            <configuration>
                <reportPlugins>
                    <reportPlugin>
                        <groupId>org.apache.maven.plugins</groupId>
                        <artifactId>maven-project-info-reports-plugin</artifactId>
                    </reportPlugin>
                </reportPlugins>
            </configuration>
        </plugin>
    </plugins>
</build>
```

In this example, the Maven Site Plugin is configured to include additional reports in the generated site.

## **Key Points**

- **Purpose**: The Site Lifecycle is crucial for generating and managing project documentation and reports, providing a comprehensive view of the project’s status and details.
- **Usage**: Typically invoked during or after the build process to create and deploy the project site.

Using the Site Lifecycle helps ensure that your project has up-to-date documentation and reports, making it easier for stakeholders to understand and assess the project.

---

# Maven Multi-Module Dependency Management

In Maven, a multi-module project allows you to manage multiple related projects or modules within a single parent project. This setup facilitates dependency management, versioning, and build processes across related modules.

## **Structure of a Multi-Module Project**

A multi-module Maven project typically consists of a parent POM (`pom.xml`) and multiple child modules. Here’s a basic structure:

```
my-project
│
├── pom.xml (Parent POM)
├── module-a
│   └── pom.xml
├── module-b
│   └── pom.xml
└── module-c
    └── pom.xml
```

### **Parent POM**

The parent POM coordinates the build process and manages common configuration for all modules.

#### **Example Parent POM**

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>my-project</artifactId>
    <version>1.0.0</version>
    <packaging>pom</packaging>

    <modules>
        <module>module-a</module>
        <module>module-b</module>
        <module>module-c</module>
    </modules>

    <dependencyManagement>
        <dependencies>
            <!-- Define common dependency versions here -->
            <dependency>
                <groupId>org.apache.commons</groupId>
                <artifactId>commons-lang3</artifactId>
                <version>3.12.0</version>
            </dependency>
        </dependencies>
    </dependencyManagement>
</project>
```

### **Child Module POM**

Each child module has its own POM file, which defines module-specific configurations and dependencies.

#### **Example Module POM**

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>com.example</groupId>
        <artifactId>my-project</artifactId>
        <version>1.0.0</version>
        <relativePath>../pom.xml</relativePath>
    </parent>
    <artifactId>module-a</artifactId>

    <dependencies>
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-lang3</artifactId>
        </dependency>
        <!-- Module dependencies -->
    </dependencies>
</project>
```

## **Managing Dependencies Between Modules**

In a multi-module project, you can define dependencies between modules. This is done by specifying the module’s artifact ID as a dependency in another module’s POM.

### **Example**

Assume `module-b` depends on `module-a`. Configure `module-b`’s POM as follows:

```xml
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>module-a</artifactId>
        <version>1.0.0</version>
    </dependency>
    <!-- Other dependencies -->
</dependencies>
```

## **Build and Dependency Resolution**

- **Building**: Run `mvn install` from the parent project directory to build all modules in the correct order, ensuring that dependencies are resolved correctly.
- **Dependency Resolution**: Maven automatically resolves dependencies between modules based on the POM files. If `module-b` depends on `module-a`, Maven ensures that `module-a` is built before `module-b`.

## **Key Points**

- **Centralized Management**: The parent POM allows for centralized dependency and plugin management, ensuring consistent versions across modules.
- **Modularization**: Modules can be built and tested independently while sharing common configurations and dependencies.
- **Inheritance**: Child modules inherit configurations from the parent POM, simplifying management and reducing duplication.

Using a multi-module project structure in Maven helps manage complex projects by organizing them into smaller, manageable units while maintaining centralized control over common aspects like dependencies and build configurations.

---

# Maven `<dependencyManagement>` Tag in `pom.xml`

The `<dependencyManagement>` tag in Maven is used to define and manage dependency versions for a project. It allows you to centralize the versioning of dependencies and ensure consistency across multiple modules in a multi-module project.

## **Purpose**

- **Centralized Versioning**: Manage versions of dependencies in one place rather than specifying them individually in each module.
- **Consistent Dependencies**: Ensure that all modules use the same version of a dependency, reducing version conflicts and inconsistencies.
- **Simplified Dependency Declaration**: Avoid specifying versions in individual module POMs, which simplifies the dependency declarations.

## **Usage**

The `<dependencyManagement>` tag is typically used in the parent POM of a multi-module project. Dependencies defined here are not directly included in the build but are available to child modules that declare them.

### **Example Parent POM with `<dependencyManagement>`**

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>parent-project</artifactId>
    <version>1.0.0</version>
    <packaging>pom</packaging>

    <dependencyManagement>
        <dependencies>
            <!-- Define versions for common dependencies here -->
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-core</artifactId>
                <version>5.3.9</version>
            </dependency>
            <dependency>
                <groupId>org.apache.commons</groupId>
                <artifactId>commons-lang3</artifactId>
                <version>3.12.0</version>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <modules>
        <module>module-a</module>
        <module>module-b</module>
    </modules>
</project>
```

### **Child Module Usage**

In child modules, you can reference dependencies defined in the parent `<dependencyManagement>` without specifying their versions:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>com.example</groupId>
        <artifactId>parent-project</artifactId>
        <version>1.0.0</version>
        <relativePath>../pom.xml</relativePath>
    </parent>
    <artifactId>module-a</artifactId>

    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <!-- Version is inherited from parent dependencyManagement -->
        </dependency>
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-lang3</artifactId>
            <!-- Version is inherited from parent dependencyManagement -->
        </dependency>
    </dependencies>
</project>
```

## **Key Points**

- **Inheritance**: Child modules inherit dependency versions from the parent’s `<dependencyManagement>`, simplifying dependency declarations and ensuring consistency.
- **No Direct Inclusion**: Dependencies defined in `<dependencyManagement>` are not automatically included in the build. You must explicitly declare them in the `<dependencies>` section of each module.
- **Version Control**: Manage versions of dependencies centrally to avoid version conflicts and ensure all modules use the same version of a library.

The `<dependencyManagement>` tag helps streamline dependency management in Maven projects, particularly in multi-module setups, by centralizing version control and reducing redundancy in dependency declarations.

---

# Maven `<plugins>` Tag in `pom.xml`

The `<plugins>` tag in Maven is used to configure and manage plugins that provide various build functionalities and lifecycle goals. Plugins are essential for extending Maven's capabilities, including tasks such as compiling code, running tests, and packaging applications.

## **Purpose**

- **Extend Functionality**: Plugins add specific tasks and goals to the Maven build lifecycle.
- **Custom Build Processes**: Configure plugins to tailor the build process to meet project requirements.
- **Automation**: Automate common tasks like code generation, testing, and deployment.

## **Usage**

Plugins are defined within the `<build>` section of the `pom.xml` file, using the `<plugins>` tag. You can specify plugin configurations, versions, and goals.

### **Example Parent POM with `<plugins>`**

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>parent-project</artifactId>
    <version>1.0.0</version>
    <packaging>pom</packaging>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>2.22.2</version>
                <configuration>
                    <includes>
                        <include>**/*Test.java</include>
                    </includes>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

### **Child Module Usage**

Child modules inherit the plugin configuration from the parent POM but can override or extend it if needed.

#### **Example Module POM**

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>com.example</groupId>
        <artifactId>parent-project</artifactId>
        <version>1.0.0</version>
        <relativePath>../pom.xml</relativePath>
    </parent>
    <artifactId>module-a</artifactId>

    <build>
        <plugins>
            <!-- Override or add additional plugins as needed -->
        </plugins>
    </build>
</project>
```

## **Common Plugin Configurations**

- **Version**: Specify the version of the plugin to use.
- **Configuration**: Customize plugin behavior through the `<configuration>` tag, where you can set specific options and parameters.
- **Goals**: Each plugin provides specific goals (e.g., `compile`, `test`, `package`) that can be bound to different phases of the build lifecycle.

### **Example Configuration**

Configuring the Maven Compiler Plugin to use Java 11:

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.8.1</version>
    <configuration>
        <source>11</source>
        <target>11</target>
    </configuration>
</plugin>
```

## **Key Points**

- **Inheritance**: Plugins and their configurations defined in the parent POM are inherited by child modules, ensuring consistent build processes.
- **Customization**: Child modules can override or extend parent plugin configurations as needed.
- **Lifecycle Integration**: Plugins are bound to specific lifecycle phases to execute goals automatically during the build process.

The `<plugins>` tag is crucial for managing build tasks and customizing the Maven build process, making it adaptable to various project requirements and workflows.

---

# Maven Wrapper

The Maven Wrapper (`mvnw`) is a script that enables projects to use a specific version of Apache Maven without requiring it to be installed globally. It ensures that all developers on a project use the same Maven version, leading to consistent builds across different environments.

## **Key Features**

- **Version Consistency**: Ensures all developers use the same Maven version, reducing build inconsistencies.
- **Ease of Use**: Simplifies setup for new developers by automatically downloading the required Maven version.
- **No Global Installation Required**: Allows specifying a Maven version without needing a global Maven installation.

## **Components**

The Maven Wrapper consists of the following components:

1. **Wrapper Scripts**:
   - `mvnw` (for Unix-based systems like Linux and macOS)
   - `mvnw.cmd` (for Windows systems)

   These scripts are used to invoke Maven with the specified version.

2. **Wrapper JAR and Properties**:
   - `mvn/wrapper/maven-wrapper.jar`: JAR file responsible for downloading and setting up the specified Maven version.
   - `mvn/wrapper/maven-wrapper.properties`: Configuration file specifying the Maven version and distribution URL.

## **How It Works**

1. **Setup**: Add the Maven Wrapper to your project using the following command:

   ```sh
   mvn wrapper:wrapper
   ```

   This command generates the necessary wrapper files in your project.

2. **Configuration**: Define the Maven version to use in the `mvn/wrapper/maven-wrapper.properties` file. Example configuration:

   ```properties
   distributionUrl=https://repo.maven.apache.org/maven2/org/apache/maven/apache-maven/3.8.6/apache-maven-3.8.6-bin.zip
   ```

3. **Execution**: Use the wrapper script to build your project:

   ```sh
   ./mvnw clean install
   ```

   On Windows:

   ```sh
   mvnw.cmd clean install
   ```

   The wrapper script checks if the specified Maven version is available locally; if not, it downloads it and runs the command.

## **Example Configuration**

Here is an example `mvn/wrapper/maven-wrapper.properties` file:

```properties
# Maven Wrapper Properties
distributionUrl=https://repo.maven.apache.org/maven2/org/apache/maven/apache-maven/3.8.6/apache-maven-3.8.6-bin.zip
```

## **Benefits**

- **Consistency**: Ensures the same Maven version is used across different environments and by all team members.
- **Ease of Setup**: New developers can start building the project without worrying about Maven installation or version issues.
- **Project Portability**: The project configuration includes everything needed to build it, making it easier to share and set up in different environments.

## **Key Points**

- **Wrapper Scripts**: Use `mvnw` (Unix) and `mvnw.cmd` (Windows) to invoke Maven with the specified version.
- **Version Management**: Control the Maven version used for the project through `maven-wrapper.properties`.
- **Local Maven Download**: The wrapper downloads Maven if it's not available locally.

The Maven Wrapper is a powerful tool for ensuring build consistency and simplifying project setup, especially in collaborative development environments.

---













