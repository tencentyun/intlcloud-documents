This document describes how to use SSH in Continuous Integration.

## Prerequisites
Before configuring the CODING Continuous Integration (CODING-CI) build environment, you must activate the CODING DevOps service for your Tencent Cloud account.

## Open Project
1. Log in to the CODING Console and click the **team domain name** to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a **project icon** to open the project.
3. Select **Continuous Integration** from the menu on the left.

## Function Overview[](id:intro)
When executing a build in Continuous Integration, you may need to log in to a remote server with SSH protocol to execute the necessary script or command. Go to **Continuous Integration** > "Build Plan Settings" > "Process Configuration", use the text editor to enter the relevant command.

## How to Use SSH Commands[](id:ssh-commands)
CODING-CI allows you to control a remote server using SSH commands.
- sshCommand: Run a specific command on the remote server.
- sshPut: Place files or directories of the current workspace in the remote server.
- sshGet: Obtain files or directories from a remote server.
- sshScript: Read the local shell script and run it on the remote server. If you run the script of the remote server, you will get the error: does not exist.
- sshRemove: Remove a certain file or directory from a remote server.

The following example shows how to use an account and password to connect to a remote server and run SSH commands. An example of a Jenkinsfile configuration is as follows:
```groovy
def remote = [:]
remote.name = "node"
remote.host = "node.abc.com"
remote.allowAnyHosts = true

node {
    withCredentials([usernamePassword(credentialsId: 'sshUserAcct', 
        passwordVariable: 'password', usernameVariable: 'userName')]) {
        remote.user = userName
        remote.password = password

        stage("SSH Steps Rocks!") {
            writeFile file: 'test.sh', text: 'ls'
            sshCommand remote: remote, 
                command: 'for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done'
            sshScript remote: remote, script: 'test.sh'
            sshPut remote: remote, from: 'test.sh', into: '.'
            sshGet remote: remote, from: 'test.sh', into: 'test_new.sh', override: true
            sshRemove remote: remote, path: 'test.sh'
        }
    }
}
```

## How to Use SSH to Connect to a Remote Service[](id:ssh-remote)
Besides using an account and password to connect to a remote server, you can also use an SSH private key to connect to a remote service. An example of a Jenkinsfile configuration is as follows:
```groovy
def remote = [:]
remote.name = "node"
remote.host = "node.abc.com"
remote.allowAnyHosts = true

node {
    withCredentials([sshUserPrivateKey(credentialsId: 'sshUser', keyFileVariable: 'identity')]) {
        // SSH login username
        remote.user = 'root'
        // Private key file address
        remote.identityFile = identity
        stage("SSH Steps Rocks!") {
            writeFile file: 'abc.sh', text: 'ls'
            sshCommand remote: remote, 
                command: 'for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done'
            sshPut remote: remote, from: 'abc.sh', into: '.'
            sshGet remote: remote, from: 'abc.sh', into: 'bac.sh', override: true
            sshScript remote: remote, script: 'abc.sh'
            sshRemove remote: remote, path: 'abc.sh'
        }
    }
}
```

## More Information[](id:more)
- For more information on SSH commands in Jenkinsfile, see the [official Jenkins Help Documentation](https://jenkins.io/doc/pipeline/steps/ssh-steps/).
- For more information about Jenkins SSH plugins, see the plugin's [official homepage](https://github.com/jenkinsci/ssh-steps-plugin).
