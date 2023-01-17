## Overview
YARN resource scheduling supports interactive YARN resource queue scheduling management, which is more convenient than file-based configuration management. Currently, it supports two types of scheduling configurations: Fair Scheduler and Capacity Scheduler.
## Notes
1. Fair Scheduler is used by default. Therefore, you need to configure parameters in the `fair-scheduler.xml` configuration file for the YARN component. If you switch to Capacity Scheduler, configure parameters in the `capacity-scheduler.xml` configuration file. No matter which scheduler you use, parameter configurations must be consistent with those on the **Resource Scheduling** page.
2. After switching the scheduler or setting the policy on the **Resource Scheduling** page, you need to click **Apply** to deliver the configuration, which may restart the ResourceManager.
3. If you have enabled label-based scheduling in **Configuration Management**, the sync operation will be performed when Capacity Scheduler is enabled.
4. Subpools can be nested inside a resource pool, and the nested subpools are subject to the rules set for the parent pool.
5. If you specify to sync the modified configuration when disabling the resource scheduler, the configuration file and parameters of the scheduler in **Configuration Management** will be overwritten.
