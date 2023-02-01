## Code Form

The code form of a SCF function developed in Java is generally as follows:

```java
package example;

public class Hello {
    public String mainHandler(KeyValueClass kv) {
        System.out.println("Hello world!");
        System.out.println(String.format("key1 = %s", kv.getKey1()));
        System.out.println(String.format("key2 = %s", kv.getKey2()));
        return String.format("Hello World");
    }
}
```

Create the parameter `KeyValueClass` class:

```java
package example;
public class KeyValueClass {
    String key1;
    String key2;
    
    public String getKey1() {
        return this.key1;
    }   
    public void setKey1(String key1) {
        this.key1 = key1;
    }   
    public String getKey2() {
        return this.key2;
    }   
    public void setKey2(String key2) {
        this.key2 = key2;
    }   
    
    public KeyValueClass() {
    }   
}
```

## Execution Method

As Java has the concept of package, its execution method is different from other languages and requires package information. The corresponding execution method in the code example is `example.Hello::mainHandler`, where `example` is identified as the Java package, `Hello` the class, and `mainHandler` the class method.

## Input Parameters and Returns

In the sample code, the input parameters used by `mainHandler` are of POJO type, and the response is of string type. Currently, types supported for event input parameters and function responses include Java base types and POJO type, the function runtime is of `com.qcloud.scf.runtime.Context` type, and its associated library files can be downloaded [here](https://search.maven.org/artifact/com.tencentcloudapi/scf-java-events/0.0.2/jar).


#### Types supported for event input and response parameters 

| Event Input Parameter | Response Parameter Type |
|---------|---------|
| Java base types | These include eight basic types and wrapper classes (`byte`, `int`, `short`, `long`, `float`, `double`, `char`, and `boolen`) and `String` type.   |
| POJO (Plain Old Java Object) type | You should use variable POJOs and public getters and setters to provide implementations of the corresponding types in the code. |



#### Context input parameters 
  * To use Context, you need to use `com.qcloud.scf.runtime.Context;` in the code to reference the package and bring the jar package when it is packaged.
  * If this object is not used, you can ignore it in the function input parameters, which can be written as `public String mainHandler(String name)`.

>! The event structures of input parameters passed in by certain triggers have been defined and can be used directly. You can get and use the Java libraries through the [Cloud Event Definition](https://github.com/tencentyun/scf-java-libs). If you have any questions during use, you can submit an [issue](https://github.com/tencentyun/scf-java-libs/issues/new) or [ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.
