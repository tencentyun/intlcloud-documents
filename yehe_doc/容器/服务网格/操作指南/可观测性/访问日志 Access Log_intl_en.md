You can configure the output range and format of access logs (standard outputs of containers) of the data plane of a service mesh, and enable automatic collection of access logs to connect to Logset-Log Topic of Cloud Log Service (CLS). You can configure access logs when creating a mesh, and you can also modify access log configurations on the basic information page after the mesh is created.

## Configuring Access Logs

Currently, supported access log configurations are described as follows:

| Configuration Item | Description |
| ----- | ----- |
| Range | Data plane (gateway and Istio proxy sidecar) for which access log outputting is enabled. You can enable access logs of all data planes of a specific gateway and namespace or all data planes of the mesh to be outputted to standard outputs of containers. |
| Output format | Output fields and templates of access logs. The fields output in the default format are the fields output by Istio by default. Compared with the fields output in the default format, the fields output in the enhanced format are added with **Trace ID**. |
| Consumer end | Configure to collect access logs from the standard outputs of data plane containers to CLS. You need to select a CLS logset and log topic for storing access logs. You can choose to automatically create a logset/topic, or associate an existing logset/topic. An automatically created logset is named in the format of `{mesh ID}`. The name of an automatically created log topic contains a Tencent Cloud Mesh identifier, that is, the log topic is named in the format of `{mesh ID}-accesslog`. After the request for enabling collection of access logs to CLS is submitted, the log collection feature is enabled on clusters managed by the mesh. Then, you need to deploy the log collection component tke-log-agent (DaemonSet) on the clusters managed by the mesh, and configure collection rules and indexes of Tencent Cloud Mesh's access logs. This feature is based on the [log collection feature](https://intl.cloud.tencent.com/document/product/457/32419). Ensure that [CLS](https://intl.cloud.tencent.com/document/product/614) has been activated, and that the service role `TKE_QCSRole` of TKE has been associated with the preset policy `QcloudAccessForTKERoleInOpsManagement` for operations management of CLS. For more information, see [Description of Role Permissions Related to Service Authorization](https://intl.cloud.tencent.com/document/product/457/37808)|

- Configuring access logs during mesh creation
![](https://qcloudimg.tencent-cloud.cn/raw/7ba68b21574e5a2c0e59a53e3ab067a1.png)
- Configuring access logs after mesh creation
![](https://qcloudimg.tencent-cloud.cn/raw/c11333301f4b763497900dbcfa698c70.png)

## Viewing Access Logs

### Viewing access logs through standard outputs of containers

Access logs of the Tencent Cloud Mesh data plane are output to the standard outputs of containers. You can view access logs in the standard outputs of the istio-proxy container through your Kubernetes cluster API server.
```
kubectl -n {Namespace} logs {Pod name} -c istio-proxy  --tail 5
```

### Viewing access logs through CLS log search

If you have enabled consumer end configurations for access logs to collect the access logs of the Tencent Cloud Mesh data plane to CLS, you can select a corresponding log topic on the search and analysis page on the CLS console to view the access logs of the Tencent Cloud Mesh data plane. For details about CLS log search syntax, see [Overview and Syntax Rules](https://intl.cloud.tencent.com/document/product/614/37803).  
![](https://qcloudimg.tencent-cloud.cn/raw/fb1cefa3df09f04ea1a3e2ebd836dd5a.png)

