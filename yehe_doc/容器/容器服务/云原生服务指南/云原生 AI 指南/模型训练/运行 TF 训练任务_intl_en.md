This document describes how to run a TF training job.


## Prerequisites

- [TF Operator](https://intl.cloud.tencent.com/document/product/457/49365) has been installed in your AI environment.
- Your AI environment has GPU resources.

## Directions

The following steps are based on the official distributed training [examples](https://github.com/kubeflow/training-operator/tree/master/examples/tensorflow/dist-mnist) in parameter server/worker mode of `TF-Operator`.

### Preparing the training code

The code sample [dist_mnist.py](https://raw.githubusercontent.com/kubeflow/training-operator/master/examples/tensorflow/dist-mnist/dist_mnist.py) at the official website of Kubeflow is used.

### Creating a training image

Image creation is easy. You only need to get an official image based on TensorFlow 1.5.0, copy the above code to the image, and configure `entrypoint`.

> ? If `entrypoint` is not configured, you can also configure the container startup command when submitting a `TFJob`.


### Submitting the job

1. Prepare a `TFJob` [YAML file](https://raw.githubusercontent.com/kubeflow/training-operator/master/examples/tensorflow/dist-mnist/tf_job_mnist.yaml) to define two parameter servers and four workers.
<dx-alert infotype="notice" title=" ">
You need to replace the `<training image>` placeholder with the address of the uploaded training image.
</dx-alert>
```yaml
apiVersion: "kubeflow.org/v1"
kind: "TFJob"
metadata:
  name: "dist-mnist-for-e2e-test"
spec:
  tfReplicaSpecs:
    PS:
      replicas: 2
      restartPolicy: Never
      template:
        spec:
          containers:
            - name: tensorflow
              image: <training image>
    Worker:
      replicas: 4
      restartPolicy: Never
      template:
        spec:
          containers:
            - name: tensorflow
              image: <training image>
```
2. Run the following command to use `kubectl` to submit the `TFJob`:
```shell
kubectl create -f ./tf_job_mnist.yaml
```
3. Run the following command to view the job status:
```shell
kubectl get tfjob dist-mnist-for-e2e-test -o yaml
kubectl get pods -l pytorch_job_name=pytorch-tcp-dist-mnist 
```

