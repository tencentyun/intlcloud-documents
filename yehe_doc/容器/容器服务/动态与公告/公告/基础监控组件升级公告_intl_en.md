
## September 2022
TKE's basic monitoring add-on `tke-monitor-agent` will be connected to the cluster add-on management module from 10:00 AM to 22:00 PM on September 27 and 28, 2022, after which you can maintain its lifecycle in the module. This change won't affect your businesses.

#### Change content 
- Connect the `tke-monitor-agent` add-on to the add-on management module to support version upgrades in the console. For detailed directions, see [Add-On Lifecycle Management](https://intl.cloud.tencent.com/document/product/457/38705).
- Create a secret named `sh.helm.release.v1.monitoragent.v1` in the `kube-system` namespace.



## July 2022
TKE's monitoring add-on will be upgraded to a new version from 10:00 AM to 23:00 PM on July 27–29 and August 1–4, 2022. This upgrade will fix some of the known issues and support the collection and reporting of some basic metrics. This change won't affect your businesses. If you don't want to have this change, [contact us](https://intl.cloud.tencent.com/document/product/457/46720) for assistance.

#### Change content


- Fix the issue where the CPU utilization (usage/request) and CPU utilization (usage/limit) of the Pod are negative values.
- Fix the data source configuration issue where the data source of the GPU metric is incorrectly configured, affecting GPU metric pull in GPU scenarios.
- Fix the issue of reporting node CPU and memory utilization metrics.
- Support the collection of some metrics:
	- Support the collection of the node CPU/memory packing rate.
	- Support the collection of metrics for calculating the recommended CPU/memory value and optimizable CPU/memory resources, which will be collected and reported only when the request recommendation add-on is installed.


## Troubleshooting
If you encounter any problems during the upgrade, [contact us](https://intl.cloud.tencent.com/document/product/457/46720) for assistance. 
