The WordCount application is a great example that gives you a hands-on experience in developing your first Hadoop MapReduce application. In this tutorial, you will learn how to implement WordCount example code in MapReduce to count the number of occurrences of a given word in the input file stored in HDFS or in COS. The program is the same as the one shown in the Hadoop community.

## 1. Development Preparations
- This task requires access to COS, so you need to [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309) in COS first.
- Create an EMR cluster. When creating the EMR cluster, you need to select a cluster type that includes HDFS and enable access to COS on the basic configuration page.

## 2. Logging in to an EMR Server
Log in to any node (preferably a master node) in the EMR cluster before performing relevant operations. EMR is built on CVM instances running on Linux; therefore, using EMR in command line mode requires logging in to an CVM instance.

After creating the EMR cluster, select **Elastic MapReduce** in the console, click the ID/name of the cluster you just created in the cluster list, click **Cluster Resource** > **Resource Management** > **Master**, and click the resource ID of an active master node to enter the CVM console and find the CVM instance of the EMR cluster.

For information about how to log in to a CVM instance, see [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can use WebShell to log in. Click **Login** on the right of the desired CVM instance to go to the login page. The default username is `root`, and the password is the one you set when creating the EMR cluster.

Once your credentials are validated, you can enter the EMR command line interface. All Hadoop operations should be performed under the `Hadoop` user. The `root` user is logged in by default when you log in to the EMR node, so you need to switch to the `Hadoop` user. Run the following command to switch users and go to the `Hadoop` folder:
```
[root@172 ~]# su hadoop
[hadoop@172 root]$ cd /usr/local/service/hadoop
[hadoop@172 hadoop]$
```

## 3. Data Preparations
Prepare an input text file. You can either **store data in an HDFS cluster** or **store data in COS**. 

First, create a .txt file named `test.txt` locally and add the following sentences to the file:
```
Hello World.
this is a message.
this is another message.
Hello world, how are you?
```

Use scp or sftp service to upload a local file to the CVM instance in your EMR cluster. Run the following command in your local shell:
```
scp $localfile root@public IP address:$remotefolder
```
Here, $localfile is the path and the name of your local file; root is the CVM instance username. You can look up the public IP address in the node information in the EMR or CVM Console; and $remotefolder is the path where you want to store the file in the CVM instance.

After the upload is completed, you can check whether the file is in the corresponding folder on the command line of the EMR cluster. The file is uploaded to the `/usr/local/service/hadoop` path in the EMR cluster in this example.
```
[hadoop@172 hadoop]$ ls –l
```

### Storing Data in HDFS
After uploading the data to the CVM instance, you can copy the data file to the Hadoop cluster by running the following command:
```
[hadoop@172 hadoop]$ hadoop fs -put /usr/local/service/hadoop/test.txt /user/hadoop/
```
After the copy is completed, run the following command to view the copied file:
```
[hadoop@172 hadoop]$ hadoop fs -ls /user/hadoop
Output:
-rw-r--r-- 3 hadoop supergroup 85 2018-07-06 11:18 /user/hadoop/test.txt
```
If there is no `/user/hadoop` folder in Hadoop, you can create it on your own by running the following command:
```
[hadoop@172 hadoop]$ hadoop fs –mkdir /user/hadoop
```
For more Hadoop commands, see [HDFS Common Operations](https://intl.cloud.tencent.com/document/product/1026/31124).

### Storing Data in COS
There are two ways to store data in COS: **uploading via the COS console from the local storage** and **uploading via a Hadoop command**.
- When [uploading via the COS console from the local storage](https://intl.cloud.tencent.com/document/product/436/13321), you can view the uploaded data file by running the following command:
```
[hadoop@10 hadoop]$ hadoop fs -ls cosn://$bucketname/ test.txt
-rw-rw-rw- 1 hadoop hadoop 1366 2017-03-15 19:09 cosn://$bucketname/test.txt
```
Replace `$bucketname` with the name and path of your bucket.
- To upload via Hadoop command, run the following command:
```
[hadoop@10 hadoop]$ hadoop fs -put test.txt cosn://$bucketname /
[hadoop@10 hadoop]$ hadoop fs -ls cosn:// $bucketname / test.txt
-rw-rw-rw- 1 hadoop hadoop 1366 2017-03-15 19:09 cosn://$bucketname / test.txt
```

## 4. Creating a Project with Maven
Maven is recommended for project management. It can help you manage project dependencies with ease. Specifically, it can get .jar packages through the configuration of the `pom.xml` file, eliminating the need to add them manually.

Download and install Maven first and then configure its environment variables. If you are using the IDE, please set the Maven-related configuration items in the IDE.

### Creating a Maven Project
Enter the directory of the Maven project, such as `D://mavenWorkplace`, and create the project using the following commands:
```
mvn     archetype:generate     -DgroupId=$yourgroupID     -DartifactId=$yourartifactID 
-DarchetypeArtifactId=maven-archetype-quickstart
```
Here, `$yourgroupID` is your package name, `$yourartifactID` is your project name, and `maven-archetype-quickstart` indicates to create a Maven Java project. Some files need to be downloaded during the project creation, so please keep the network connected.

After successfully creating the project, you will see a folder named `$yourartifactID` in the `D://mavenWorkplace` directory. Files in the folder have the following structure:
```
simple
　　　---pom.xml　　　　Core configuration, under the project root directory
　　　---src
　　　　　---main　　　　　　
　　　　　　　---java　　　　  Java source code directory
　　      　---resources　  Java configuration file directory
　　　　---test
　　　　　　---java　　　　  Test source code directory
　　　　　　---resources　  Test configuration directory
```
We need to pay attention to the pom.xml file and the Java folder under the main directory, as the former is primarily used for dependency and packaging configuration, and the latter for source code storage.

First, add the Maven dependencies to pom.xml:
```
<dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-common</artifactId>
            <version>2.7.3</version>
        </dependency>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-mapreduce-client-core</artifactId>
            <version>2.7.3</version>
        </dependency>
</dependencies>
```
Then, add the packaging and compiling plugins to pom.xml:
```
<build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                    <encoding>utf-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <artifactId>maven-assembly-plugin</artifactId>
                <configuration>
                    <descriptorRefs>
                        <descriptorRef>jar-with-dependencies</descriptorRef>
                    </descriptorRefs>
                </configuration>
                <executions>
                    <execution>
                        <id>make-assembly</id>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
</build>
```
Right-click in src>main>java and create a Java Class. Enter the Class name (e.g., WordCount here) and add the sample code to the Class:
```
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

import java.io.IOException;
import java.util.StringTokenizer;

/**
 * Created by tencent on 2018/7/6.
 */
public class WordCount {
    public static class TokenizerMapper
            extends Mapper<Object, Text, Text, IntWritable>
    {
        private static final IntWritable one = new IntWritable(1);
        private Text word = new Text();

        public void map(Object key, Text value, Mapper<Object, Text, Text, IntWritable>.Context context)
                throws IOException, InterruptedException
        {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens())
            {
                this.word.set(itr.nextToken());
                context.write(this.word, one);
            }
        }
    }

    public static class IntSumReducer
            extends Reducer<Text, IntWritable, Text, IntWritable>
    {
        private IntWritable result = new IntWritable();

        public void reduce(Text key, Iterable<IntWritable> values, Reducer<Text, IntWritable, Text, IntWritable>.Context context)
                throws IOException, InterruptedException
        {
            int sum = 0;
            for (IntWritable val : values) {
                sum += val.get();
            }
            this.result.set(sum);
            context.write(key, this.result);
        }
    }

    public static void main(String[] args)
            throws Exception
    {
        Configuration conf = new Configuration();
        String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
        if (otherArgs.length < 2)
        {
            System.err.println("Usage: wordcount <in> [<in>...] <out>");
            System.exit(2);
        }
        Job job = Job.getInstance(conf, "word count");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(TokenizerMapper.class);
        job.setCombinerClass(IntSumReducer.class);
        job.setReducerClass(IntSumReducer.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        for (int i = 0; i < otherArgs.length - 1; i++) {
            FileInputFormat.addInputPath(job, new Path(otherArgs[i]));
        }
        FileOutputFormat.setOutputPath(job, new Path(otherArgs[(otherArgs.length - 1)]));

        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```
As you can see, there is a Map function and a Reduce function.

If your Maven is configured correctly and its dependencies are successfully imported, the project can be compiled directly. Enter the project directory in the local shell, and run the following command to package the entire project:
```
mvn package
```
Some files may need to be downloaded during the running process. "Build success" indicates that package is successfully created. You can see the generated .jar package in the target folder under the project directory.

Upload the packaged project file to the CVM instance of the EMR cluster using the scp or sftp service. Run the following command in the local shell:
```
scp $jarpackage root@public IP address: /usr/local/service/hadoop
```
Here, `$jarpackage` is the path plus name of your local .jar package; `root` is the CVM instance username; and the public IP address can be viewed in the node information in the EMR console or the CVM console. The file is uploaded to the `/usr/local/service/hadoop` folder of the EMR cluster.

### Counting a Text File in HDFS
Go to the `/usr/local/service/hadoop` directory as described in data preparations, and submit the task by running the following command:
```
[hadoop@10 hadoop]$ bin/hadoop jar 
/usr/local/service/hadoop/WordCount-1.0-SNAPSHOT-jar-with-dependencies.jar
WordCount /user/hadoop/test.txt /user/hadoop/WordCount_output
```
>!Above is a complete command, where `/user/hadoop/ test.txt` is the input file and `/user/hadoop/ WordCount_output` is the output folder. You should not create the `WordCount_output` folder before the command is submitted; otherwise, the submission will fail.

After the execution is completed, view the output file by running the following command:

```
[hadoop@172 hadoop]$ hadoop fs -ls /user/hadoop/WordCount_output
Found 2 items
-rw-r--r-- 3 hadoop supergroup 0 2018-07-06 11:35 /user/hadoop/MEWordCount_output/_SUCCESS
-rw-r--r-- 3 hadoop supergroup 82 2018-07-06 11:35 /user/hadoop/MEWordCount_output/part-r-00000
```
View the statistics in part-r-00000 by running the following command:
```
[hadoop@172 hadoop]$ hadoop fs -cat /user/hadoop/MEWordCount_output/part-r-00000
Hello	2
World.	1
a	1
another	1
are	1
how	1
is	2
message.	2
this	2
world,	1
you?	1……
```

### Counting a Text File in COS
Go to the `/usr/local/service/hadoop` directory and submit the task by running the following command:
```
[hadoop@10 hadoop]$ hadoop jar
/usr/local/service/hadoop/WordCount-1.0-SNAPSHOT-jar-with-dependencies.jar
WordCount cosn://$bucketname/test.txt cosn://$bucketname /WordCount_output
```
The input file for the command is changed to `cosn:// $bucketname/ test.txt`, where $bucketname is your bucket name and path. The result will go to COS as well. Run the following command to view the output file:
```
[hadoop@10 hadoop]$ hadoop fs -ls cosn:// $bucketname /WordCount_output
Found 2 items
-rw-rw-rw- 1 hadoop Hadoop 0 2018-07-06 10:34 cosn://$bucketname /WordCount_output/_SUCCESS
-rw-rw-rw- 1 hadoop Hadoop 1306 2018-07-06 10:34 cosn://$bucketname /WordCount_output/part-r-00000
```
View the final output result:
```
[hadoop@10 hadoop]$ hadoop fs -cat cosn:// $bucketname /WordCount_output1/part-r-00000
Hello	2
World.	1
a	1
another	1
are	1
how	1
is	2
message.	2
this	2
world,	1
you?	1
```

