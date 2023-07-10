## Overview

This document describes how to set data and metadata caching parameters.

## Directions

### Enabling/Disabling data caching

To enable data caching in GooseFSRuntime, set `goosefs.worker.ufs.instream.cache.enabled` to `true` (default value).

To disable data caching, set `goosefs.worker.ufs.instream.cache.enabled` to `false`, as shown below.
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: hadoop
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1/
        quota: 290G
        high: "0.9"
        low: "0.8"
  properties:
    goosefs.worker.ufs.instream.cache.enabled: "false"
```

### Enabling metadata caching

In GooseFSRuntime, you can use metadata to cache metadata information. To enable metadata caching, set `goosefs.user.metadata.cache.enabled` to `true`. The default value of the attribute is `false`.

Sample code:
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: hadoop
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1/
        quota: 290G
        high: "0.9"
        low: "0.8"
  properties:
    oosefs.worker.ufs.instream.cache.enabled: "true"
    goosefs.user.metadata.cache.enabled: "true"
```

