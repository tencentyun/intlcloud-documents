Pod security groups integrate CVM security groups and Kubernetes Pods. You can use CVM security groups to define rules, so as to allow the inbound and outbound network traffic of Pods running on different TKE nodes (currently, only super nodes are supported, and general nodes will be supported).

## Limits

Consider the following limits before using security groups for Pods:
- Pods must run in TKE clusters on v1.20 or later.
- Only super nodes are supported for Pod security groups, and more node types will be released.
- Pod security groups cannot be used together with dual-stack clusters.
- Super nodes are only supported in some regions. For more information, see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/457/41125).

## Enabling Security Group Capabilities for Pods

### Installing the add-on

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Install the `SecurityGroupPolicy` add-on for the cluster.
  - If you haven't created a cluster yet, you can install the `SecurityGroupPolicy` add-on during creation. For detailed directions, see [Add-On Lifecycle Management](https://intl.cloud.tencent.com/document/product/457/38705).
  - To enable security group capabilities for Pods in a created cluster, install the `SecurityGroupPolicy` add-on on the **Add-On Management** page. For detailed directions, see [Add-On Lifecycle Management](https://intl.cloud.tencent.com/document/product/457/38705).
3. On the **Add-On Management** page, view the add-on status. If the status is **Success**, the add-on has been deployed, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/dce3dbe8df425c3b409d49bc9028a9ef.png)
4. On the super node page, verify that your TKE general cluster contains a super node. Currently, you can enable security group capabilities only for Pods scheduled to a super node.
![](https://qcloudimg.tencent-cloud.cn/raw/de96ba5d58bbb29a6d60cc387fc8e746.png)

## Deploying the Sample Application

To use security groups for Pods, you must deploy [SecurityGroupPolicy](#sgp) in your cluster. The following describes how to use the security group policy for a Pod via CloudShell. Unless otherwise stated, the steps should be performed on the same terminal, as the variables involved don't apply to different terminals.

### Deploying the sample Pod with a security group

1. Create a security group to be used with the Pod. The following describes how to create a simple security group and is for reference only. The rules may differ in a production cluster.
    a. Search for the VPC and security group ID of the cluster. Replace `my-cluster` with the actual value.
    ```shell
    my_cluster_name=my-cluster
    my_cluster_vpc_id=$(tccli tke DescribeClusters --cli-unfold-argument --ClusterIds $my_cluster_name --filter Clusters[0].ClusterNetworkSettings.VpcId | sed 's/\"//g')
    my_cluster_security_group_id=$(tccli vpc DescribeSecurityGroups --cli-unfold-argument --Filters.0.Name security-group-name --Filters.0.Values tke-worker-security-for-$my_cluster_name --filter SecurityGroupSet[0].SecurityGroupId | sed 's/\"//g')
    ```
    b. Create a security group for your Pod. Replace `my-pod-security-group` with the actual value. Record the security group ID returned by the command for further use.
    ```shell
    my_pod_security_group_name=my-pod-security-group
    tccli vpc CreateSecurityGroup --GroupName "my-pod-security-group" --GroupDescription "My pod security group"
    my_pod_security_group_id=$(tccli vpc DescribeSecurityGroups --cli-unfold-argument --Filters.0.Name security-group-name --Filters.0.Values my-pod-security-group --filter SecurityGroupSet[0].SecurityGroupId | sed 's/\"//g')
    echo $my_pod_security_group_id
    ```
    c. Allow the traffic over TCP and UDP on port 53 from the Pod security group created in the previous step to the cluster security group, so that the Pod can access the application through the domain name.
    ```shell
    tccli vpc CreateSecurityGroupPolicies --cli-unfold-argument --SecurityGroupId $my_cluster_security_group_id --SecurityGroupPolicySet.Ingress.0.Protocol UDP --SecurityGroupPolicySet.Ingress.0.Port 53 --SecurityGroupPolicySet.Ingress.0.SecurityGroupId $my_pod_security_group_id --SecurityGroupPolicySet.Ingress.0.Action ACCEPT
    tccli vpc CreateSecurityGroupPolicies --cli-unfold-argument --SecurityGroupId $my_cluster_security_group_id --SecurityGroupPolicySet.Ingress.0.Protocol TCP --SecurityGroupPolicySet.Ingress.0.Port 53 --SecurityGroupPolicySet.Ingress.0.SecurityGroupId $my_pod_security_group_id --SecurityGroupPolicySet.Ingress.0.Action ACCEPT
    ```
    d. Allow the inbound traffic over any protocol and port from the Pod associated with the security group to the Pod associated with any security group, and allow the outbound traffic over any protocol and port from the Pod associated with the security group.
    ```shell
    tccli vpc CreateSecurityGroupPolicies --cli-unfold-argument --SecurityGroupId $my_pod_security_group_id --SecurityGroupPolicySet.Ingress.0.Protocol ALL --SecurityGroupPolicySet.Ingress.0.Port ALL --SecurityGroupPolicySet.Ingress.0.SecurityGroupId $my_pod_security_group_id --SecurityGroupPolicySet.Ingress.0.Action ACCEPT
    tccli vpc CreateSecurityGroupPolicies --cli-unfold-argument --SecurityGroupId $my_pod_security_group_id --SecurityGroupPolicySet.Egress.0.Protocol ALL --SecurityGroupPolicySet.Egress.0.Port ALL --SecurityGroupPolicySet.Egress.0.Action ACCEPT
    ```

2. Create a Kubernetes namespace to deploy resources.
  ```shell
  kubectl create namespace my-namespace
  ```
[](id:sgp)
3. Deploy the `SecurityGroupPolicy` in your cluster.
    a. Save the following sample security policy as `my-security-group-policy.yaml`. If you prefer to select a Pod by service account tag, you can replace `podSelector` with `serviceAccountSelector`, and you must specify a selector. If you specify multiple security groups, all their rules will take effect for the selected Pod. Replace `$my_pod_security_group_id` with the security group ID recorded in the previous step.
    ```yaml
    apiVersion: vpcresources.tke.cloud.tencent.com/v1beta1
    kind: SecurityGroupPolicy
    metadata:
      name: my-security-group-policy
      namespace: my-namespace
    spec:
      podSelector: 
        matchLabels:
          app: my-app
      securityGroups:
        groupIds:
          - $my_pod_security_group_id
    ```
    <dx-alert infotype="notice" title="">
    Consider the following limits when specifying one or multiple security groups for the Pod:
- They must exist.
- They must allow inbound requests from cluster security groups (for kubelet) and health checks configured for the Pod.
- Your CoreDNS Pod security groups must allow the inbound traffic over TCP and UDP on port 53 from Pod security groups.
- They must have necessary inbound and outbound rules to communicate with other Pods.


**A security group policy applies only to newly scheduled Pods and doesn't affect running Pods. To make it effective for existing Pods, you need to verify that the existing Pods meet the above limits before manually recreating it.**
</dx-alert>
    b. Deploy the policy.
    ```shell
    kubectl apply -f my-security-group-policy.yaml
    ```
4. To deploy the sample application, use the `my-app` match tag specified by using the `podSelector` in the previous step.
    a. Save the following content as `sample-application.yaml`.
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: my-deployment
      namespace: my-namespace
      labels:
        app: my-app
    spec:
      replicas: 2
      selector:
        matchLabels:
          app: my-app
      template:
        metadata:
          labels:
            app: my-app
        spec:
          terminationGracePeriodSeconds: 120
          containers:
          - name: nginx
            image: nginx:latest
            ports:
            - containerPort: 80
          nodeSelector:
            node.kubernetes.io/instance-type: eklet
          tolerations: 
          - effect: NoSchedule
            key: eks.tke.cloud.tencent.com/eklet
            operator: Exists
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: my-app
      namespace: my-namespace
      labels:
        app: my-app
    spec:
      selector:
        app: my-app
      ports:
        - protocol: TCP
          port: 80
          targetPort: 80
    ```

    b. Run the following command to deploy the application. During deployment, Pods will be preferably scheduled to super nodes, and the security group specified in the previous step will be applied to the Pod.
    ```shell
    kubectl apply -f sample-application.yaml
    ```
>! If you don't use `nodeSelector` to preferably schedule the Pod to a super node, when it is scheduled to another node, the security group will not take effect, and `kubectl describe pod` will output "security groups is only support super node, node 10.0.0.1 is not super node".
>
5. View the Pod deployed by using the sample application. So far, the involved terminal is `TerminalA`.
  ```shell
  kubectl get pods -n my-namespace -o wide
  ```
  Below is the sample output:
  ```shell
  NAME                             READY   STATUS    RESTARTS   AGE   IP           NODE                             NOMINATED NODE   READINESS GATES
  my-deployment-866ffd8886-9zfrp   1/1     Running   0          85s   10.0.64.10   eklet-subnet-q21rasu6-8bpgyx9r   <none>           <none>
  my-deployment-866ffd8886-b7gzb   1/1     Running   0          85s   10.0.64.3    eklet-subnet-q21rasu6-8bpgyx9r   <none>           <none>
  ```

6. Go to any Pod on another terminal (`TerminalB`) and replace the Pod ID with the one returned in the previous step.
  ```shell
  kubectl exec -it -n my-namespace my-deployment-866ffd8886-9zfrp -- /bin/bash
  ```

7. Verify that the sample application works normally on `TerminalB`.
  ```shell
  curl my-app
  ```
  Below is the sample output:
  ```html
  <!DOCTYPE html>
  <html>
  <head>
  <title>Welcome to nginx!</title>
  ...
  ```
  You receive a response, as all Pods of the running application are associated with the security group you create, which contains the following rules:
	1. Allow all traffic between all Pods associated with the security group.
	2. Allow the DNS traffic from the security group to the cluster security group associated with your node. CoreDNS Pods are running on these nodes, and your Pod will search for `my-app` by domain name.

8. On `TerminalA`, delete the security group rule that allows DNS communication from the cluster security group.
  ```shell
  tccli vpc DeleteSecurityGroupPolicies --cli-unfold-argument --SecurityGroupId $my_cluster_security_group_id --SecurityGroupPolicySet.Ingress.0.Protocol UDP --SecurityGroupPolicySet.Ingress.0.Port 53 --SecurityGroupPolicySet.Ingress.0.SecurityGroupId $my_pod_security_group_id --SecurityGroupPolicySet.Ingress.0.Action ACCEPT
  tccli vpc DeleteSecurityGroupPolicies --cli-unfold-argument --SecurityGroupId $my_cluster_security_group_id --SecurityGroupPolicySet.Ingress.0.Protocol TCP --SecurityGroupPolicySet.Ingress.0.Port 53 --SecurityGroupPolicySet.Ingress.0.SecurityGroupId $my_pod_security_group_id --SecurityGroupPolicySet.Ingress.0.Action ACCEPT
  ```

9. On `TerminalB`, try accessing the application again.
  ```shell
  curl my-app
  ```
  The trial will fail, as the Pod cannot access the CoreDNS Pod, and the cluster security group no longer allows DNS communication from Pods associated with the security group.
  If you try using an IP to access the application, you will receive a response, as all ports allow the communication between Pods associated with the security group, and no domain name search is required.

10. After the trial, run the following command to delete the sample security group policy, application, and security group.
  ```
  kubectl delete namespace my-namespace
  tccli vpc DeleteSecurityGroup --cli-unfold-argument --SecurityGroupId $my_pod_security_group_id
  ```
