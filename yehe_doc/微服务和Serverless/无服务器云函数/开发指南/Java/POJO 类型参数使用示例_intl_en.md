## Operation Scenarios
With POJO type parameters, you can handle more complex data structures than simple event input parameters. This document uses an example to describe how to use POJO parameters in SCF and which input parameter formats are supported.

## Prerequisites
You have logged in to the [SCF Console](https://console.cloud.tencent.com/scf/index?rid=1).

## Directions
### Event input parameters and POJOs 
The event input parameters used in this document are as follows:
```json
{
  "person": {"firstName":"bob","lastName":"zou"},
  "city": {"name":"shenzhen"}
}
```
With the input parameters above, the following content is outputted:
```json
{
  "greetings": "Hello bob zou.You are from shenzhen"
}
```
Based on the input parameters, the following four classes are built:
* RequestClass: used to accept the event as the class that accepts events
* PersonClass: used to handle the `person` section in the event JSON
* CityClass: used to handle the `city` section in the event JSON
* ResponseClass: used to assemble the response content

### Code preparations
Prepare the code by following the steps below for the four classes constructed based on the input parameters and entry function:

#### Project directory preparations
Create a project root directory, such as `scf_example`.

#### Code directory preparations
1. Create the folder `src\main\java` as the code directory in the project root directory.
2. According to the name of the package to be used, create a package folder in the code directory.
For example, create `example` to form the directory structure `scf_example\src\main\java\example`.

#### Code preparations
Create files `Pojo.java`, `RequestClass.java`, `PersonClass.java`, `CityClass.java`, and `ResponseClass.java` in the `example` folder with the following contents respectively:
* **Pojo.java**

```
package example;

public class Pojo{  
    public ResponseClass handle(RequestClass request){
        String greetingString = String.format("Hello %s %s.You are from %s", request.person.firstName, request.person.lastName, request.city.name);
        return new ResponseClass(greetingString);
    }
}
```

* **RequestClass.java**

```
package example;

public class RequestClass {
    PersonClass person;
    CityClass city;

    public PersonClass getPerson() {
        return person;
    }

    public void setPerson(PersonClass person) {
        this.person = person;
    }
    
    public CityClass getCity() {
        return city;
    }

    public void setCity(CityClass city) {
        this.city = city;
    }

    public RequestClass(PersonClass person, CityClass city) {
        this.person = person;
        this.city = city;
    }

    public RequestClass() {
    }
}
```

* **PersonClass.java**

```
package example;

public class PersonClass {
    String firstName;
    String lastName;

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public PersonClass(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }

    public PersonClass() {
    }
}
```

* **CityClass.java**

```
package example;

public class CityClass {
    String name;
    
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public CityClass(String name) {
        this.name = name;
    }

    public CityClass() {
    }
}
```

* **ResponseClass.java**

```
package example;

public class ResponseClass {
    String greetings;

    public String getGreetings() {
        return greetings;
    }

    public void setGreetings(String greetings) {
        this.greetings = greetings;
    }

    public ResponseClass(String greetings) {
        this.greetings = greetings;
    }

    public ResponseClass() {
    }
}
```

### Code compilation
>In the example, Maven is chosen to compile and package the code. You can choose another packaging method according to your own conditions.
>
1. Create the `pom.xml` function in the project root directory and enter the following content:
```
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
2. Run the `mvn package` command on the command line and make sure that there is a successful compilation message. If the output result is as follows, the packaging is successful:
```
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.800 s
[INFO] Finished at: 2017-08-25T15:42:41+08:00
[INFO] Final Memory: 18M/309M
[INFO] ------------------------------------------------------------------------
```
If the compilation fails, please modify the code as prompted.
3. The generated package after compilation is located at `target\java-example-1.0-SNAPSHOT.jar`.

### Function creation and testing
1. Create a function. For more information, please see [Creating and Updating Functions](https://intl.cloud.tencent.com/document/product/583/19806).
2. Upload the compiled package as a submission package.
You can choose to upload the packaging by zipping it or uploading it to a COS bucket and then submitting it through COS bucket upload.
3. Set the execution method of the function to `example.Pojo::handle`.
4. Expand the testing page by using the test button and enter the input parameters expected to be handled in the test template:
```json
{
  "person": {"firstName":"bob","lastName":"zou"},
  "city": {"name":"shenzhen"}
}
```
After clicking "Execute", you can see the return as shown below:
```
{
  "greetings": "Hello bob zou.You are from shenzhen"
}
```
You can also modify the values of the structures in the test input parameters, and you can see the modification effect after execution.

### Sample
You can go to the following address and pull the sample code for testing:
```
https://github.com/tencentyun/scf-demo-java
```
