This document describes how to [create a zip deployment package with Gradle](#UseGradle) and [create a jar deployment package with Maven](#UseMaven). Then, you can upload the created package (if less than 50 MB) directly in the SCF console, or upload it to a COS bucket and then specify the bucket and object information in the SCF console.


## Creating zip Deployment Package with Gradle[](id:UseGradle)
This document describes how to create a Java-type SCF function deployment package with Gradle. As long as the created zip package conforms to the following rules, it can be recognized and invoked by the SCF runtime environment.
* The compiled package, class files and resource files are located in the root directory of the zip package.
* The jar package required by the dependencies is located in the /lib directory.

### Preparing environment

Make sure that you have Java and Gradle installed.
- For Java 11, install TencentKona 11 or JDK 11.
- For Java 8, install JDK 8. You can download and install the JDK appropriate for your system by using OpenJDK (Linux) or through [Java](https://www.java.com/zh-CN/).

#### Installing Gradle
For Gradle installation details, see [Gradle Installation](https://gradle.org/install/). The manual installation steps are as follows:

1. Download Gradle's [binary package](https://services.gradle.org/distributions/gradle-4.1-bin.zip) or [full package with documentation and source code](https://services.gradle.org/distributions/gradle-4.1-all.zip).
2. Unzip the package to a desired directory, such as `C:\Gradle` (Windows) or `/opt/gradle/gradle-4.1` (Linux).
3. Add the path of the `bin` directory in the unzipped directory to the system environment variable `PATH` in the following way as appropriate:
 - Linux: Add through `export PATH=$PATH:/opt/gradle/gradle-4.1/bin`.
 - Windows: Right click Computer and select **Properties > Advanced system settings > Advanced > Environment Variables**, select the `Path` variable, click Edit, and add `;C:\Gradle\bin;` at the end of the variable value.
4. Run the following command on the command line to check whether Gradle is installed correctly.
```
gradle -v
```
If the following is output, Gradle is properly installed. If you have any questions, see Gradle's [official documentation](https://gradle.org/docs/).
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

### Preparing code

#### Preparing code file

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

#### Preparing compilation file

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

#### Using local jar package to handle package dependencies

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

### Compiling and packaging

Execute the command `gradle build` in the root directory of the project folder, and the compilation output should be like the example below:

```
Starting a Gradle Daemon (subsequent builds will be faster)

BUILD SUCCESSFUL in 5s
3 actionable tasks: 3 executed
```

If a compilation failure is displayed, adjust the code based on the outputted compilation error message.
The compiled zip package is located in the `/build/distributions` directory of the project folder and named `scf_example.zip` after the project folder.

## Creating jar Deployment Package Using Maven[](id:UseMaven)

This document describes how to create a Java-type function deployment jar package with Maven.

### Preparing environment

Make sure that you have Java and Gradle installed.
- For Java 11, install TencentKona 11 or JDK 11.
- For Java 8, install JDK 8. You can download and install the JDK appropriate for your system by using OpenJDK (Linux) or through [Java](https://www.java.com/zh-CN/).

#### Installing Maven
For Maven installation details, see [Installing Apache Maven](https://maven.apache.org/install.html). The manual installation steps are as follows: 

1. Download Maven's zip or tar.gz package.
2. Unzip the package to a desired directory, such as `C:\Maven` (Windows) or `/opt/mvn/apache-maven-3.5.0` (Linux).
3. Add the path of the `bin` directory in the unzipped directory to the system environment variable `PATH` in the following way as appropriate:
 - Linux: Add through `export PATH=$PATH:/opt/mvn/apache-maven-3.5.0/bin`.
 - Windows: Right click Computer and select **Properties > Advanced system settings > Advanced > Environment Variables**, select the `Path` variable, click Edit, and add `;C:\Maven\bin;` at the end of the variable value.
4. Run the following command on the command line to check whether Maven is installed correctly.
```
mvn -v
```
If the following is output, Maven is properly installed. If you have any questions, see Maven's [official documentation](https://maven.apache.org/install.html).
```
Apache Maven 3.5.0 (ff8f5e7444045639af65f6095c62210b5713f426; 2017-04-04T03:39:06+08:00)
Maven home: C:\Program Files\Java\apache-maven-3.5.0\bin\..
Java version: 1.8.0_144, vendor: Oracle Corporation
Java home: C:\Program Files\Java\jdk1.8.0_144\jre
Default locale: zh_CN, platform encoding: GBK
OS name: "windows 7", version: "6.1", arch: "amd64", family: "windows"
```

### Preparing code

#### Preparing code file

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

#### Preparing compilation file

Create a `pom.xml` file in the root directory of the project folder and enter the following content:
<dx-codeblock>
::: Java\s11 Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>examples</groupId>
  <artifactId>java-example</artifactId>
  <packaging>jar</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>java-example</name>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
        <version>2.3</version>
        <configuration>
          <source>11</source>
          <target>11</target>
        </configuration>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>shade</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
:::
::: Java\s8 Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>examples</groupId>
  <artifactId>java-example</artifactId>
  <packaging>jar</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>java-example</name>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
        <version>2.3</version>
        <configuration>
          <createDependencyReducedPom>false</createDependencyReducedPom>
        </configuration>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>shade</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
:::
</dx-codeblock>



#### Using Maven Central library to handle package dependencies

If you need to reference the external package of Maven Central, you can add dependencies as needed. The content of the `pom.xml` file is as follows. To add dependencies, pay attention to the `<dependencies>` section.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>examples</groupId>
  <artifactId>java-example</artifactId>
  <packaging>jar</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>java-example</name>
  
  <dependencies>
    <dependency>
      <groupId>com.tencentcloudapi</groupId>
      <artifactId>scf-java-events</artifactId>
      <version>0.0.2</version>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
        <version>2.3</version>
        <configuration>
          <createDependencyReducedPom>false</createDependencyReducedPom>
        </configuration>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>shade</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

### Compiling and packaging

Execute the command `mvn package` in the root directory of the project folder, and the compilation output should be like the example below:
```
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building java-example 1.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO]
...
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.785 s
[INFO] Finished at: 2017-08-25T10:53:54+08:00
[INFO] Final Memory: 17M/214M
[INFO] ------------------------------------------------------------------------
```
If a compilation failure is displayed, adjust the code based on the outputted compilation error message.
The compiled zip package is located in the `target` directory of the project folder and named `java-example-1.0-SNAPSHOT.jar` after the artifactId and version fields in pom.xml.

