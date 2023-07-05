## Overview 

Developed by the [Kubeflow](https://www.kubeflow.org) community, [MPI-Operator](https://github.com/kubeflow/mpi-operator) is an add-on used to help deploy and execute data-parallel distributed training such as [Horovod](https://horovod.ai) in a Kubernetes cluster.

After deployment, you can create, view, and delete [MPI jobs](https://github.com/kubeflow/mpi-operator/blob/master/pkg/apis/kubeflow/v1/types.go).


## Prerequisite dependencies

Kubernetes cluster (v1.16 or later)

## Deployment

During Helm deployment, all configuration items are included in `values.yaml`.

Some fields may need to be customized, as listed below:

| Parameter               | Description                                   | Default Value                                               |
| ------------------ | -------------------------------------- | ---------------------------------------------------- |
| `image.repository` | The repository where the MPI-Operator image resides              | `ccr.ccs.tencentyun.com/kubeflow-oteam/mpi-operator` |
| `image.tag`        | MPI-Operator image version                | `"latest"`                                           |
| `namespace.create` | Whether to create a separate namespace for MPI-Operator | `true`                                               |
| `namespace.name`   | The namespace where MPI-Operator is to be deployed           | `"mpi-operator"`                                     |

