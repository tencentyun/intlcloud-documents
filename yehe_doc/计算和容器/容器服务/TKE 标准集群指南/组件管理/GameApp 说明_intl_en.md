## Overview


### Add-on description
This add-on is based on the feature of maintaining shared memory after a game process restarts. It is a Kubernetes workload controller (GameApp) with container in-place updating.

### Add-on features

- Supports in-place updates, and maintains shared memory (currently supports image updates).
- Supports the GameApp Scale (HPA) feature.
- Supports operator high availability deployment.
- By injecting one-time metadata into the restarted container, the add-on implements the feature of controlling whether to clear shared memory during the container restart process.


### Kubernetes objects deployed in a cluster



| Kubernetes Object Name | Type | Default Resource Occupation | Namespace |
| -------------------------- | ------------------------ | ------ | ------------ |
| gameapps.game.scr.ied.com | CustomResourceDefinition | - | - |
| gameapp-operator | ClusterRoleBinding | - | - |
| gameapp-operator | ClusterRole | - | - |
| gameapp-operator | ServiceAccount | - | default |
| gameapp-controller-manager | StatefulSet | 1C2G | default |


## Limits
- Supports clusters with Kubernetes version 1.10 and above.
- You must set the launch parameters of kube-apiserver as follows: ` --feature-gates=CustomResourceSubresources=true`.

>? We recommend that you purchase clusters of version 1.12.4 on [Tencent Cloud TKE](https://console.qcloud.com/tke2) so that you do not need to modify any parameters.

## Usage

### Installing the add-on



1. Log in to the [TKE Console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the "Add-on List" page.
4. On the "Add-on List" page, click **Create**. Then, on the "Create an Add-on" page that appears, select **GameApp**.
5. Click **Finish** to create the add-on.



### Using YAML to create and use GameApp workloads
#### Creating
1. When creating `GameApp` resources, specify the `env` to be injected, and specify the update policy as in-place update. The YAML file content is as shown in the following example:
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
3. Execute the following command to set only the update image.
```
kubectl patch gameapp test-gameapp --type=json -p'[{"op":"replace","path":"/spec/template/spec/containers/0/image","value":"nginx:1.14"}]'
```
5. Execute the following command again to view whether `env` has been injected.
```
kubectl exec test-gameapp-1 printenv clearSHM
```
If no value is returned, this means that `env` is not injected.
