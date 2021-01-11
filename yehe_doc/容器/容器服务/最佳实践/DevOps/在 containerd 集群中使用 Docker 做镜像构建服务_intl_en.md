## Overview

In a Kubernetes cluster, some CI/CD workflow may need to use Docker to provide image packaging services. This can be implemented by the Docker of the host. Mount Docker's UNIX Socket (`/var/run/docker.sock`) as the hostPath to the CI/CD service Pod, and then call the Docker of the host through the UNIX Socket to build image in the container. This method is simple and can save more resources than running a Docker host inside of another Docker host (Docker in Docker). However, this method may encounter the following problems:
- It cannot be performed in a cluster whose Runtime is containerd.
- If it is not controlled, it may overwrite the existing image on the node.
- When you need to modify the Docker Daemon configuration file, it may affect other services.
- It is not safe in the multi-tenancy scenario. After the privileged Pod obtains the UNIX Socket of Docker, the container in the Pod can not only call the host's Docker to build the image, delete the existing image or container, or even operate other containers through `docker exec` interface.

For the first problem above, Kubernetes has officially announced that Docker will be disused after version 1.22. These users may switch their service to containerd. For some clusters that require a containerd, and still use Docker to build the image without changing the CI/CD service process, you can add the DinD container to the original Pod as a sidecar or use DaemonSet to deploy the Docker service dedicated to building the image on the node.
This document describes the following two ways to use Docker to build images on the CI/CD workflow:
- [Using DinD as the Sidecar of Pod](#DinD)
- [Using DaemOnset to deploy Docker on each Containerd node](#DaemonSet)

## Directions

### Using DinD as the Sidecar of Pod

For the implementation principle of DinD (Docker in Docker), see [DinD](https://hub.docker.com/_/docker) Official Document. The following example shows that adding a Sidecar to clean-ci container, and combined with emptyDir, making the clean-ci container can access the DinD container through UNIX sockets.
```yaml
apiVersion: v1
kind: Pod
metadata:
   name: clean-ci
spec:
   containers:
   - name: dind
     image: 'docker:stable-dind'
     command:
     - dockerd
     - --host=unix:///var/run/docker.sock
     - --host=tcp://0.0.0.0:8000
     securityContext:
       privileged: true
     volumeMounts:
     - mountPath: /var/run
       name: cache-dir
   - name: clean-ci
     image: 'docker:stable'
     command: ["/bin/sh"]
     args: ["-c", "docker info >/dev/null 2>&1; while [ $? -ne 0 ] ; do sleep 3; docker info >/dev/null 2>&1; done; docker pull library/busybox:latest; docker save -o busybox-latest.tar library/busybox:latest; docker rmi library/busybox:latest; while true; do sleep 86400; done"]
     volumeMounts:
     - mountPath: /var/run
       name: cache-dir
   volumes:
   - name: cache-dir
     emptyDir: {}
```

### Using DaemOnset to deploy Docker on each containerd node

This method is simple. You just need to directly forward the DaemonSet in the containerd cluster (mounting hostPath). In order not to affect the `/var/run` path on the node, you can specify other paths.

1. Use the following YAML to deploy DaemonSet, as shown below:
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
      name: docker-ci
spec:
      selector:
        matchLabels:
          app: docker-ci
      template:
        metadata:
          labels:
            app: docker-ci
        spec:
          containers:
          - name: docker-ci
            image: 'docker:stable-dind'
            command:
            - dockerd
            - --host=unix:///var/run/docker.sock
            - --host=tcp://0.0.0.0:8000
            securityContext:
              privileged: true
            volumeMounts:
            - mountPath: /var/run
              name: host
          volumes:
          - name: host
            hostPath:
              path: /var/run
```
2. Share the same hostPath between the service Pod and DaemonSet, as shown below:
```yaml
apiVersion: v1
kind: Pod
metadata:
      name: clean-ci
spec:
      containers:
      - name: clean-ci
        image: 'docker:stable'
        command: ["/bin/sh"]
        args: ["-c", "docker info >/dev/null 2>&1; while [ $? -ne 0 ] ; do sleep 3; docker info >/dev/null 2>&1; done; docker pull library/busybox:latest; docker save -o busybox-latest.tar library/busybox:latest; docker rmi library/busybox:latest; while true; do sleep 86400; done"]
        volumeMounts:
        - mountPath: /var/run
          name: host
      volumes:
      - name: host
        hostPath:
          path: /var/run
```
