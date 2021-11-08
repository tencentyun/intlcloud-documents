
This document describes how to create a Java-type function deployment jar package with Maven.

## Environment Preparations
Make sure that you have installed Java and Maven. For the Java version, please use JDK 8. You can download and install the JDK appropriate for your system through OpenJDK (Linux) or at `www.java.com`.

### Installing Maven

The specific installation instructions can be found at `https://maven.apache.org/install.html`. The following describes how to install it manually:
1. Download Maven's zip packageor tar.gz package.
2. Unzip the package to a desired directory, such as `C:\Maven` (Windows) or `/opt/mvn/apache-maven-3.5.0` (Linux).
3. Add the path of the `bin` directory in the unzipped directory to the system environment variable `PATH` in the following way as appropriate:
 - Linux: add through `export PATH=$PATH:/opt/mvn/apache-maven-3.5.0/bin`.
 - Windows: right click Computer and select `Properties > Advanced system settings > Advanced > Environment Variables`, select the `Path` variable, click Edit, and add `;C:\Maven\bin;` at the end of the variable value.
4. Run the following command on the command line to check whether Maven is installed correctly.
```
mvn -v
```
If the following is output, Maven is properly installed. If you have any questions, please see Maven's [official documentation](https://maven.apache.org/install.html).
```
Apache Maven 3.5.0 (ff8f5e7444045639af65f6095c62210b5713f426; 2017-04-04T03:39:06+08:00)
Maven home: C:\Program Files\Java\apache-maven-3.5.0\bin\..
Java version: 1.8.0_144, vendor: Oracle Corporation
Java home: C:\Program Files\Java\jdk1.8.0_144\jre
Default locale: zh_CN, platform encoding: GBK
OS name: "windows 7", version: "6.1", arch: "amd64", family: "windows"
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

### Prepare the compilation file
Create a `pom.xml` file in the root directory of the project folder and enter the following content:
```xml
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
```

#### Using Maven Central library to handle package dependencies
If you need to reference the external package of Maven Central, you can add dependencies as needed. The content of the `pom.xml` file is as follows:
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

## Compiling and Packaging
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
If a compilation failure is displayed, adjust the code based on the output compilation error message.
The compiled zip package is located in the `target` directory of the project folder and named `java-example-1.0-SNAPSHOT.jar` after the `artifactId` and version fields in pom.xml.

## Function Usage
After the jar package is generated after compilation and packaging, when creating or modifying a function, you can upload the package (if less than 10 MB) through the page or upload it (if bigger) to a COS bucket and then update it into the function through COS upload.

