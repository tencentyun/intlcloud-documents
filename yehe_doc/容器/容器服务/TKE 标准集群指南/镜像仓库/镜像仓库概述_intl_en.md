## Image Registry Overview
Image Registry is a repository for Docker images, which can be used to deploy the Tencent Kubernetes Engine (TKE) service. Each image has a unique ID in the following format: image registry address + image name + image tag.

## Image Types
Currently, Image Registry supports official images of Docker Hub and users’ private images.

## Image Lifecycle

The image lifecycle covers the generation, upload, and deletion of image tags. To facilitate the management of global images, TKE uses the following image lifecycle management mechanism:
- Global image lifecycle management. After this feature is enabled, the configured global rules are applied to all images of the root account.
- Configuration of an image tag automatic clearing policy for a specified image repository. This policy has higher priority than the global configuration.

For information on how to configure the image lifecycle in the image repository, see "Image Lifecycle Management".


## Help Documentation
- [Basic Operations of Image Registry](https://intl.cloud.tencent.com/document/product/457/9117)
- Image Lifecycle Management
- [How to Build a Docker Image](https://intl.cloud.tencent.com/document/product/457/9115)
- [How to Build a Private Image Registry](https://intl.cloud.tencent.com/document/product/457/9114)
- [Using a Docker Hub Accelerator](https://intl.cloud.tencent.com/document/product/457/9113)
