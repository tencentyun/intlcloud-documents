This document describes how to report the data of a PHP application over the SkyWalking protocol.

>? For more information, see [SkyAPM-php-sdk](https://github.com/SkyAPM/SkyAPM-php-sdk).

## Prerequisites

- GCC/G++ compiler: v4.9 or later.
- PHP: v7.0 or later. 
- CMake: v3.20.0 or later, which can be installed as follows:
<dx-codeblock>
:::  sh
wget https://cmake.org/files/v3.20/cmake-3.20.0.tar.gz
tar -zxvf cmake-3.20.0.tar.gz
cd cmake-3.20.0

./bootstrap
make
make install
:::
</dx-codeblock>
<dx-alert infotype="explain" title="">
The version installed by yum is low, so the source code is used for installation.
</dx-alert>



## Directions 

### Step 1. Get the endpoint and token
Log in to the [APM console](https://console.cloud.tencent.com/apm), enter the **Application monitoring** > **Application list** page, click **Access application**, and select the PHP language and the SkyWalking data collection method. Then, get the endpoint and token in the step of access method selection.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5rBD100_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A120230112-120043%402x.png)

### Step 2. Install gRPC
<dx-codeblock>
:::  sh
wget https://apm-php-depend-src-1258344699.cos.ap-guangzhou.myqcloud.com/grpc.submodule.tar.gz
tar -xzf grpc.submodule.tar.gz
cd grpc/
mkdir -p cmake/build
cd cmake/build
cmake ../..
make -j$(nproc)
ldconfig
# protobuf
cd third_party/protobuf/
./autogen.sh
./configure
make -j$(nproc)
make install
ldconfig
:::
</dx-codeblock>

### Step 3. Compile the `skywalking.so` extension

1. To compile the `skywalking.so` extension, you need to install the dependency library in advance.
<dx-codeblock>
:::  Linux
# yum install boost-devel
# yum install autoconf
  :::
</dx-codeblock>

2. Configure environment variables:
` export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib:/usr/local/lib64`
`export LD_RUN_PATH=$LD_RUN_PATH:/usr/local/lib:/usr/local/lib64`

3. Compile the `skywalking.so` extension:
<dx-codeblock>
:::  sh
wget https://apm-php-depend-src-1258344699.cos.ap-guangzhou.myqcloud.com/SkyAPM-php-sdk.tar.gz
cd SkyAPM-php-sdk/
/usr/local/services/php7/bin/phpize
./configure --with-grpc-src="/local path/grpc" --with-php-config="/local path/php7/bin/php-config"
make
make install
:::
</dx-codeblock>

>?After compilation, you can see the [skywalking.so](http://skywalking.so/) file in the PHP extension directory.

### Step 4. Modify the `php.ini` configuration file

Modify the following configuration items in `php.ini`:
<dx-codeblock>
:::  ini
[skywalking]
; Add the extension
extension=skywalking.so
; Set the application name
skywalking.app_code = php_misterli_test
; Enable the collector
skywalking.enable = 1
; Set the SkyWalking service version
skywalking.version = 8
; Set the SkyWalking service address
skywalking.grpc = ap-guangzhou.apm.tencentcs.com:11800
; Set the authentication token
skywalking.authentication = jnNURCx*******biKzgu
skywalking.error_handler_enable = 0
:::
</dx-codeblock>


>?For more information on the configuration, see [SkyAPM-php-sdk/php.ini](https://github.com/SkyAPM/SkyAPM-php-sdk/blob/master/php.ini).


### Step 5. Restart PHP-FPM

**Option 1:** Change the startup method in the configuration item of **php-fpm.conf** to **daemonize = no**.
**Option 2:** Run the `nohup` command to restart PHP-FPM:
<dx-codeblock>
:::  nohup
nohup /usr/local/services/php7/sbin/php-fpm > /usr/local/services/php7/log/php-fpm-output.log 2>&1 &
:::
</dx-codeblock>


### Step 6. Request the backend service to check whether the access is successful

1. Request your service. The following takes a simple HTTP service deployed with the Laravel framework as an example:
<dx-codeblock>
:::  sh
# curl "http://test.skywalking.com/getHelloWorld"
hello, skywalking
:::
</dx-codeblock>
2. Run the `tcpdump` command to check whether there are packets sent from port 11800:
<dx-codeblock>
:::  sh
# tcpdump -i any -A -s0 -n -nn -l port 11800
dropped privs to tcpdump
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode 262144 bytes
:::
</dx-codeblock>
3. Check whether there is any reported data in **Application monitoring** > **Application list** and **Application details** in the [APM console](https://console.cloud.tencent.com/apm).
