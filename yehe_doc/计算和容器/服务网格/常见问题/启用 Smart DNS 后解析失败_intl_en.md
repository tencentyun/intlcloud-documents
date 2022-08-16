After Istio's smart DNS is enabled, DNS resolution fails in some cases. For example: 

- DNS resolution fails in a container created from an alpine image.
- DNS resolution fails in a gRPC service.

## Cause

There are some problems in the initial implementation of smart DNS. The format of a responded DNS packet is different from that of ordinary DNS. There is no problem when the underlying library glibc is used for resolution. However, resolution may fail if another DNS client is used.

- The alpine image uses musl libc as its underlying library. The resolution behavior of musl libc is different from that of glibc. When the packet format is abnormal, musl libc may fail to resolve the packet. Most applications use the underlying library for resolution, which causes a resolution failure.
- For services that use the c/c++ based gRPC framework, the c-ares library is used for DNS resolution by default, and the underlying library is not invoked for resolution. c-ares will fail to resolve the packet in some scenarios when the packet is abnormal.

## Bug Fixing

This issue has been fixed in Istio 1.9.2. For details, see the key PR [#31251](https://github.com/istio/istio/pull/31251) and one of the [issues](https://github.com/istio/istio/issues/31295).

## Workaround Solution

If Istio cannot be upgraded to a version later than 1.9.2 temporarily, you can work around the problem by the following methods:

- Change the base image from the alpine image to another image (underlying libraries of other base images are basically glibc).
- Set the `GRPC_DNS_RESOLVER` environment variable for the c/c++ based gRPC service to `native`. This setting indicates that the underlying library is used for resolution, not the default library c-ares. For description of environment variables, see the [gRPC Documentation](https://github.com/grpc/grpc/blob/master/doc/environment_variables.md).
