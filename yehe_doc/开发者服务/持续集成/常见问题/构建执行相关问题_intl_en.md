In most computer operating systems, any process that exits leaves an exit code that indicates whether the process ran as expected. Therefore, if the exit code of the execution process in continuous integration (CI) is not 0, the system judges the build to have failed. The following are common causes of build execution failure:

### How do I fix CI configuration file syntax errors?

Like most programming languages, a Jenkinsfile is composed of a domain-specific language (DSL), so syntax errors can cause compilation or runtime failures.

### How do I resolve failed tests?

Most mainstream testing tools and frameworks set the exit code to a non-zero value by default when the test logic fails.

[](id:que3)
### How do I resolve a build timeout or an insufficient build quota?

When using CODING Continuous Integration (CODING-CI), each team has a certain build quota. To prevent the malicious use of CI in cyberattacks, each build task has a timeout limit. Build tasks that time out or exceed the build quota are terminated by the system. If you need a higher quota, you can adjust the quota in Team Management by purchasing the quota you require.

### How do I view build logs and build snapshots?

CODING-CI provides build logs, which allow users to determine the causes of faults. In addition, CODING-CI provides a configuration snapshot for each build. You can use the snapshot to get the configuration file content and parameters used in the build. This way, you can see if configuration issues caused the build to fail.

#### Build log
![](https://qcloudimg.tencent-cloud.cn/raw/9b2d92d40567cddf3dc8847b39577404.png)

#### Build snapshot
![](https://qcloudimg.tencent-cloud.cn/raw/fe101ae4878052d20e57567b40d9f56b.png)

### How do I run automated tasks locally?

You can re-execute the automated logic (for example, re-run the test code locally) or modify the code in real time to get more feedback for troubleshooting.

### What happens if I use an interactive command-line program?

In the CI process, you cannot directly use interactive commands. If you use a program that calls up an interactive command-line window, the build will fail.

A common command is `npm login docker login -u xxx` (the `docker -u xx -p xx` command is required when logging in to Docker during CI).

>?If you cannot find an answer to your question in this document, please go to the [Ticket Center](https://e.coding.net/signin?redirect=/workorder) to submit an issue. We will promptly provide a solution to your problem.

[](id:how-to-debug)
### How do I debug build tasks?

If you need to debug a build run process, you can provide the SSH by adding the following steps to the build process:

```groovy
steps {
  sh 'apt-get update'
  sh 'apt-get install -y tmate openssh-client'
  sh '''echo -e \'y
\'|ssh-keygen -q -t rsa -N "" -f ~/.ssh/id_rsa'''
  sh 'tmate -S /tmp/tmate.sock new-session -d'
  sh 'tmate -S /tmp/tmate.sock wait tmate-ready'
  sh '''
tmate -S /tmp/tmate.sock display -p \'#{tmate_ssh}\'
tmate -S /tmp/tmate.sock display -p \'#{tmate_web}\'
echo "WebURL: ${tmateWeb}"
echo "SSH: ${tmateSSH}"
'''
  sh 'sleep 3600'
}
```

[](id:aliyun)
### Why can't I connect to Alibaba Cloud servers?

The system may return the error `Connection reset` when you run an SSH command to access an Alibaba Cloud server.
![](https://main.qcloudimg.com/raw/feb1ac52d4e3f34bebd8bc5f4608d358.png)

This problem occurs when the CODING IP address has not been added to the Alibaba Cloud whitelist. Go to the Alibaba Cloud **Security Management Platform** > **Security Management** > **Add to Access Whitelist** and add the IP address of the builder to the whitelist so that it will not be blocked when accessing the cloud server.

CODING's builders use the following egress IP addresses:

```bash
# China Shanghai Node

111.231.92.100

81.68.101.44

# China Hong Kong Node

124.156.164.25

119.28.15.65

# US Silicon Valley Node

170.106.136.17

170.106.83.77

```

>? When directly copying the IP address of the builder provided on the build plan page, remove the `/32` at the end to prevent formatting errors.
