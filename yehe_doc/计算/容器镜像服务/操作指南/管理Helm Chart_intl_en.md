## Scenario
Tencent Container Registry (TCR) can host Helm charts to meet users' requirements for hosting and distribution of cloud native applications. You can manage both container images and Helm charts in the same namespace so that cloud native deliverables of both container images and Helm charts can be used in a business project.

Currently, only TCR Enterprise Edition instances support Helm chart hosting and the use of a Helm client to upload and download Helm charts. Helm chart repositories inherit the public or private attribute from their namespaces, and no extra configuration is needed. In terms of permission management, Helm charts and container images share the **repository** resource type. That is, the resource description `qcs::tcr:$region:$account:repository/tcr-xxxxxx/project-a/*` contains all image repositories and Helm charts in the "project-a" namespace. You can flexibly use these image repositories and Helm charts during resource permission management. 


## Prerequisites
Before uploading and managing Helm charts in a TCR Enterprise Edition instance, complete the following tasks:
- [Create an Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/35486).
- If you are using a sub-account, grant the sub-account operation permissions for the corresponding instance in advance. For more information, see Examples of Enterprise Edition Authorization Schemes.

## Procedure
### Configuring and installing the Helm client
1. Download the specified [Helm client](https://github.com/helm/helm/releases) from the official Helm project and install it.
   Note that, if you wish to use Helm in Tencent Kubernetes Engine (TKE), you need to select the v2.10.0 version. You can run the `helm version -c` command to check the version of the installed client.
   ```
    # The Linux platform is selected by default. If you install the client on other platforms, download the installation package corresponding to this platform.
    
    # Decompress the installation package.
    tar -zxvf helm-v2.10.0-linux-amd64.tgz
    # Move the installation package to the specified location.
    mv linux-amd64/helm /usr/local/bin/helm 
   ```
2. Install the Helm plugin.
   You need to install Git and the Helm-Push plugin before using the Helm client to upload charts.
    ```
    # Install the Helm plugin.
    helm plugin install https://github.com/chartmuseum/helm-push
    ```
3. Initialize Helm.
    - Initialize Helm on the container cluster node. By default, Helm is activated and Tiller is installed.
        ```
        helm init --client-only --skip-refresh
        ```
    - Tiller is not installed in your Kubernetes cluster.
        ```
        helm init --skip-refresh   
        ```
### Adding a Helm repository
1. Obtain the access credentials for the current instance. The access credential is the username plus the temporary password, which is consistent with the credential used for Docker login.
2. Add the namespace, which is used to manage Helm charts, to the local Helm repository.
   ```
    helm repo add $instance-$namespace https://$instance.tencentcloudcr.com/chartrepo/$namesapce --username $username --password $instance-token
   ```
    "$instance-$namespace" is the name of the Helm repository. We recommend that you name this Helm repository using the following format to differentiate instances and namespaces: instance name + namespace name. `https://$instance.tencentcloudcr.com/chartrepo/$namespace` is the remote address of the Helm repository, where "$instance" and "$namespace" must be replaced by the actual instance name and namespace name. "$username" and "$instance-token" are the username and temporary password obtained in Step 1.
    After the namespace is added, the following prompt is displayed:
    ```
    "$instance-$namespace" has been added to your repositories
    ```

### Pushing Helm charts
The installed Helm-Push plug-in can use the `helm push` command to push Helm charts to a specified repository. Both directories and compressed packages can be uploaded.
In the following example, tcr-chart-demo 1.0.0 is uploaded to the repository added in the previous step.
```
# Create a local chart.
helm create tcr-chart-demo
# Push the chart directory, where "$instance-$namespace" is the name of the added local repository.
helm push tcr-chart-demo $instance-$namespace
# Push the chart package, where "$instance-$namespace" is the name of the added local repository.
helm push tcr-chart-demo-1.0.0.tgz $instance-$namespace 
```

### Pulling Helm charts
```
# Pull Helm charts of a specified version.
helm fetch <Local repository name>/<Chart name> --version <Chart version>
```
In the following example, tcr-chart-demo 1.0.0 in the "project-a" namespace is pulled from the "tcr-demo" Enterprise Edition instance.
```
helm fetch tcr-demo-project-a/tcr-chart-demo --version 1.0.0
```
### Managing Helm charts on the console
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Helm Chart** in the left sidebar.
2. On the "Helm Chart" page, you can view the list of Helm charts in the current instance. To change the instance, select the desired instance name from the "Instance Name" drop-down list at the top of the page.
   The Helm chart list provides the following information and operations:
   - Name: name of a Helm chart. You can click a chart name to go to the details page of this chart.
   - Namespace: namespace to which a Helm chart belongs.
   - Create Time: time when the Helm chart is pushed to the repository for the first time.
   - Operation: you can click **Delete** to delete the current repository.
3. Click a specific chart repository to go to the details page. On the details page, you can view and manage chart versions. In addition, you can view the details of the files contained in each chart version on the **Basic Information** tab.