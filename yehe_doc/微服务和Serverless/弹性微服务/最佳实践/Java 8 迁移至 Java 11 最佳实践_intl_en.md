Since the release of Java 9, Java has been improved and enhanced in many features with some modifications in APIs to improve startup, performance, and memory usage of your applications.

## Significant Improvements From Java 8 to Java 11

### Module system

The module system [JSR 376](http://openjdk.java.net/projects/jigsaw/spec/) is integrated to Java since Java 9 to solve problems such as disordered class paths, complex configuration, and ineffective encapsulation in large applications.

A module is a collection of Java classes, APIs, and relevant resources. It can customize the application runtime configuration. It uses a smaller space (which is very useful in the microservice architecture) and allows you to use [jlink](https://docs.oracle.com/en/java/javase/11/tools/jlink.html) to link an application to a custom runtime for deployment. JVM is faster to load a class from a module than to directly load it from a class path.

Modules help implement strong encapsulation by requiring explicit declaration of which packages a module exports and which components it requires, and by restricting reflective access. This level of encapsulation makes an application more secure and easier to maintain.

An application compiled with Java 8 can continue to use the class path and does not have to migrate to modules as a requisite for running on Java 11.

For more information on how the module system works, see [The State of the Module System](http://openjdk.java.net/projects/jigsaw/spec/sotms).

### JVM analysis and diagnosis tools

#### Java Flight Recorder and Java Mission Control

Java Flight Recorder (JFR) [JEP 328](http://openjdk.java.net/jeps/328) collects diagnosis and analysis data from running Java applications. It almost has no impact on running applications. You can use Mission Control (JMC) and other tools to analyze collected data. JFR and JMC are commercial features in Java 8 but open-source in Java 11.

#### JVM log system

Java 11 has a common logging system [JEP 158](http://openjdk.java.net/jeps/158) for all components of the JVM. This unified logging system allows you to define what components to log, and to what level. This fine-grained logging is useful for performing root-cause analysis on JVM crashes and for diagnosing performance issues in a production environment.

#### Low-overhead heap profiling

A new API has been added to the Java Virtual Machine Tool Interface (JVMTI) for sampling Java heap allocations ([JEP 331](http://openjdk.java.net/jeps/331). The sampling features low overheads.

### Garbage collection

The following garbage collectors are available in Java 11: Serial, Parallel, Garbage-First (G1), and Epsilon. The default garbage collector in Java 11 is G1.

- The aim of G1 is to strike a balance between latency and throughput. It is designed to avoid full collections, but when the concurrent collections can't reclaim memory fast enough, a full GC will occur.
- The Parallel garbage collector is the default collector in Java 8. It is a throughput collector that uses multiple threads to speed up garbage collection.
- The Epsilon garbage collector handles allocations but does not reclaim any memory. When the heap is exhausted, the JVM will shut down. It is useful for short-lived services and for applications that are known to be garbage-free.

In addition, Java 11 provides other three garbage collectors:

- ZGC is a concurrent and low-latency collector that attempts to keep pause times under 10 milliseconds. It is available as an experimental feature in Java 11.
- Shenandoah is a low-pause collector that reduces GC pause times by performing more garbage collection concurrently with the running Java program. It is an experimental feature in Java 12, but there are backports to Java 11.
- CMS is available in Java 11 but has been deprecated since Java 9.

### Improvements on the container environment

Prior to Java 10, memory and CPU constraints set on a container were not recognized by the JVM. In Java 8, for example, the JVM will default the maximum heap size to 1/4 of the physical memory of the underlying host. Starting with Java 10, the JVM uses constraints set by container control groups (cgroups) to set memory and CPU limits. For example, the default maximum heap size is 1/4 of the container's memory limit.

New JVM parameters were also added to Java 10 to give Docker container users fine-grained control over the amount of system memory that will be used for the Java heap.

>?Most of the cgroup enablement work was backported to Java 8 as of JDK 8u191.

## Migration from Java 8 to Java 11

There's no one-size-fits-all solution to migrate applications from Java 8 to Java 11. Potential issues include removed APIs, deprecated packages, use of internal APIs, changes to class loaders, and changes to garbage collectors.

### Trying directly compiling and running the application

In general, the simplest method is to try running the application compiled with Java 8 on Java 11 without recompiling, or to compile with JDK 11 first. If the goal is to get an application up and running as quickly as possible, just trying running on Java 11 is often the best method.

### Other tools

Java 11 has two tools, jdeprscan and jdeps, which are useful for sniffing out potential issues. These tools can be run against existing class or JAR files. You can assess the migration effort without having to recompile.

#### jdeprscan

[jdeprscan](https://docs.oracle.com/en/java/javase/11/tools/jdeprscan.html) looks for use of deprecated or removed APIs. Use of deprecated APIs is not a blocking issue, but is something to look into, as such APIs may be removed in later versions.

The easiest way to use [jdeprscan](https://docs.oracle.com/en/java/javase/11/tools/jdeprscan.html) is to give it a JAR file from an existing build. You can also give it a directory, such as the compiler output directory, or an individual class name. Use the `--release 11` parameter to get the most complete list of deprecated APIs; for example, you can run `jdeprscan --release 11 my-application.jar`.

If an `error: cannot find class XXX` error occurs, you need to check whether the dependent class file exists in the class path of the JAR file. If the dependent class is not a third-party dependency, you may use an API removed in Java 11.

You can run `jdeprscan --release 11 --list` to get an understanding of what APIs have been deprecated since Java 8. To get the list of APIs that have been removed, run `jdeprscan --release 11 --list --for-removal`.

#### jdeps

[jdeps](https://docs.oracle.com/en/java/javase/11/tools/jdeps.html) is a Java class dependency analyzer. When used with the `--jdk-internals` parameter, jdeps tells you which class depends on which internal APIs. We recommend you add the `--multi-release 11` parameter to support multi-version build JAR files; for example, you can run `jdeps --jdk-internals --multi-release 11 --class-path log4j-core-2.13.0.jar my-application.jar`.

You can continue to use internal APIs in Java 11, but replacing the usage should be a priority. The OpenJDK wiki page [Java Dependency Analysis Tool](https://wiki.openjdk.java.net/display/JDK8/Java+Dependency+Analysis+Tool) has recommended replacements for some commonly used JDK internal APIs.

Try to eliminate the use of any API coming from the module `jdk.unsupported`. Even though your code may use JDK internal APIs, it will continue to run, for a while at least. Do take a look at [JEP 260](http://openjdk.java.net/jeps/260) since it does point to replacements for some internal APIs.

There are jdeps and jdeprscan plugins for both Gradle and Maven. We recommend you add these tools to your build scripts.

| Tool      | Gradle Plugin                                                  | Maven Plugin                                                   |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| jdeps     | [jdeps-gradle-plugin](https://github.com/kordamp/jdeps-gradle-plugin) | [Apache Maven JDeps Plugin](https://maven.apache.org/plugins/maven-jdeps-plugin/index.html) |
| jdeprscan | [jdeprscan-gradle-plugin](https://github.com/kordamp/jdeprscan-gradle-plugin) | [Apache Maven JDeprScan Plugin](https://maven.apache.org/plugins/maven-jdeprscan-plugin/index.html) |

What jdeprscan and jdeps cannot do is warn about the use of reflection to access encapsulated APIs. You need to check for reflective access in your code at runtime.

### Check at runtime

#### Checking JVM parameters

Check JVM parameters before running your application on Java 11. Using a removed JVM parameter will cause JVM to crash (`Error: Could not create the Java Virtual Machine`). If you enable GC logs, parameter check is especially important, as GC logs have changed drastically from Java 8. You can use JaCoLine to check JVM parameters.

#### Checking third-party dependent class libraries

You need to update all your third-party dependent class libraries to versions supporting Java 11. The OpenJDK Quality Group maintains a [Quality Outreach](https://wiki.openjdk.java.net/display/quality/Quality+Outreach) wiki page that lists the status of testing of many Free Open Source Software (FOSS) projects against versions of OpenJDK.

#### Checking garbage collection parameters

The Parallel garbage collector is the default collector in Java 8. Starting from Java 9, the default garbage collector has been changed to G1. You need to check whether your garbage collection parameters are correct.

#### Notes on class loaders

- The class loader hierarchy has changed in Java 11. `SystemClassloader` (also known as `AppClassloader`) is now an internal class. Casting to a `URLClassLoader` will report a `ClassCastException` at runtime. Java 11 does not have APIs to dynamically augment the `classpath` at runtime but it can be done through reflection.
- In Java 11, `BootstrapClassloader` only loads core modules. If you create a class loader with a null parent, it may not find all platform classes. In Java 11, you need to pass in `ClassLoader.getPlatformClassLoader()` instead of `null` as the parent class loader in such cases.

#### Locale data changes

The default source for locale data in Java 11 was changed with [JEP 252](http://openjdk.java.net/jeps/252) to the Unicode Consortium's Common Locale Data Repository. This may have an impact on localized formatting. Set the system property `java.locale.providers=COMPAT,SPI` to revert to the Java 8 locale behavior, if necessary.

### Common issues

#### Unrecognized options

If a JVM parameter has been removed, the application will print `Unrecognized option:` or `Unrecognized VM option`. An unrecognized parameter will cause the JVM to exit (`Error: Could not create the Java Virtual Machine`). Options that have been deprecated, but not removed, will produce a JVM warning (`VM Warning: Option <option> was deprecated`).

In general, such unrecognized JVM parameters need to be removed. The exception is parameters for garbage collection logging. GC logging was reimplemented in [JEP 271](http://openjdk.java.net/jeps/271). Refer to [Enable Logging with the JVM Unified Logging Framework](https://docs.oracle.com/en/java/javase/11/tools/java.html#GUID-BE93ABDC-999C-4CB5-A88B-1994AAAC74D5) to configure parameters.

#### WARNING: An illegal reflective access operation has occurred

When Java code uses reflection to access a JDK internal API, the runtime will issue an illegal reflective access warning.

#### java.lang.reflect.InaccessibleObjectException

This exception indicates that you are trying to call `setAccessible(true)` on a field or method of an encapsulated class/module. Use the `--add-opens` parameter to give your code access to the non-public members of a package/module.

#### java.lang.NoClassDefFoundError

If the application runs on Java 8 but reports a `java.lang.NoClassDefFoundError` or `java.lang.ClassNotFoundException` error on Java 11, then it is likely that the application is using a package from the Java EE or CORBA modules. These modules were deprecated in Java 9 and removed in Java 11. For more information, see [JEP 320: Remove the Java EE and CORBA Modules](https://openjdk.java.net/jeps/320).

To resolve the issue, add a runtime dependency to your project.

| Removed Module | Affected Package             | Suggested Dependency                                                   |
| -------- | ---------------------- | ------------------------------------------------------------ |
| JAX-WS   | java.xml.ws            | [JAX WS RI Runtime](https://mvnrepository.com/artifact/com.sun.xml.ws/jaxws-rt) |
| JAXB     | java.xml.bind          | [JAXB Runtime](https://mvnrepository.com/artifact/org.glassfish.jaxb/jaxb-runtime) |
| JAV      | java.activation        | [JavaBeans (TM) Activation Framework](https://mvnrepository.com/artifact/javax.activation/activation) |
| Common Annotations     | java.xml.ws.annotation | [Javax Annotation API](https://mvnrepository.com/artifact/javax.annotation/javax.annotation-api) |
| CORBA    | java.corba             | [GlassFish CORBA ORB](https://mvnrepository.com/artifact/org.glassfish.corba/glassfish-corba-orb) |
| JTA      | java.transaction       | [Java Transaction API](https://mvnrepository.com/artifact/javax.transaction/jta) |

#### UnsupportedClassVersionError

This exception means that you are trying to run code that was compiled with a later version of Java on an earlier version of Java. For example, you are running on Java 11 with a JAR that was compiled with JDK 13.

| Java Version | Class File Format Version |
| -------- | ---------- |
| 8        | 52         |
| 9        | 53         |
| 10       | 54         |
| 11       | 55         |
| 12       | 56         |
| 13       | 57         |
