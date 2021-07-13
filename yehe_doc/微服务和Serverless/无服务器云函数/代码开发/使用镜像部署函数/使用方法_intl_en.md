This document describes how to use image to deploy function via the console.

## Prerequisites

SCF supports the image repositories of TCR Enterprise Edition and Personal Edition. You can select the image repository as needed.
- For how to purchase the TCR Enterprise Edition instance, please see [Quick Start](https://intl.cloud.tencent.com/document/product/1051/35484).
- For how to use the image repository of TCR Personal Edition, please see [Getting Started](https://intl.cloud.tencent.com/document/product/1051/38866).


## Creating functions via the console

### Image pushing

Run the following code to push the built image to your image repository.
```
# Switch to the file download directory
cd /opt

# Download Demo
git clone https://github.com/awesome-scf/scf-custom-container-code-snippet.git

# Log in to the image repository. Replace $YOUR_REGISTRY_URL with your image repository, and replace $USERNAME and $PASSWORD with your login credentials respectively.
docker login $YOUR_REGISTRY_URL --username $USERNAME --password $PASSWORD

# Build images. Replace $YOUR_IMAGE_NAME with your image address.
docker build -t $YOUR_IMAGE_NAME .

# Push images
docker push  $YOUR_IMAGE_NAME
```

### Creating a function

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and select **Function Service** in the left sidebar.
2. Choose a region at the top of the **Function Service** page and click **Create** to start creating a function.
3. Select **Custom** for **Creation Method**, and enter the basic configurations.
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Operation</th>
</tr>
</thead>
<tbody><tr>
<td>Function Type</td>
<td>Select “Event Function” or “Web Function”.</td>
</tr>
<tr>
<td>Function Name</td>
<td>Enter the function name.</td>
</tr>
<tr>
<td>Region</td>
<td>Select the region where the function is deployed, which must be the same as the region where the image repository is located.</td>
</tr>
<tr>
<td>Deployment Mode</td>
<td>Select “Image”.</td>
</tr>
<tr>
<td>Image</td>
<td>Select the image repository of the Personal or Enterprise Edition that you created.</td>
</tr>
<tr>
<td>Image Tag</td>
<td>Select the image tag.<br>If it is left empty, the latest version of the image will be used by default.</td>
</tr>
<tr>
<td>Command</td>
<td>Enter the container's startup command, such as <code>"nginx"</code>.<br>This parameter is optional. If you do not specify it, the Entrypoint / CMD in the image will be used by default.</td>
</tr>
<tr>
<td>Args</td>
<td>Enter the container’s startup parameter, such as <code>"-args","value"</code>. This parameter is optional. If you do not specify it, the CMD in the image will be used by default.</td>
</tr>
</tbody></table>
4. Click **Complete**.
