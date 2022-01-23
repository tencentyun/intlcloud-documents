This document describes how to use an image to deploy a function in the console.

## Prerequisites

SCF supports image repositories on TCR Personal Edition and Enterprise Edition. You can select an image repository as needed.
- Purchase a TCR Enterprise Edition instance. For more information, see [Quick Start](https://intl.cloud.tencent.com/document/product/1051/35484).
- Use a TCR Personal Edition image repository. For more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/1051/38866).


## Creating Function in Console

### Pushing image

Run the following code to push the built image to your image repository.
```
# Switch to the file download directory
cd /opt

# Download the demo
git clone https://github.com/awesome-scf/scf-custom-container-code-snippet.git

# Log in to the image repository. Please replace `$YOUR_REGISTRY_URL` with the address of your image repository and replace `$USERNAME` and `$PASSWORD` with your login credentials respectively
docker login $YOUR_REGISTRY_URL --username $USERNAME --password $PASSWORD

# Build the image. Please replace `$YOUR_IMAGE_NAME` with the address of your image
docker build -t $YOUR_IMAGE_NAME .

# Push the image
docker push  $YOUR_IMAGE_NAME
```

### Creating function

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and click **Function Service** on the left sidebar.
2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
3. Select **Custom Creation** for **Creation Method** and enter the basic function information.
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Operation</th>
</tr>
</thead>
<tbody><tr>
<td>Function type</td>
<td>Select event-triggered function or HTTP-triggered function</td>
</tr>
<tr>
<td>Function name</td>
<td>Define the function name</td>
</tr>
<tr>
<td>Region</td>
<td>Select the function deployment region, which must be the same as that of the image repository</td>
</tr>
<tr>
<td>Deployment mode</td>
<td>Select image deployment</td>
</tr>
<tr>
<td>Image</td>
<td>Select the Personal Edition or Enterprise Edition image repository you created</td>
</tr>
<tr>
<td>Image tag</td>
<td>Select the image tag<br>If this parameter is left empty, the latest version of the image will be used by default</td>
</tr>
<tr>
<td>Command</td>
<td>Enter the bootstrap command of the container.<br>Parameter input specification: enter an executable command, such as <code>python</code>. <br>This parameter is optional. If it is left empty, the `Entrypoint` in the Dockerfile will be used by default</td>
</tr>
<tr>
<td>Args</td>
<td>Enter the bootstrap parameter of the container.<br>Parameter input specification: use "space" as the parameter separator, such as <code>-u app.py</code>. <br>This parameter is optional. If it is left empty, the CMD in the Dockerfile will be used by default</td>
</tr>
</tbody></table>
4. Click **Complete**.
