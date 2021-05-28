## Installation
The Tencent Cloud Monitor App plugin can be installed in a variety of ways. Please choose one of the following ways to install it.


<dx-alert infotype="notice" title="Prerequisites">
The Tencent Cloud Monitor App plugin runs on Grafana 7.0 or above. Please start by setting up a Grafana environment. For more information, please see [Download Grafana](https://grafana.com/grafana/download).
</dx-alert>


### Using Grafana CLI

Check all versions of the plugin.

```bash
$ grafana-cli plugins list-versions tencentcloud-monitor-app
```

Install the latest version of the plugin.

```bash
$ grafana-cli plugins install tencentcloud-monitor-app
```
**If a plugin installation directory is customized, use the `--pluginsDir` parameter to configure the directory.**

Restart Grafana.
```bash
$ systemctl restart grafana-server
```

For more information, please see [Install Grafana plugins](https://grafana.com/docs/grafana/latest/plugins/installation/).

>!The only reliable installation method is installation by using Grafana CLI. Any other approach should be considered as a solution and does not provide any guarantee of backward compatibility.

### Using GitHub releases

All release numbers can be viewed in [GitHub Releases](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/releases).

1. Download the latest version of the Tencent Cloud Monitor App plugin code in [GitHub Releases](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/releases) (the resource name is `tencentcloud-monitor-app-[x.x.x].zip`) and place the decompressed code in the plugin directory of Grafana, which is `${GRAFANA_HOME}/data/plugins` by default. You can configure the plugin directory in `${GRAFANA_HOME}/conf/default.ini` or `${GRAFANA_HOME}/conf/custom.ini`. For more information on the plugin directory, please see [here](https://grafana.com/docs/grafana/latest/administration/configuration/#plugins).
2. Restart Grafana.
3. Hover over the **gear** icon on the left sidebar and click **Plugins** to go to the plugin management page. If the Tencent Cloud Monitor App plugin is displayed in the plugin list, it indicates that the plugin has been installed successfully.
4. Enter the app details page and click **Enable**. After the Tencent Cloud Monitor App plugin is enabled successfully, you can use it in Grafana.

### Using source code
If you want to build the software package yourself or provide help, please see [here](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/blob/master/CONTRIBUTING.md).

## Updates

```bash
$ grafana-cli plugins update tencentcloud-monitor-app
```

Restart Grafana.
```bash
$ systemctl restart grafana-server
```

### Upgrading from version 1.x to 2.x
```bash
$ grafana-cli plugins upgrade tencentcloud-monitor-app
```

>!After the upgrade, you need to delete the old data source and configure a new one.

## More Options
If you need more help, run the following to view the help documentation:

```bash
$ grafana-cli plugins --help
```
