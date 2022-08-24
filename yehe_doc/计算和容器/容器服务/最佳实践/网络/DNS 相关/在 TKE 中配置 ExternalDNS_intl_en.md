
This document introduces how to configure ExternalDSN in a Tencent Cloud TKE cluster.

## What is ExternalDNS?

ExternalDNS can sync the public Kubernetes Services and Ingress to the DNS provider.

Inspired by Kubernetes DNS, Kubernetes' cluster-internal DNS server, ExternalDNS makes Kubernetes resources discoverable via public DNS servers. Like KubeDNS, it retrieves a list of resources (Services, Ingresses, etc.) from the Kubernetes API to determine a desired list of DNS records. Unlike KubeDNS, however, it's not a DNS server itself, but merely configures other DNS providers accordingly. For more information, see [ExternalDNS Readme](https://github.com/kubernetes-sigs/external-dns).

## Directions

### Configuring CAM Permissions for the API Key

Go to the Tencent Cloud [CAM console](https://console.cloud.tencent.com/cam/overview) and get the SecretId and SecretKey of the API key. Make sure the current user is assigned with the following permissions.

```json
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "dnspod:ModifyRecord",
                "dnspod:DeleteRecord",
                "dnspod:CreateRecord",
                "dnspod:DescribeRecordList",
                "dnspod:DescribeDomainList"
            ],
            "resource": [
                "*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "privatedns:DescribePrivateZoneList",
                "privatedns:DescribePrivateZoneRecordList",
                "privatedns:CreatePrivateZoneRecord",
                "privatedns:DeletePrivateZoneRecord",
                "privatedns:ModifyPrivateZoneRecord"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```

### Deploying ExternalDNS Service

#### Configuring PrivateDNS or DNSPod

Tencent Cloud DNSPod provides free intelligent resolution services to all types of domain names. It features massive processing capability, flexible scalability and superior security, providing stable, fast and secure domain name resolution for your sites.

Tencent Cloud [Private DNS](https://www.tencentcloud.com/document/product/1097) is a private domain resolution and management service based on Tencent Cloud Virtual Private Cloud (VPC), providing you with safe, stable, and efficient private network resolution service. It supports quick building of a DNS system in VPCs to fulfill your needs.

* To use private network DNS in Tencent Cloud environment: 
  * Add the following parameter in the YAML file: `--tencent-cloud-zone-type=private`   
  * Create a DNS domain in the PrivateDNS console. The DNS records are included in the DNS domain name records.
* To use public network DNS in Tencent Cloud environment: 
  * Add the following parameter in the YAML file: `--tencent-cloud-zone-type=public`   
  * Create a DNS domain in the [DNSPod console](https://console.dnspod.cn). The DNS records are included in the DNS domain name records.

#### Deploying resource objects in the Kuberentes cluster

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: external-dns
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: external-dns
rules:
- apiGroups: [""]
  resources: ["services","endpoints","pods"]
  verbs: ["get","watch","list"]
- apiGroups: ["extensions","networking.k8s.io"]
  resources: ["ingresses"] 
  verbs: ["get","watch","list"]
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: external-dns-viewer
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: external-dns
subjects:
- kind: ServiceAccount
  name: external-dns
  namespace: default
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: external-dns
data:
  tencent-cloud.json: |
    {
      "regionId": "ap-shanghai", # (Required) ID of the region where the cluster locates
      "secretId": "******",  
      "secretKey": "******",
      "vpcId": "vpc-******" (Required), ID of the VPC where the cluster is deployed
    }
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: external-dns
spec:
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: external-dns
  template:
    metadata:
      labels:
        app: external-dns
    spec:
      containers:
      - args:
        - --source=service
        - --source=ingress
        - --domain-filter=external-dns-test.com # Make ExternalDNS see only the hosted zones matching provided domain, omit to process all available hosted zones
        - --provider=tencentcloud
        - --policy=sync # Set it to `upssert-only` to prevent ExternalDNS from deleting any records
        - --tencent-cloud-zone-type=private # Only look at private hosted zones. To use public DNS service, set it to `public`.
        - --tencent-cloud-config-file=/etc/kubernetes/tencent-cloud.json
        image: ccr.ccs.tencentyun.com/tke-market/external-dns:v1.0.0
        imagePullPolicy: Always
        name: external-dns
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /etc/kubernetes
          name: config-volume
          readOnly: true
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      serviceAccount: external-dns
      serviceAccountName: external-dns
      terminationGracePeriodSeconds: 30
      volumes:
      - configMap:
          defaultMode: 420
          items:
          - key: tencent-cloud.json
            path: tencent-cloud.json
          name: external-dns
        name: config-volume
```

## Example

Creating a Service named “nginx”

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx
  annotations:
    external-dns.alpha.kubernetes.io/hostname: nginx.external-dns-test.com # Public domain name address
    external-dns.alpha.kubernetes.io/internal-hostname: nginx-internal.external-dns-test.com # Private domain name address
    external-dns.alpha.kubernetes.io/ttl: "600"
spec:
  type: LoadBalancer
  ports:
  - port: 80
    name: http
    targetPort: 80
  selector:
    app: nginx
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - image: nginx
        name: nginx
        ports:
        - containerPort: 80
          name: http
```

- `nginx.external-dns-test.com` will record the service's loadbalancer VIP.
- `nginx-internal.external-dns-test.com` will record the service's ClusterIP. The TTL of all DNS records is 600.

#### Verification

A Service named “nginx” is created with the ClusterIP `192.168.254.214` and Loadbalancer VIP `129.211.179.31`. As shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/9cf1709ac78fa73a9ff28c9b4feb72f8.png)


Log in to a node in the same VPC as the cluster. PING the domain name in the annotation of nginx service. The domain name will be resolved to the ClusterIP and Loadbalancer VIP. As shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/dfaec4597cf7dd9c9702cef897031b51.png)
