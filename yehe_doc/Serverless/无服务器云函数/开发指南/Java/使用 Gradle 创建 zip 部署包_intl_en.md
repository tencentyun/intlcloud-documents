
This document describes how to create a Java-type SCF function deployment package with Gradle. As long as the created zip package conforms to the following rules, it can be recognized and invoked by the SCF runtime environment.

* The compiled package, class files, and resource files are located in the root directory of the zip package.
* The jar package required by the dependencies is located in the `/lib` directory.

## Environment Preparations
Make sure that you have installed Java and Gradle. For the Java version, please use JDK 8. You can download and install the JDK appropriate for your system through OpenJDK (Linux) or at `www.java.com`.

### Installing Gradle
The specific installation instructions can be found at `https://gradle.org/install/`. The following describes how to install it manually:
1. Download Gradle's [binary package](https://services.gradle.org/distributions/gradle-4.1-bin.zip) or [full package with documentation and source code](https://services.gradle.org/distributions/gradle-4.1-all.zip).
2. Unzip the package to a desired directory, such as  `C:\Gradle` (Windows) or `/opt/gradle/gradle-4.1` (Linux).
3. Add the path of the `bin` directory in the unzipped directory to the system environment variable `PATH` in the following way as appropriate:
 - Linux: add through `export PATH=$PATH:/opt/gradle/gradle-4.1/bin`.
 - Windows: right click Computer and select `Properties > Advanced system settings > Advanced > Environment Variables`, select the `Path` variable, click Edit, and add `;C:\Gradle\bin;` at the end of the variable value.
4. Run the following command on the command line to check whether Gradle is installed correctly.
```
gradle -v
```
If the following is output, Gradle is properly installed. If you have any questions, please see Gradle's [official documentation](https://gradle.org/docs/).
```
	------------------------------------------------------------
	Gradle 4.1
	------------------------------------------------------------
	Build time:   2017-08-07 14:38:48 UTC
	Revision:     941559e020f6c357ebb08d5c67acdb858a3defc2
	Groovy:       2.4.11
	Ant:          Apache Ant(TM) version 1.9.6 compiled on June 29 2015
	JVM:          1.8.0_144 (Oracle Corporation 25.144-b01)
	OS:           Windows 7 6.1 amd64
```

## Code Preparations

### Preparing code file
1. Create a project folder in the selected location, such as `scf_example`.
2. In the root directory of the project folder, create a directory `src/main/java/` as the directory where the package is stored.
3. Create an `example` package directory in the created directory and then create a `Hello.java` file in the package directory. The final directory structure is formed as follows:
```
scf_example/src/main/java/example/Hello.java
```
4. Enter the following code content in the `Hello.java` file:
```java
package example;
public class Hello {
    public String mainHandler(String name, Context context) {
        System.out.println("Hello world!");
        return String.format("Hello %s.", name);
    }
}
```

### Preparing the compilation file
Create a `build.gradle` file in the root directory of the project folder and enter the following content:
```
apply plugin: 'java'

task buildZip(type: Zip) {
    from compileJava
    from processResources              
    into('lib') {
        from configurations.runtime
    }           
}

build.dependsOn buildZip
```

#### Using Maven Central library to handle package dependencies
If you need to reference the external package of Maven Central, you can add dependencies as needed. The content of the `build.gradle` file is as follows:
```
apply plugin: 'java'

repositories {
    mavenCentral()
}

dependencies {
    compile (
        'com.tencentcloudapi:scf-java-events:0.0.2'
    )
}

task buildZip(type: Zip) {
    from compileJava
    from processResources              
    into('lib') {
        from configurations.runtime
    }           
}

build.dependsOn buildZip
```

After `repositories` is used to indicate that the dependent library source is mavenCentral, Gradle will pull the dependencies from Maven Central during compilation, i.e., the `com.tencentcloudapi:scf-java-events:0.0.2` package specified in `dependencies`.

#### Using local Jar package to handle package dependencies
If you have already downloaded the Jar package to your local system, you can use the local library to handle package dependencies. In this case, create a `jars` directory in the root directory of the project folder and place the downloaded dependent Jar package into it. The content of the `build.gradle` file is as follows:
```
apply plugin: 'java'

dependencies {
    compile fileTree(dir: 'jars', include: '*.jar')
}

task buildZip(type: Zip) {
    from compileJava
    from processResources              
    into('lib') {
        from configurations.runtime
    }
}

build.dependsOn buildZip
```
After `dependencies` is used to indicate that the search directory is the `*.jar` file in the jars directory, the dependencies will be automatically searched for during compilation.

## Compilation and Packaging
Run the `gradle build` command in the root directory of the project folder, and the compilation output should be like the example below:
```
Starting a Gradle Daemon (subsequent builds will be faster)

BUILD SUCCESSFUL in 5s
3 actionable tasks: 3 executed
```
If a compilation failure is displayed, adjust the code based on the output compilation error message.
The compiled zip package is located in the `/build/distributions` directory of the project folder and named `scf_example.zip` after the project folder.

## Function Usage
After the zip package is generated after compilation and packaging, when creating or modifying a function, you can upload the package (if less than 10 MB) through the page or upload it (if bigger) to a COS bucket and then update it into the function through COS upload.
