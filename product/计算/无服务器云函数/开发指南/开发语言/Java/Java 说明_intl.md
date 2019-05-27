SCF provides a Java 8 runtime environment.

As the Java language can be executed in JVM only after compilation, it is used in SCF in a different way from scripting languages such as Python and Node.js, with the following restrictions:

* Code upload is not supported: When Java is used, only developed, compiled, and packaged zip/jar packages can be uploaded. The SCF environment does not provide Java compiling capability.
* Online editing is not supported: Since code cannot be uploaded, online editing of code is not supported. The code page of a Java runtime function only lists the ways to upload the code through the page or submit the code through COS.

## Code Form

The code form of a SCF function developed in Java is generally as follows:
```java
package example;

public class Hello {
    public String mainHandler(String name) {
        System.out.println("Hello world!");
        return String.format("Hello %s.", name);
    }
}
```

## Execution Method

As Java has the concept of package, its execution method is different from other languages and requires package information. The corresponding execution method in the code example is `example.Hello::mainHandler`, where `example` is identified as the Java package, `Hello` the class, and `mainHandler` the class method.

## Deployment Package Upload

You can [create a zip deployment package using Gradle](https://cloud.tencent.com/document/product/583/12216) or [create a jar deployment package using Maven](https://cloud.tencent.com/document/product/583/12217). Then you can upload the created package (if less than 10 MB) directly in the SCF console, or upload it to the COS bucket and then specify its bucket and object information in the SCF console.

## Input Parameters and Returns

In the code example, the input parameters used by mainHandler contain two types, i.e., String and Context, and the return uses the String type. The former type of the input parameters identifies the event input parameter, while the latter the function runtime information. Currently, types supported for event input parameters and function returns include Java base types and POJO type; the function runtime is currently `com.qcloud.scf.runtime.Context` type, and its associated library files can be downloaded [here](https://mc.qcloudimg.com/static/archive/12ec94d2852a4cfbdb066e0b99b39070/com.qcloud.scf.runtime.Context.1.0.jar.zip).

* Types supported for event input and return parameters
	* Java base types, including eight basic types and wrapper classes (byte, int, short, long, float, double, char, and boolen) and String type.
	* POJO (Plain Old Java Object) type. You should use variable POJOs and public getters and setters to provide implementations of the corresponding types in the code.

* Context input parameters
	* To use Context, you need to use `com.qcloud.scf.runtime.Context;` in the code to reference the package and bring the jar package when it is packaged.
	* If this object is not used, you can ignore it in the function input parameters, which can be written as `public String mainHandler(String name)`.


## Log

You can use the following statements in the program to output the log:

```java
System.out.println("Hello world!");
```

The output can be viewed at the `log` location in the function log.

## Testing

You can click the test button on the console page to open the testing interface, trigger a function in real time, and view the execution result. For the sample code, since the input parameters are `String name` string type, you need to enter the string content such as `"Tencent Cloud"` when you trigger and execute it in the testing interface.

If you modify the sample code and expect to receive JSON input parameters in a more complex format, you can use [POJO type parameters](https://cloud.tencent.com/document/product/583/12215) to define the corresponding data structures in the code. When the SCF platform passes the corresponding JSON parameters to the entry function, it converts them into an object instance, which can be used directly by the code.



