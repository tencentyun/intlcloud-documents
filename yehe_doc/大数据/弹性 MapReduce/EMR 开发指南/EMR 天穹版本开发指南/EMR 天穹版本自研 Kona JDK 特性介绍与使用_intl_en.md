## Garbage Collection (GC) Optimized Work Stealing Threads (OWST)
### How to enable
Enabled by default. You can disable it by adding `-XX:-UseOWSTTaskTerminator` to the startup parameters.

### How it works
Parallel GC threads use work stealing for load balancing to reduce GC pause time. In the original work stealing algorithm, all idle GC threads frequently try work stealing, resulting in the waste of CPU resources. The OWST algorithm uses a master thread to check for work to steal and wake up other idle GC threads at the right moment, which greatly reduces the waste of CPU resources and the competition for CPU resources between processes. OWST is available in OpenJDK community version 12 or later. According to HiBench testing, Kona JDK performance can be improved by 30% max and 8% on average.

## Concurrent Mark Sweep (CMS) Full GC Parallelization
### How to enable
Set the `-XX:+CMSParallelFullGC` parameter to `false` in the startup parameters.

### How it works
CMS full GC is considered as single-threaded full-shutdown GC where all nodes are shut down with a long downtime. When the 20 GB heap uses the CMS algorithm, the downtime may be about 50 seconds once a full GC is triggered. With the full GC parallelization feature of EMR-TianQiong-V1.0.0, GC can be run in multiple threads in some stages, reducing the downtime of full GC by up to 40% and improving the worst-case performance of the system.

## Optimized Physical Memory Release
### How to enable
- Add `-XX:+FreeHeapPhysicalMemory` to the startup parameters. For PS, CMS, and G1 algorithms, when a full GC is triggered (G1 algorithm triggers a concurrent cycle and full GC), the Java Virtual Machine (JVM) will call `madvise` to release the physical memory corresponding to the virtual address space of the second half of the old region that does not contain objects after finishing memory defragmentation.
- With the above parameter enabled, if you specify `-XX:PeriodicGCInterval=x` in the startup parameters, the JVM will automatically determine the load of the current process every five minutes. If the load is lower than the 99th percentile for three consecutive times, a full GC will be triggered to reclaim the physical memory. Full GC can be triggered only once within the `PeriodicGCInterval` (unit: ms). The default value of `PeriodicGCInterval` is `0`.
- The features corresponding to the above two parameters are disabled by default.

## Default Class Data Sharing (CDS) Archive
The default CDS archive feature of Tencent Kona is enabled by default. You can disable this feature via the following startup flag:
```
java -Xshare:off
```

## Supporting Chinese Cryptographic Algorithms
### How to use
The APIs of Chinese cryptographic algorithms in Kona JDK conform to the JCE CipherAPI standard. Users using Kona JDK can use Chinese cryptographic algorithms seamlessly.


### How it works
- Chinese cryptographic algorithms are a series of algorithms formulated by the State Cryptography Administration of China, including symmetric cryptographic algorithms, asymmetric elliptic curve cryptographic algorithms, and hashing algorithms, for example, SM1, SM2, and SM3.
- To make Kona JDK easier to use and lower the requirements for converting cryptographic algorithms to Chinese cryptographic algorithms for existing businesses, Kona JDK and TencentSM together introduce Chinese cryptographic algorithms into the JDK library. Kona JDK Chinese cryptographic algorithms comply with the JCE standard and have defined SMCSProvider to provide APIs.

## Java Flight Recorder (JFR)
### JFR overview
JFR is a tool that collects the diagnostic and performance data about a running Java application. Its backend APIs come from OpenJDK11. Theoretically, the JFR performance overhead is less than 2% when default settings are used. Therefore, it can be used to collect data in the production environment.

### Directions for usage
#### Starting JFR
```
//JFR is disabled by default. You can start JFR by adding the `-XX:+FlightRecorder` parameter to the application startup command.
$JAVA_HOME/bin/java -XX:+FlightRecorder YourApplication
```
#### Starting a recording with JFR
```
//You need to get the `pid` of `YourApplication` first, and run the `jcmd pid JFR.start` command to start a recording. When the Java application stops normally, the running data will be automatically recorded in the file specified by the `filename` parameter.
$JAVA_HOME/bin/jcmd <your_pid> JFR.start name=anyname_for_dump filename=anyname_for_your_record.jfr
 
The available parameters are as follows:
    name=name
    Name of a recording
    
    defaultrecording=true/false
    Whether to start recording events upon initialization. The default value is `false`. For response analysis, it should be set to `true`.
    
    settings=path
    Path of JFR configuration file
    
    delay=time
    Delay before starting recording
    
    duration=time
    Duration of recording
    
    filename=path
    File path to save the recorded events
    
    compress=true/false
    Whether to compress the recorded data using Gzip. The default value is `false`.
    
    maxage=time
    Maximum time to save recorded data in circular buffers
     
    maxsize=size
    Maximum space occupied by circular buffers
```

#### Exporting recordings

```
//After running the `JFR.start` command, you can run the `jcmd JFR.dump` command to export the recordings up to now. You can specify the location where the data will be exported to via `filename`. Please note that the `name` must be the same as the `name` specified in `JFR.start`.
$JAVA_HOME/bin/jcmd <your_pid> JFR.dump name=anyname_for_your_record filename=anyname_for_dump_record.jfr
 
 
The available parameters are as follows:
    name=name
    Event recording name for exported data
    
    recording=n
    JFR event recording number
    
    filename=path
    Path to export the file
```

#### Stopping a recording

```
//Stop a recording (note that if this stop does not carry the `name` and `filename` parameters as shown below, dump will not be executed and the recording will be stopped directly).
$JAVA_HOME/bin/jcmd <your_pid> JFR.stop name=anyname_for_your_record filename=anyname_for_dump_record.jfr
 
The available parameters are as follows:
    name=name
    The name of the event recording to be stopped
    
    recording=n
    The number of the event recording to be stopped
    
    discard=Boolean
    If the value is `true`, previously saved data will be discarded.
    
    filename=path
    File path to save data
```

#### Viewing all running event recordings

```
//There can be multiple JFR event recordings concurrently running under a process. You can view all the running event recordings via the following command:
$JAVA_HOME/bin/jcmd <your_pid> JFR.check 
```

 
