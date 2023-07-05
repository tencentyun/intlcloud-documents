## Overview
Theia IDE is an open-source extensible framework for building web-based cloud IDEs, with proper multi-language support and VS Code extensions. Tencent Cloud Lighthouse provides the Theia IDE image with Go, Python, Node.js, Clang, and OpenJDK development environments installed, allowing you to easily and quickly develop projects and businesses across platforms.


## Directions
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Click **Create** to enter the Lighthouse purchase page.
	![](https://qcloudimg.tencent-cloud.cn/raw/0a3adf01ba4390699c76b6522fc7f097.png)
	- **Region**: Select a region near your target users to reduce the network latency and improve their access speed.
	- **Image**: Select the **Theia IDE 1.21.1** application image.
	- **Availability zone**: **Randomly assigned** is selected by default. You can select one as well.
	- **Instance bundle**: Select an instance bundle according to the required instance configuration (including CPU, memory, system disk, bandwidth, and monthly traffic).
	- **Instance name**: Enter a custom instance name. If it is left empty, an "image name + 4-digit random string" will be used as the name by default. When instances are created in batches, their names will be consecutive with auto-incrementing suffixes. For example, if you enter "LH" as the name and purchase three instances, the three instances are named "LH1", "LH2", and "LH3".
	- **Purchase period**: Default to **1 month**.
	- **Quantity**: Default to **1**.
3. Click **Buy now** to submit your order and make the payment as prompted. Then, return to the Lighthouse console.
4. After the instance is created, select the instance from the list to enter its details page.
You can view the configuration items of the Theia IDE application.
5. Select the **Pre-installed application** tab to enter the application details page.
6. [](id:Step6)In the **Pre-installed software** section, click <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin:-3px 0px"/> to copy the command for getting the admin password of Theia 1.21.1.
7. In the **Pre-installed software** section, click **Log in**.
![](https://qcloudimg.tencent-cloud.cn/raw/94f8855e0b336f6b75af2c1bdcd7e4d4.png)
8. [](id:Step8)In the pop-up login window, paste the command copied in [step 6](#Step6) and press **Enter**.
Then, you can get the Theia IDE admin account (admin) and password. Store and record them properly.
9. Close the login window and go back to the application details page of the instance.
10. In the **Pre-installed software** section, click the **Access address** of Theia 1.21.1.
<dx-alert infotype="explain" title="">
We recommend you use Chrome or Firefox for this operation, as other browsers (such as Safari) may have compatibility issues.
</dx-alert>
11. In the pop-up window, enter the admin account and password obtained in [step 8](#Step8) and click **OK**.
After successful verification, you can enter the Theia IDE GUI.

## Subsequent Operations
### Selecting the workspace
1. Select **Open Workspace** on the Theia IDE Getting Started page.
2. In the **Open Workspace** pop-up window, select `/` from the drop-down list to open the directory. In Theia IDE, a directory is a workspace. `/data` is used as an example in this document.
![](https://main.qcloudimg.com/raw/5451fbf0a2d310a2b3b77be9bab1a1a4.png)
3. Click **Open** to enter the `/data` workspace.


### Examples

<dx-alert infotype="explain" title="">
Theia IDE supports Python, Java, Go, C/C++, and Node.js languages. Sample programs in Python, Go, and C++ are run on the command line and in the GUI here.
</dx-alert>



#### Python
1. In the workspace, select **File** > **New Folder** at the top of the window.
2. In the pop-up window, create a folder named `Python` and a simple sample file `main.py` under it.
![](https://main.qcloudimg.com/raw/f8b8f3f14629f090571bdc84f67bd577.png)
3. You can run the program in either of the following ways:
<ul>
<li><b>Command line:</b></li>
<ol type="i">
<li class="roman">Select <b>Terminal</b> > <b>New Terminal</b> at the top of the window to open a terminal.</li>
<li class="roman">Run the following commands in sequence in the terminal to run the program.
<pre>cd Python</pre>
<pre>python3.8 main.py</pre>
The execution result is as shown below:
<br>
<img src="https://main.qcloudimg.com/raw/77a29e75d9473027a7b6d4b411c49a68.png" />
</li>
</ol>
</ul>
<ul>
<li><b>GUI:</b></li>
Click <img src="https://main.qcloudimg.com/raw/708198cbeab5c12c186e832ec484c60e.png" style="margin:-3px 0px"/> in the top-right corner of the window to run the program.
The execution result is as shown below:
<br>
<img src="https://main.qcloudimg.com/raw/da0fb5c90d70695d8e1636cf6863cc20.png" />
</li>
</ol>
</ul>

#### Go
1. In the workspace, select **File** > **New Folder** at the top of the window.
2. In the pop-up window, create a folder named `go` and a simple sample file `main.go` under it.
![](https://main.qcloudimg.com/raw/caedca384df2a2e8e42cee06af6600d9.png)
3. You can run the program in either of the following ways:
<ul>
<li><b>Command line:</b></li>
<ol type="i">
<li class="roman">Select <b>Terminal</b> > <b>New Terminal</b> at the top of the window to open a terminal.</li>
<li class="roman">Run the following commands in sequence in the terminal to run the program.
<pre>cd go</pre>
<pre>go run main.go</pre>
The execution result is as shown below:
<br>
<img src="https://main.qcloudimg.com/raw/6550d3deeb6b9cd9776f1985d1bac710.png" />
</li>
</ol>
</ul>
<ul>
<li><b>GUI:</b></li>
<ol type="i">
<li class="roman">Click <img src="https://main.qcloudimg.com/raw/710f37253b774a7e3aed3e94b5bb1777.png" style="margin:-6px 0px"> on the left to open the **DEBUG** section.</li>
<li class="roman">In **DEBUG**, select <b>Add Configuration</b> from the drop-down list to generate the configuration file.
<br>
<img src="https://main.qcloudimg.com/raw/6e6e83d3bc7476029b662997be9c1525.png" style="margin:-3px 0px">
</li>
<li class="roman">Open the <code>main.go</code> file and select <img src="https://main.qcloudimg.com/raw/8d1ae32ecac7a0865835e8f3cfb7916c.png" style="margin:-3px 0px"/> in the **DEBUG** section to run the program. The execution result is as shown below:
<br>
<img src="https://main.qcloudimg.com/raw/dab083f4d4496ef058a65a98782c33a9.png" style="margin:-3px 0px">
</li>
</ol>
</ul>

#### C++
1. In the workspace, select **File** > **New Folder** at the top of the window.
2. In the pop-up window, create a folder named `c++` and a simple sample file `main.cpp` under it.
![](https://main.qcloudimg.com/raw/3eadfa7a7924581d0b3c87dd3cac35e2.png)
3. You can run the program in either of the following ways:
<ul>
<li><b>Command line:</b></li>
<ol type="i">
<li class="roman">Select <b>Terminal</b> > <b>New Terminal</b> at the top of the window to open a terminal.</li>
<li class="roman">Run the following commands in sequence in the terminal to run the program.
<pre>cd c++</pre>
<pre>clang++ main.c</pre>
<pre>./a.out</pre>
The execution result is as shown below:
<br>
<img src="https://main.qcloudimg.com/raw/7f905e65bfa92c5182ad551993014f42.png" />
</li>
</ol>
</ul>
<ul>
<li><b>GUI:</b></li>
<ol type="i">
<li class="roman">Click <img src="https://main.qcloudimg.com/raw/710f37253b774a7e3aed3e94b5bb1777.png" style="margin:-6px 0px"> on the left to open the **DEBUG** section.</li>
<li class="roman">In **DEBUG**, select <b>Add Configuration</b> from the drop-down list to generate the configuration file as.
<br>
<img src="https://main.qcloudimg.com/raw/6e6e83d3bc7476029b662997be9c1525.png" style="margin:-3px 0px">
</li>
<li class="roman">In the drop-down list of the configuration file, select <b>{ } GDB CDT Local debugging</b>.</li>
<li class="roman">Replace <code>/${command:askProgramPath}</code> in the configuration file with <code>/c++/a.out</code> and save the change.</li>
<li class="roman">Select <img src="https://main.qcloudimg.com/raw/7090e9c3a03493c183e8a259896dcde9.png" style="margin:-3px 0px"> in the *DEBUG** section to open the Debug console.</li>
<li class="roman">Select <img src="https://main.qcloudimg.com/raw/8d1ae32ecac7a0865835e8f3cfb7916c.png" style="margin:-3px 0px"/> in the **DEBUG** section to run the program. The execution result is as shown below:
<br>
<img src="https://main.qcloudimg.com/raw/fc23bdc950648b3e4302968ce9d4e240.png">
</li>
</ol>
</ul>

### Enabling HTTPS access
You can install an SSL certificate and enable HTTPS access for your Theia IDE instance as instructed in [Installing Certificate on NGINX Server](https://intl.cloud.tencent.com/document/product/1103/47406).
<dx-alert infotype="notice" title="">
You only need to modify the `/usr/local/lighthouse/softwares/nginx/conf/include/theia.conf` configuration file but not `/usr/local/lighthouse/softwares/nginx/conf/nginx.conf` for your Theia IDE instance.
</dx-alert>
See the following configuration to modify the file:
```
server {
    listen 443 ssl;
    server_tokens off;
    keepalive_timeout 5;
    root /usr/local/lighthouse/softwares/nginx/html;
    index index.php index.html;
    access_log logs/theia.log combinediox;
    error_log logs/theia.error.log;
    server_name cloud.tencent.com;   # Enter the domain name bound to your certificate, such as `cloud.tencent.com`
    ssl_certificate 1_cloud.tencent.com_bundle.crt;   # Enter the name of your certificate file, such as `1_cloud.tencent.com_bundle.crt`
    ssl_certificate_key 2_cloud.tencent.com.key;    # Enter the name of your private key file, such as `2_cloud.tencent.com.key`
    ssl_session_timeout 5m;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;  # You can see this SSL protocol for configuration
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE;   # You can use this encryption suite configuration written in line with the OpenSSL standard
    ssl_prefer_server_ciphers on;

   auth_digest_user_file /home/lighthouse/passwd.digest;
    auth_digest_shm_size  8m;   # the storage space allocated for tracking active sessions

   location / {
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";

        auth_digest 'lighthouse';
        auth_digest_timeout 120s;   # allow users to wait 2 minute between receiving the
                                    # challenge and hitting send in the browser dialog box
        auth_digest_expires 600s;   # after a successful challenge/response, let the client
                                    # continue to use the same nonce for additional requests
                                    # for 600 seconds before generating a new challenge
        auth_digest_replays 60;     # also generate a new challenge if the client uses the
                                    # same nonce more than 60 times before the expire time limit

        proxy_pass http://127.0.0.1:3000;
    }
}

server {
    listen 80;
    server_name cloud.tencent.com;    # Enter the domain name bound to your certificate, such as `cloud.tencent.com`
    return 301 https://$host$request_uri;       # Redirect HTTP requests to HTTPS
}
```


<style>
	.roman{
		list-style-type:lower-roman
	}
</style>
