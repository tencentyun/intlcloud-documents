## Overview

### Add-on description
This add-on is based on the feature of maintaining shared memory after a game process restarts. It is a Kubernetes workload controller (GameApp) with container in-place updating.

### Add-on features

- Supports in-place updates, and maintains shared memory (currently supports image updates).
- Supports GameApp Scale (HPA) feature.
- Supports operator high availability deployment.
- By injecting one-time metadata into the restarted container, it implements the function of controlling whether to clear shared memory.


### Kubernetes objects deployed in a cluster

Deploying GameApp Add-on in a cluster will deploy the following Kubernetes objects in the cluster:

| Kubernetes Object Name             | Type                       | Default Resource Occupation | Namespaces |
| -------------------------- | ------------------------ | ------ | ------------ |
| gameapps.game.scr.ied.com  | CustomResourceDefinition | \      | \            |
| gameapp-operator           | ClusterRoleBinding       | \      | \            |
| gameapp-operator           | ClusterRole              | \      | \            |
| gameapp-operator           | ServiceAccount           | \      | default      |
| gameapp-controller-manager | StatefulSet              | 1C2G   | default      |


## Limits
- Supports clusters with Kubernetes version 1.10 and above.
- The launch parameters of kube-apiserver must be set as follows: ` --feature-gates=CustomResourceSubresources=true`.

>We recommend to purchase clusters of version 1.12.4 on [Tencent Cloud TKE](https://console.cloud.tencent.com/tke2), so that you do not need to modify any parameters.

## Usage

### Installing the add-on
1. Log in to the [TKE Console](https://console.cloud.tencent.com/tke2), and select **Add-ons** in the left sidebar.
2. On the top of the **Add-ons** management page, select the region and the cluster for installing GameApp, and click **Create**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/601a8e4118a112fe26355ef6535e6038.png)
3. In the **Create Add-on** page, select **GameApp**, and click **Complete** to install it.



### Using YAML to create and use GameApp
#### Creating
1. When creating `GameApp`  resources, specify the `env` needs to be injected, and specify the update policy as in-place update. The YAML file content is as shown in the following example:
```
apiVersion: game.scr.ied.com/v1
kind: GameApp
metadata:
  name: "test-gameapp"
spec:
  replicas: $replicas
  selector:
    matchLabels:
      app: nginx
  serviceName: "test-gameapp"
  template:
    metadata:
      annotations:
        test: test
      labels:
        app: nginx
    spec:
      containers:
      - image: nginx
        name: c1
        ports:
        - containerPort: 80
          name: web
        resources: {}
        volumeMounts:
        - mountPath: /dev/shm
          name: shm
        env:
        - name: clearSHM
          valueFrom:
            fieldRef:
              # Specifies `env` needs to be injected
              fieldPath: metadata.annotations['oneshot.cloud.tencent.com/clearSHM'] 
      terminationGracePeriodSeconds: 10
      volumes:
      - emptyDir:
          medium: Memory
          sizeLimit: 1Gi
        name: shm
  updateStrategy:
    type: StableUpdate # Specifies the policy is in-place update
```

#### Usage
1. <span id="step1"></span>Execute the following command to set the upgrade image and one-time parameters.
```
$ cat example/patch.yaml
template:
  metadata:
    annotations:
      oneshot.cloud.tencent.com/clearSHM: "true"
  spec:
    containers:
    - image: nginx:1.14        
      name: c1
$ kubectl patch gameapp test-gameapp --patch "$(cat patch.yaml)"
```
2. Execute the following command to verify whether env has been injected successfully.
```
kubectl exec test-gameapp-1 printenv clearSHM
true
```
If the execution result returns the parameters set in [Step 1](#step1), `env` has been injected successfully.
4. Execute the following command to set only the update image.
```
kubectl patch gameapp test-gameapp --type=json -p'[{"op":"replace","path":"/spec/template/spec/containers/0/image","value":"nginx:1.14"}]'
```
5. Execute the following command again to view whether `env` has been injected.
```
kubectl exec test-gameapp-1 printenv clearSHM
```
If no value is returned, this means that env has not been injected.
