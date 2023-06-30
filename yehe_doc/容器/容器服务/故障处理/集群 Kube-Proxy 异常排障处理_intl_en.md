
TKE cluster access may fail in some cases. If you have confirmed that the backend Pod is normal, the cause may be that the kube-proxy add-on version is earlier than required, preventing iptables or IPVS forwarding rules on the node from being delivered successfully. This document describes some problems due to earlier kube-proxy versions and offers fixes. If you still have problems, [contact us](https://intl.cloud.tencent.com/document/product/457/46720) for assistance.

## kube-proxy was not correctly adapted to the iptables backend of the node

#### Sample error message
```shell
Failed to execute iptables-restore: exit status 2 (iptables-restore v1.8.4 (legacy): Couldn't load target 'KUBE-MARK-DROP':No such file or directory
```

#### Cause
1. When `iptables-restore` is executed in kube-proxy, the dependent `KUBE-MARK-DROP` chain doesn't exist, leading to the rule sync failure and exit. The `KUBE-MARK-DROP` chain is maintained by kubelet.
2. On some later OS versions, the iptables backend is nft; while on earlier kube-proxy versions, the iptables backend is legacy. When kube-proxy on an earlier version runs on OS on a later version, the iptables backend cannot be matched, and the `KUBE-MARK-DROP` chain cannot be read. Later OS versions include:
    -   TLinux 2.6 (TK4)
    -   TLinux 3.1
    -   TLinux 3.2
    -   CentOS 8
    -   Ubuntu 20

#### Fix guide
Upgrade kube-proxy. Below is the sample logic:
<table>
<thead>
  <tr>
    <th>TKE Cluster Version</th>
    <th>Fix Policy</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>&gt; 1.18</td>
    <td>No fixes are required, as the problem doesn't exist.</td>
  </tr>
  <tr>
    <td>1.18</td>
    <td>Upgrade kube-proxy to v1.18.4-tke.26 or later.</td>
  </tr>
  <tr>
    <td>1.16</td>
    <td>Upgrade kube-proxy to v1.16.3-tke.28 or later.</td>
  </tr>
  <tr>
    <td>1.14</td>
    <td>Upgrade kube-proxy to v1.14.3-tke.27 or later.</td>
  </tr>
  <tr>
    <td>1.12</td>
    <td>Upgrade kube-proxy to v1.12.4-tke.31 or later.</td>
  </tr>
  <tr>
    <td>1.10</td>
    <td>Upgrade kube-proxy to v1.10.5-tke.20 or later.</td>
  </tr>
</tbody>
</table>

>? For more information on the latest TKE versions, see [TKE Kubernetes Revision Version History](https://intl.cloud.tencent.com/document/product/457/9315).

---
## iptables lock of kube-proxy

### Concurrent write failure due to no iptables lock mounted to another add-on

#### Sample error message
```shell
Failed to execute iptables-restore: exit status 1 (iptables-restore: line xxx failed)
```

#### Cause
1. When writing iptables rules to the kernel, iptables commands (such as `iptables-restore`) will use a file lock for sync to avoid concurrent writes of multiple instances. On Linux, the file is generally `/run/xtables.lock`.
2. For a Pod that needs to call iptables commands, such as kube-proxy, kube-router, or HostNetwork Pod on the client, if the file is not mounted, the above problem of concurrent writes may occur.

#### Fix guide
For a Pod that needs to call iptables commands, you need to mount the host `/run/xtables.lock` file to the Pod as follows:
```yaml
        volumeMounts:
        -   mountPath: /run/xtables.lock
          name: xtables-lock
          readOnly: false
      volumes:
      -   hOStPath:
          path: /run/xtables.lock
          type: FileOrCreate
        name: xtables-lock
```

### Writes are blocked due to an earlier iptables-restore version

#### Sample error message
```shell
Failed to execute iptables-restore: exit status 4 (Another app is currently holding the xtables lock. Perhaps you want to use the -w option?)
```

#### Cause
1. When writing iptables rules to the kernel, iptables commands (such as `iptables-restore`) will use a file lock for sync to avoid concurrent writes of multiple instances. When `iptables-restore` is executed, it tries getting a file lock or exits if the lock is held by another process.
2. The error is a soft error, and kube-proxy will try getting the lock again in the next sync cycle (or when the next Service event is triggered). If the lock cannot be obtained after several attempts, a high latency will occur during rule sync.
3. The `iptables-restore` on later versions provide a `-w(--wait)` option. If `-w=5`, `iptables-restore` will be blocked for five seconds when getting the lock. If another process releases the lock during this period, `iptables-restore` can continue its operation.

#### Fix guide
1. If kube-proxy is a binary deployment on the node, you can upgrade `iptables-restore` by upgrading the node OS. Below is the sample logic:
<table>
<thead>
  <tr>
    <th>Node OS</th>
    <th>Target Version</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>CentOS</td>
    <td>7.2 or later</td>
  </tr>
  <tr>
    <td>Ubuntu</td>
    <td>20.04 or later</td>
  </tr>
  <tr>
    <td>Tencent Linux</td>
    <td>2.4 or later</td>
  </tr>
</tbody>
</table>
2. If kube-proxy is a DaemonSet deployment in the cluster, you can upgrade `iptables-restore` by upgrading kube-proxy. Below is the sample logic:
<table>
<thead>
  <tr>
    <th>TKE Cluster Version</th>
    <th>Fix Policy</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>&gt; 1.12</td>
    <td>No fixes are required, as the problem doesn't exist.</td>
  </tr>
  <tr>
    <td>1.12</td>
    <td>Upgrade kube-proxy to v1.12.4-tke.31 or later.</td>
  </tr>
  <tr>
    <td>&lt; 1.12</td>
    <td>Upgrade the TKE cluster.</td>
  </tr>
</tbody>
</table>
>? For more information on the latest TKE versions, see [TKE Kubernetes Revision Version History](https://intl.cloud.tencent.com/document/product/457/9315).

### Another add-on holding the iptables lock for too long

#### Sample error message
```shell
Failed to ensure that filter chain KUBE-SERVICES exists: error creating chain "KUBE-EXTERNAL-SERVICES": exit status 4: Another app is currently holding the xtables lock. Stopped waiting after 5s.
```

#### Cause
1. When writing iptables rules to the kernel, iptables commands (such as `iptables-restore`) will use a file lock for sync to avoid concurrent writes of multiple instances. When `iptables-restore` is executed, it tries getting a file lock. If the lock is held by another process, `iptables-restore` will be blocked for a certain period of time (subject to the `-w` value, which is five seconds by default) before getting the lock. It will continue after getting the lock or exit.
2. The error indicates that the iptables file lock is held by another add-on for more than five seconds.

#### Fix guide
Reduce the time when other add-ons hold the iptables file lock as much as possible. In particular, the NetworkPolicy (kube-router) add-on provided on the add-on management page in the TKE console on an earlier version holds the iptables lock for a long time. You can upgrade it to the latest version `v1.3.2`.

---
## kube-proxy to kube-apiserver connection exception

#### Sample error message
```shell
Failed to list *core.Endpoints: Stream error http2.StreamError{StreamID:0xea1, Code:0x2, Cause:error(nil)} when reading response body, may be caused by closed connection. Please retry.
```

#### Cause
There is a bug when Kubernetes on an earlier version calls the go HTTP/2 package, which causes the client to use a disabled connection of the API server. When this bug occurs in kube-proxy, rule sync will fail. For more information, see [(1.17) Kubelet won't reconnect to Apiserver after NIC failure (use of closed network connection) #87615](https://github.com/kubernetes/kubernetes/issues/87615) and [Enables HTTP/2 health check #95981](https://github.com/kubernetes/kubernetes/pull/95981).

#### Fix guide
Upgrade kube-proxy. Below is the sample logic:
<table>
<thead>
  <tr>
    <th>TKE Cluster Version</th>
    <th>Fix Policy</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>&gt; 1.18</td>
    <td>No fixes are required, as the problem doesn't exist.</td>
  </tr>
  <tr>
    <td>1.18</td>
    <td>Upgrade kube-proxy to v1.18.4-tke.26 or later.</td>
  </tr>
  <tr>
    <td>&lt; 1.18</td>
    <td>Upgrade the TKE cluster.</td>
  </tr>
</tbody>
</table>

>? For more information on the latest TKE versions, see [TKE Kubernetes Revision Version History](https://intl.cloud.tencent.com/document/product/457/9315).

## kube-proxy panicked after the first startup and became normal after restart
#### Sample error message
```
panic: runtime error: invalid memory address or nil pointer dereference
[signal SIGSEGV: segmentation violation code=0x1 addr=0x50 pc=0x1514fb8]
```

#### Cause
1. The community code of kube-proxy has a bug, where the kernel module for statistics loading is missing during initialization, leading to the use of uninitialized variables.
2. The log is not detailed enough and failed to output the result regarding whether the IPVS mode can be used. For more information, see [kube-proxy panics with SIGSEGV on first run #89729](https://github.com/kubernetes/kubernetes/issues/89729), [Do not forget recording loaded modules #89823](https://github.com/kubernetes/kubernetes/pull/89823), and [ipvs: log err from CanUseIPVSProxier #89785](https://github.com/kubernetes/kubernetes/pull/89785).

#### Fix guide
Upgrade kube-proxy. Below is the sample logic:
<table>
<thead>
  <tr>
    <th>TKE Cluster Version</th>
    <th>Fix Policy</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>&gt; 1.18</td>
    <td>No fixes are required, as the problem doesn't exist.</td>
  </tr>
  <tr>
    <td>1.18</td>
    <td>Upgrade kube-proxy to v1.18.4-tke.26 or later.</td>
  </tr>
  <tr>
    <td>&lt; 1.18</td>
    <td>No fixes are required, as the problem doesn't exist.</td>
  </tr>
</tbody>
</table>

>? For more information on the latest TKE versions, see [TKE Kubernetes Revision Version History](https://intl.cloud.tencent.com/document/product/457/9315).

---
## kube-proxy kept panicking
#### Sample error message
```shell
Observed a panic: "slice bounds out of range" (runtime error: slice bounds out of range)
```

#### Cause
There is a bug in the community code of kube-proxy. When `iptables-save` is executed, the standard output and standard error are targeted at the same buffer, and the sequence of the two is uncertain, leading to an unexpected data format in the buffer and thereby a panic during processing. For more information, see [kube-proxy panics when parsing iptables-save output #78443](https://github.com/kubernetes/kubernetes/issues/78443) and [Fix panic in kube-proxy when iptables-save prints to stderr #78428](https://github.com/kubernetes/kubernetes/pull/78428).

#### Fix guide
 Upgrade kube-proxy. Below is the sample logic:
<table>
<thead>
  <tr>
    <th>TKE Cluster Version</th>
    <th>Fix Policy</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>&gt; 1.14</td>
    <td>No fixes are required, as the problem doesn't exist.</td>
  </tr>
  <tr>
    <td>1.14</td>
    <td>Upgrade kube-proxy to v1.14.3-tke.27 or later.</td>
  </tr>
  <tr>
    <td>1.12</td>
    <td>Upgrade kube-proxy to v1.12.4-tke.31 or later.</td>
  </tr>
  <tr>
    <td>&lt; 1.12</td>
    <td>No fixes are required, as the problem doesn't exist.</td>
  </tr>
</tbody>
</table>

>? For more information on the latest TKE versions, see [TKE Kubernetes Revision Version History](https://intl.cloud.tencent.com/document/product/457/9315).
---

## kube-proxy occupied high CPU periodically in IPVS mode

#### Cause
This is because kube-proxy frequently refreshes the node Service forwarding rules, specifically:
- kube-proxy frequently performs periodic rule syncs.
- The business Service or Pod is frequently changed.

#### Fix guide
If the problem is caused by frequent periodic rule syncs by kube-proxy, you need to modify relevant parameters. Below are default parameters of kube-proxy on an earlier version:
```yaml
--ipvs-min-sync-period=1s (minimum refresh interval of one second)
--ipvs-sync-period=5s (periodic refresh every five seconds)
```
Therefore, kube-proxy refreshes the node iptables rules once every five seconds, consuming many CPU resources. You can change the configuration to:
```yaml
--ipvs-min-sync-period=0s (real-time refresh upon event occurrence)
--ipvs-sync-period=30s (periodic refresh every 30 seconds) 
```
The above configured values are default values and can be configured as needed.
