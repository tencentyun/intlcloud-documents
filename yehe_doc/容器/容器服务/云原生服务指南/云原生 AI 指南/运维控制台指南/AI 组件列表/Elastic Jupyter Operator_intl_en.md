## Overview 

[elastic-jupyter-operator](https://github.com/tkestack/elastic-jupyter-operator) is a native elastic Jupyter service in Kubernetes. It provides an elastic Jupyter Notebook service as needed with the following features:

- It automatically releases resources to the Kubernetes cluster when the GPU is idle.
- It supports delayed resource application, allowing you to apply for CPU, memory, and GPU resources as needed.
- Multiple Jupyter notebooks share a resource pool to increase the resource utilization.


## Deployment

During Helm deployment, all configuration items are included in `values.yaml`.

Some fields may need to be customized, as listed below:

| Parameter               | Description         | Default Value                                                       |
| ------------------ | ------------ | ------------------------------------------------------------ |
| `image.repository` | The repository where the image resides | `ccr.ccs.tencentyun.com/kubeflow-oteam/elastic-jupyter-operator` |
| `image.tag`        | Image version   | `"v0.1.1"`                                                   |
| `namespace.name`   | Namespace     | `"enterprise-gateway"`                                       |

## How to use

>?For more information, see [elastic-jupyter-operator](https://github.com/tkestack/elastic-jupyter-operator/blob/master/README.md).

1. Run the following command to create a Jupyter Gateway CR:
```bash
kubectl apply -f ./config/samples/kubeflow.tkestack.io_v1alpha1_jupytergateway.yaml
```
Below is the content of the YAML file:
```yaml
apiVersion: kubeflow.tkestack.io/v1alpha1
kind: JupyterGateway
metadata:
  name: jupytergateway-sample
spec:
  cullIdleTimeout: 3600
```
Here, `cullIdleTimeout` is a configuration item. If a kernel is idle in the time in seconds specified by `cullIdleTimeout`, Gateway will repossess it to release resources.
2. Run the following command to create a Jupyter Notebook CR instance and specify the Gateway CR:
```bash
kubectl apply -f ./config/samples/kubeflow.tkestack.io_v1alpha1_jupyternotebook.yaml
```
Below is the content of the YAML file:
```yaml
apiVersion: kubeflow.tkestack.io/v1alpha1
kind: JupyterNotebook
metadata:
  name: jupyternotebook-sample
spec:
  gateway:
    name: jupytergateway-sample
    namespace: default
```
3. All resources in the cluster are as listed below:
```shell
NAME                                          READY   STATUS    RESTARTS   AGE
pod/jupytergateway-sample-6d5d97949c-p8bj6    1/1     Running   2          11d
pod/jupyternotebook-sample-5bf7d9d9fb-nq9b8   1/1     Running   2          11d

NAME                            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
service/jupytergateway-sample   ClusterIP   10.96.138.111   <none>        8888/TCP   11d
service/kubernetes              ClusterIP   10.96.0.1       <none>        443/TCP    31d

NAME                                     READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/jupytergateway-sample    1/1     1            1           11d
deployment.apps/jupyternotebook-sample   1/1     1            1           11d

NAME                                                DESIRED   CURRENT   READY   AGE
replicaset.apps/jupytergateway-sample-6d5d97949c    1         1         1       11d
replicaset.apps/jupyternotebook-sample-5bf7d9d9fb   1         1         1       11d
```
4. Use a method such as NodePort, `kubectl port-forward`, or Ingress to expose Notebook CR to provide the Service. Here, `kubectl port-forward` is used as an example. Run the following command:
```shell
kubectl port-forward jupyternotebook-sample-5bf7d9d9fb-nq9b8 8888
```

## API documentation

See [API Reference](https://github.com/tkestack/elastic-jupyter-operator/blob/master/docs/api/generated.asciidoc).
