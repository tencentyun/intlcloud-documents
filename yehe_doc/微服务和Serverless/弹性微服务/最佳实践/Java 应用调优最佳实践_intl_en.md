## Optimizing Container Image

By optimizing the container image in the following ways, you can reduce the loading and startup time:

- Minimize the container image size.
- Avoid using nested JAR packages.
- Use TEM JAR/WAR for deployment.

Deployment based on TEM JAR/WAR is easy to use and efficient. It provides best practices for JAR package image builds by default. TEM offers a build process that can fully utilize the build cache by default and uses the new-gen build tool BuildKit to increase the build speed by over 50%. Moreover, build logs can be queried to make the entire build process traceable.

## Setting Application Acceleration

If you use TEM JAR/WAR for deployment and select the KONA JDK 11/Open JDK 11 runtime environment, TEM will enable the application acceleration feature and support zero-code modification acceleration for Spring Boot applications by default. TEM enhances the AppCDS feature in OpenJDK, so you don't need to modify the nested JAR package structure in the original Spring Boot application, and TEM directly provides best practices of Java application acceleration to shorten the startup time by 10%–40% during instance scale-out.

## JVM Parameter Optimization

### Using JDK that can perceive container memory resources

On a VM or physical machine, when allocating CPU and memory resources, JVM will search for available resources from common locations such as `/proc/cpuinfo` and `/proc/meminfo` on Linux. However, at the container runtime, the CPU and memory restrictions are stored in `/proc/cgroups/...`. JDK on an early version will still search for resources in `/proc` but not `/proc/cgroups`, which may cause the CPU and memory usage to exceed the allocated upper limit and further lead to more severe problems:

- There are too many threads, as the size of the thread pool is configured by `Runtime.availableProcessors()`.
- The memory used by JVM exceeds the upper limit of the container memory and causes the `OOMKilled` error in the container.

JDK 8u131 first implements the `UseCGroupMemoryLimitForHeap` parameter, but this parameter has a defect. After the `UnlockExperimentalVMOptions` and `UseCGroupMemoryLimitForHeap` parameters are added to your application, JVM can perceive the container memory and control the actual heap size of the application, but JVM still cannot fully utilize the memory allocated to the container.

Therefore, JVM provides the `-XX:MaxRAMFraction` flag to help better calculate the heap size. The default value of `MaxRAMFraction` is `4` (that is, `4` is the divisor), but it is a fraction, not a percentage; therefore, it is difficult to set a value that can use available memory effectively.

JDK 10 provides better support for the container environment. If you run a Java application in a Linux container, JVM will use the `UseContainerSupport` option to automatically check the memory limits and use `InitialRAMPercentage`, `MaxRAMPercentage`, and `MinRAMPercentage` to control the memory. Here, percentages rather than fractions are used to make the control more accurate.

By default, the `UseContainerSupport` parameter is activated, `MaxRAMPercentage` is 25%, and `MinRAMPercentage` is 50%.

Note that `MinRAMPercentage` here is not used to set the minimum value of the heap size but to restrict the heap size by JVM only when the total available memory of the physical server (or container) is less than 250 MB.

Similarly, `MaxRAMPercentage` here is used to restrict the heap size by JVM only when the total available memory of the physical server (or container) exceeds 250 MB.

These parameters have been backported to JDK 8u191. By default, `UseContainerSupport ` is activated. You can set `-XX:InitialRAMPercentage=50.0 -XX:MaxRAMPercentage=80.0` to enable JVM to perceive and fully utilize the available memory of the container. Note that if `-Xms -Xmx` is specified, `InitialRAMPercentage` and `MaxRAMPercentage` will become invalid.

### Disabling the optimization compiler

By default, JVM has multi-stage JIT compilation. Though such stages can gradually improve the application efficiency, they also increase the memory overheads and the application startup time.

For short-lived cloud native applications, you can consider using the following parameters to disable the optimization stage, so as to reduce the startup time at the cost of the long-term running efficiency.
<dx-codeblock>
:::  JAVA
JAVA_TOOL_OPTIONS="-XX:+TieredCompilation -XX:TieredStopAtLevel=1"
:::
</dx-codeblock>


### Disabling class verification

When JVM loads a class to the memory for execution, it will verify whether the class is not tampered with, modified maliciously, or corrupted. However, in a cloud native environment, the CI/CD pipeline is provided by the cloud native platform, which means that the application compilation and deployment are trusted. Therefore, you need to consider using the following parameters to disable verification. If many classes need to be loaded during startup, disabling verification may accelerate the startup.
<dx-codeblock>
:::  JAVA
JAVA_TOOL_OPTIONS="-noverify"
:::
</dx-codeblock>



### Reducing the thread size

Most Java web applications use the one-thread-per-connection model, where each Java thread will consume the memory of the local server rather than the heap memory (this is called thread stack), and each thread is 1 MB in size by default. If your application processes 100 concurrent requests, it may have at least 100 threads, which means that it uses 100 MB thread stack space. The memory is not counted as the heap size, and you can use the following parameter to reduce the thread stack size:
<dx-codeblock>
:::  JAVA
JAVA_TOOL_OPTIONS="-Xss256k"
:::
</dx-codeblock>


Note that if you reduce the size too much, `java.lang.StackOverflowError` will occur. You can analyze the application to find the optimal thread stack size to be configured.

## Optimizing a Spring Boot Application

### Using Spring Boot 2.2 or later

Staring from v2.2, Spring Boot has significantly increased the startup speed. However, if you use an earlier version, consider upgrading the version or [making optimizations manually](https://spring.io/blog/2018/12/12/how-fast-is-spring).

### Using delayed initialization

On Spring Boot 2.2 or later, you can enable global delayed initialization to increase the startup speed at the cost of lengthening the delay of the first request, as you need to wait for the first initialization of the component.
You can enable delayed initialization in `application.properties`:
<dx-codeblock>
:::  javascript
spring.main.lazy-initialization=true
:::
</dx-codeblock>
Alternatively, you can use the following environment variable:
<dx-codeblock>
:::  javascript
SPRING_MAIN_LAZY_INITIALIZATIION=true
:::
</dx-codeblock>
