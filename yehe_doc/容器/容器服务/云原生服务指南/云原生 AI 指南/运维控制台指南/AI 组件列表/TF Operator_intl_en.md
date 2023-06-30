## Overview 

Developed by the [Kubeflow](https://www.kubeflow.org) community, [TF-Operator](https://github.com/kubeflow/tf-operator) is an add-on used to help deploy and execute [TensorFlow](https://www.tensorflow.org) distributed training jobs in a Kubernetes cluster.

After deployment, you can create, view, and delete [TF jobs](https://www.kubeflow.org/docs/components/training/tftraining/).

## Prerequisite dependencies

 Kubernetes cluster (v1.16 or later)

## Deployment

During Helm deployment, all configuration items are included in `values.yaml`.

Some fields may need to be customized, as listed below:

| Parameter               | Description                                  | Default Value                                              |
| ------------------ | ------------------------------------- | --------------------------------------------------- |
| `image.repository` | The repository where the TF-Operator image resides              | `ccr.ccs.tencentyun.com/kubeflow-oteam/tf-operator` |
| `image.tag`        | TF-Operator image version                | `"latest"`                                          |
| `namespace.create` | Whether to create a separate namespace for TF-Operator | `true`                                              |
| `namespace.name`   | The namespace where TF-Operator is to be deployed           | `"tf-operator"`                                     |

## Best practices

See [Running TF Training Job](https://intl.cloud.tencent.com/document/product/457/49369).



