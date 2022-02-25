[](id:ci-init)
### Why am I prompted with "cannot pull code" when using ci-init?

When the ci-init command is used for a build plan (job) created before October 10, 2019, a public/private key pair is created for the user, so they can pull code from repositories in the project. A key pair will not be created when calling ci-init for a build plan created after this date.

We have built in a credential ID for newly created build plans so users can pull code from repositories. Simply use env.CREDENTIALS_ID as the credentialsId of userRemoteConfigs.

#### Old syntax

```groovy
pipeline {
    agent any
        stages {
        stage('check out') {
            steps {
                // The old syntax includes ci-init 
                sh 'ci-init'

                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: env.GIT_BUILD_REF]],
                    userRemoteConfigs: [[url: env.GIT_REPO_URL]]
                ])
            }
        }
    }
}
```

#### New syntax

```groovy
pipeline {
    agent any
        stages {
        stage('check out') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: env.GIT_BUILD_REF]],
                    // Note that the new checkout syntax has the additional credentialsId: env.CREDENTIALS_ID
                    userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]
                ])
            }
        }
    }
}
```

**As CODING already supports credential management, you should use the more secure credential ID in place of ci-init.**


[](id:apostrophe)
### When should I use single or double quotes?

When using CODING Continuous Integration (CODING-CI), you often need to splice strings or use environment variables as parameters in a Jenkinsfile. Single and double quotes are used differently in a Jenkinsfile. The following demonstrates the differences between the commonly used echo and sh commands.

```groovy
pipeline {
    agent any
    environment {
        MY_ENV = 'this is my env'
    }
    stages {
        stage('Test') {
            steps {
                script    {
                    def MY_ENV = 'define in script'

                    echo "${env.MY_ENV}"
                    // Output: this is my env

                    echo "\${env.MY_ENV}"
                    // Output: ${env.MY_ENV}

                    echo "${MY_ENV}"
                    // Output: define in script

                    echo '${MY_ENV}'
                    // Output: ${MY_ENV}

                    sh 'echo ${MY_ENV}'
                    // Output: this is my env

                    sh "echo ${MY_ENV}"
                    // Output: define in script

                    sh "echo ${env.MY_ENV}"
                    // Output: this is my env
                }
            }
        }
    }
}
```

- echo: When using single quotes, the $ symbols inside are not parsed, but directly included in the output. When using double quotes, MY_ENV in the environment variables is printed.
- sh: When using single quotes, the original text is executed as the sh command normally used in the terminal, so MY_ENV in the environment variables can be printed.

[](id:source)
### When creating a build plan, what is the difference between choosing to use a Jenkinsfile from a code repository or a static, configured Jenkinsfile?

- When you select a Jenkinsfile from a code repository, the file is stored in the repository. Modifications to the Jenkinsfile require commits to the code repository. If you modify the trigger conditions for continuous integration, integration tasks can still be automatically triggered.
- When you use a static, configured Jenkinsfile, the file is not stored in a code repository, so modifications to the Jenkinsfile do not involve repository updates. During build execution, you should use only static, configured files to ensure the consistency of the build process.
