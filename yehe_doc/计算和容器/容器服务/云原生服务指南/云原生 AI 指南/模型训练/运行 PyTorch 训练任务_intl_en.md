This document describes how to run a PyTorch training job.


## Prerequisites

- PyTorch Operator has been installed in your AI environment.
- Your AI environment has GPU resources.

## Directions

The following steps are based on the official distributed training [examples](https://github.com/kubeflow/pytorch-operator/tree/master/examples/mnist) of `PyTorch-Operator`.

### Preparing the training code

The code sample [mnist.py](https://raw.githubusercontent.com/kubeflow/pytorch-operator/master/examples/mnist/mnist.py) at the official website of Kubeflow is used.

### Creating a training image

Training image creation is easy. You only need to get an official image based on PyTorch 1.0, copy the above code to the image, and configure `entrypoint` (if `entrypoint` is not configured, you can also configure the startup command when submitting a `PyTorchJob`).

> ! The training code is written based on PyTorch 1.0. As APIs of different PyTorch versions may be incompatible, you may need to adjust the above training code in a PyTorch environment on other versions.

### Submitting the job

1. Prepare a `PyTorchJob` [YAML file](https://raw.githubusercontent.com/kubeflow/pytorch-operator/master/examples/mnist/v1/pytorch_job_mnist_nccl.yaml) to define one master worker and one worker.
<dx-alert infotype="notice" title=" ">
- You need to replace the `<training image>` placeholder with the address of the uploaded training image.
- As GPU resources are configured in resource configuration, set `backend` for training to `"nccl"` in `args`; in jobs using no (Nvidia) GPU resources, use another backend such as `gloo`.
</dx-alert>
```yaml
apiVersion: "kubeflow.org/v1"
kind: "PyTorchJob"
metadata:
  name: "pytorch-dist-mnist-nccl"
spec:
  pytorchReplicaSpecs:
    Master:
      replicas: 1
      restartPolicy: OnFailure
      template:
        metadata:
          annotations:
            sidecar.istio.io/inject: "false"
        spec:
          containers:
            - name: pytorch
              image: <training image>
              args: ["--backend", "nccl"]
              resources: 
                limits:
                  nvidia.com/gpu: 1
    Worker:
      replicas: 1
      restartPolicy: OnFailure
      template:
        metadata:
          annotations:
            sidecar.istio.io/inject: "false"
        spec:
          containers: 
            - name: pytorch
              image: <training image>
              args: ["--backend", "nccl"]
              resources: 
                limits:
                  nvidia.com/gpu: 1
```
2. Run the following command to use `kubectl` to submit the `PyTorchJob`:
```shell
kubectl create -f ./pytorch_job_mnist_nccl.yaml
```
3. Run the following command to view the `PyTorchJob`:
```shell
kubectl get -o yaml pytorchjobs pytorch-dist-mnist-nccl
```
4. Run the following command to view Pods created by the PyTorch job:
```shell
kubectl get pods -l pytorch_job_name=pytorch-dist-mnist-nccl  
```

