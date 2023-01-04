### Container
A container is a lightweight virtualization technology. It can run everywhere once built. A Docker container is in essence a host process featuring namespace-based resource isolation, cgroup-driven resource limitation, and efficient file operations through copy-on-write.
### TCSS
TCSS is a one-stop security solution and platform that protects containers against all kinds of risks throughout their lifecycle. It implements a closed loop of security from container security prediction, defense, and check to response.
### Orchestration tool
The container orchestration tool provides a framework for managing large-scale containers and microservice architectures. It can be used in any environment where containers run.
### Container escape
Attackers get certain permission to run commands in the container by hijacking the containerized business logic or through direct control. They leverage some means to further get certain permission to run commands on the host of the container.
### Killing a container
A container process is quickly killed, usually when the container cannot be stopped.
### Image repository
An image repository is used to store Docker images. A single image repository corresponds to a single Docker application and hosts different versions of the application to deploy TKE.
### Docker image
A Docker image is a special file system. In addition to the required program, library, resource, and configuration files, it also provides some configuration parameters for the container runtime, such as anonymous volumes, environment variables, and users. An image does not contain any dynamic data, and its content will not change after the build.
