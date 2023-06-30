## Operation Scenario
The dynamic admission controller Webhook can change the request object or completely reject a request during access authentication. The way it calls the Webhook service makes it independent of cluster components.
The dynamic admission controller has a high degree of flexibility and allows you to configure various custom admission control settings. The following figure shows the position of dynamic admission control in the API request call chain. For more information, visit the [official Kubernetes website](https://kubernetes.io/blog/2019/03/21/a-guide-to-kubernetes-admission-controllers/).
![admission-controller-phases](https://main.qcloudimg.com/raw/85a757f42598097d24f3eae3736261b9.png)
As shown in the figure, dynamic admission control is divided into two phases: Mutating and Validating. During the Mutating phase, incoming requests can be modified. Subsequently, during the Validating phase, the dynamic admission controller validates incoming requests to determine whether to allow them to pass. These two phases can be used independently or in combination.

This document introduces a simple use case for calling the dynamic admission controller in TKE. You can refer to this document and take your actual requirements into consideration when performing the relevant operations.

## Directions
### Viewing and verifying the plug-in
The existing TKE cluster versions (1.10.5 and later) enable the [validating admission webhook](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#validatingadmissionwebhook) and [mutating admission webhook](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#mutatingadmissionwebhook) APIs by default. If your cluster version is earlier than 1.10.5, you can run the following command to check whether the plug-in has been enabled in your current cluster.
```
kube-apiserver -h | grep enable-admission-plugins
```
If the returned result includes `MutatingAdmissionWebhook` and `ValidatingAdmissionWebhook`, the dynamic admission controller is already enabled in the cluster, as shown in the figure below:
![image-20201117102438615](https://main.qcloudimg.com/raw/534694e9a6976d0ec18d2e1074932126.png)

### Certificate issuance
To ensure that the dynamic admission controller calls a trustworthy Webhook server, it needs to call the Webhook service (TLS certification) via HTTPS. Therefore, you need to issue a certificate to the Webhook server. During registration of the dynamic admission controller Webhook, you need to bind the `caBundle` field (`caBundle` field in the resource list of `ValidatingWebhookConfiguration` and `MutatingAdmissionWebhook`) with a trustworthy certificate authority (CA) to verify whether the Webhook server certificate is trustworthy. This document introduces two recommended methods for issuing certificates: [making a self-signed certificate](#Method1) and [using the K8S CSR API to issue a certificate](#Method2).
>! When `ValidatingWebhookConfiguration` and `MutatingAdmissionWebhook` use the `clientConfig.service` configuration (and the Webhook service is in the cluster), the domain name of the certificate issued to the server must be `<svc_name>.<svc_namespace>.svc`.

<span id="Method1"></span>
#### Method 1: making a self-signed certificate 
This method is not dependent on Kubernetes clusters and is relatively independent. It’s similar to the way in which websites make their own self-signed certificates. Currently, many tools can be used to make a self-signed certificate. This document uses OpenSSL as an example. The procedure is as follows:
1. Run the following command to generate a `ca.key` with 2048 key digits.
```bash
openssl genrsa -out ca.key 2048
```
2. Run the following command to generate a `ca.crt` based on the `ca.key`.
"webserver.default.svc" is the domain name of the Webhook server in the cluster. The `-days` parameter is used to specify the validity period of the certificate.
```bash
openssl req -x509 -new -nodes -key ca.key -subj "/CN=webserver.default.svc" -days 10000 -out ca.crt
```
3. Run the following command to generate a `server.key` with 2048 key digits.
```bash
openssl genrsa -out server.key 2048
```
4. Create the configuration file `csr.conf` used to generate a certificate signature request (CSR). See the sample below: 
```text
[ req ]
default_bits = 2048
prompt = no
default_md = sha256
distinguished_name = dn
[ dn ]
C = cn
ST = shaanxi
L = xi'an
O = default
OU = websever
CN = webserver.default.svc

subjectAltName = @alt_names

[ alt_names ]
DNS.1 = webserver.default.svc

[ v3_ext ]
authorityKeyIdentifier=keyid,issuer:always
basicConstraints=CA:FALSE
keyUsage=keyEncipherment,dataEncipherment
extendedKeyUsage=serverAuth,clientAuth
subjectAltName=@alt_names
```
5. Run the following command to generate a CSR based on the configuration file `csr.conf`.
```bash
openssl req -new -key server.key -out server.csr -config csr.conf
```
6. Run the following commands to use `ca.key`, `ca.crt`, and `server.csr` to issue the generated server certificate (x509 signature).

```bash
openssl x509 -req -in server.csr -CA ca.crt -CAkey ca.key \
 -CAcreateserial -out server.crt -days 10000 \
 -extensions v3_ext -extfile csr.conf
```
7. Run the following command to view the Webhook server certificate.
```bash
openssl x509  -noout -text -in ./server.crt
```
The generated certificates and key files are described as follows:
- `ca.crt`: the CA certificate
- `ca.key`: the CA certificate key, used to issue a server certificate
- `server.crt`: the issued server certificate
- `server.key`: the issued server certificate key

<span id = "Method2"></span>
#### Method 2: using the K8S CSR API to issue a certificate
You can also use the Kubernetes CA system to issue a certificate. You can execute the following script to use the Kubernetes cluster root certificate and root key to issue a trustworthy certificate user.
>! The username must be the domain name of the Webhook service in the cluster.

```bash
USERNAME='webserver.default.svc' # Set the username to be created to the domain name of the Webhook service in the cluster
# Use OpenSSL to generate a self-signed certificate key
openssl genrsa -out ${USERNAME}.key 2048
# Use OpenSSL to generate a self-signed CSR file, with CN indicating the user name and O indicating the group name
openssl req -new -key ${USERNAME}.key -out ${USERNAME}.csr -subj "/CN=${USERNAME}/O=${USERNAME}" 
# Create a Kubernetes CSR
cat <<EOF | kubectl apply -f -
apiVersion: certificates.k8s.io/v1beta1
kind: CertificateSigningRequest
metadata:
   name: ${USERNAME}
spec:
   request: $(cat ${USERNAME}.csr | base64 | tr -d '\n')
   usages:
   - digital signature
   - key encipherment
   - server auth
EOF
# Approve the certificate as trustworthy
kubectl certificate approve ${USERNAME}
# Obtain the self-signed certificate CRT
kubectl get csr ${USERNAME} -o jsonpath={.status.certificate} > ${USERNAME}.crt
```
 - `${USERNAME}`.crt: the Webhook server certificate
 -  `${USERNAME}`.key: the Webhook server certificate key


## Use Cases
This document uses `ValidatingWebhookConfiguration` resources to illustrate how to call the dynamic admission controller Webhook.
To ensure accessibility, the sample code is forked from the [original code library](https://github.com/larkintuckerllc/hello-dynamic-admission-control.git) to implement a simple API for dynamic admission Webhook requests and responses. For the detailed API format, see [Webhook request and response](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#request). The sample code can be obtained in [Sample Code](https://github.com/imjokey/hello-dynamic-admission-control). This document uses it as the Webhook server code.

1. Prepare the `caBundle` content corresponding to the actual certificate issuance method.
 - If you use method 1 to issue a certificate, run the following command to use `base64` to encode `ca.crt` and generate the `caBundle` field content.
```bash
cat ca.crt | base64 --wrap=0 
```
 - If you use method 2 to issue a certificate, the cluster root certificate is the `caBundle` field content. The procedure for obtaining it is as follows:
    1. Log in to the TKE console and click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** in the left sidebar.
    2. On the "Cluster Management" page, click the ID of the target cluster.
    3. On the cluster details page, click **Basic Information** on the left.
    4. On the "Basic Information" page, obtain the `clusters.cluster[].certificate-authority-data` field in "Kubeconfig" in the "Cluster APIServer Info" module. This field has been encoded in `base64`, and no further processing is needed.
2. Copy the generated `ca.crt` (CA certificate), `server.crt` (HTTPS certificate), and `server.key` (HTTPS key) to the main directory of the project, as shown in the figure below:
![image-20201117131409795](https://main.qcloudimg.com/raw/61d2ad7f881606af8271abfbbb78d88b.png)
3. Modify the Dockerfile in the project and add three certificate files to the container working directory, as shown in the figure below:
![image-20201117131639307](https://main.qcloudimg.com/raw/a2faa20c9c1db85075458bde232840ea.png)
4. Run the following command to build a Webhook server image.
```
docker build -t webserver .
```
5. Deploy a Webhook backend service with the domain name of "weserver.default.svc" and modify the adapted `controller.yaml`, as shown in the figure below:
![image-20201117131843384](https://main.qcloudimg.com/raw/4d06816731be0b1ea3478a5fc3938f8b.png)
6. Register and create resources of the `ValidatingWebhookConfiguration` type, and modify the `admission.yaml` file in the adapted project, as shown in the figure below:
The Webhook triggering rule configured in this sample is as follows: when an API of `pods` type and version "v1" is created, Webhook is triggered. The configuration of `clientConfig` corresponds to the above Webhook backend service created in the cluster. The `caBundle` field content is the content of the `ca.crt` obtained in method 1.
![](https://main.qcloudimg.com/raw/239814926510536dc17619bd77d8acad.png)
7. After registration, create test resources of the Pod type and the API version of "v1", as shown in the figure below:
![image-20201117132642385](https://main.qcloudimg.com/raw/cc2b9a842085f319a42b54ec7366936a.png)  
8. The test code prints the request log. You can view the Webhook server log to see that the dynamic admission controller has triggered a webhook call, as shown in the figure below:
![image-20201117132840262](https://main.qcloudimg.com/raw/877c7eb459fff8f3e8e4a56c6893d0f5.png)
9. At this moment, you can see that the test pod has been created successfully. As the test Webhook server code includes the `allowed: true` configuration item, the test pod has been created successfully, as shown in the figure below:
![](https://main.qcloudimg.com/raw/1d46955ef82a072194a80b9c434cbd89.png)
For further verification, you can change "allowed" to "false" and then repeat the above steps to rebuild a Webserver server image and redeploy `controller.yaml` and `admission.yaml` resources. If the request of your reattempt to create pods resources is intercepted by the dynamic admission controller, then the configured dynamic admission policy has taken effect, as shown in the figure below:
   ![image-20201117133504920](https://main.qcloudimg.com/raw/3df15331208bf316fc06e432598658ae.png)

## Summary
This document mainly introduces the concept and functionality of the dynamic admission controller Webhook, as well as how to issue certificates needed by the dynamic admission controller in a TKE cluster. This document also describes a simple use case for configuring and using the dynamic admission Webhook feature.



## References
- [Kubernetes Dynamic Admission Control by Example](https://codeburst.io/kubernetes-dynamic-admission-control-by-example-d8cc2912027c )
- [Dynamic Admission Control](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/)
