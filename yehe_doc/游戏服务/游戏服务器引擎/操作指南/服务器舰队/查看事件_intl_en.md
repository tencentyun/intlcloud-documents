## Overview

This document describes how to view events for activity tracing, troubleshooting, and debugging. When each stage of server fleet creation is completed, a series of events related to the fleet and current fleet status will be generated. You can trace all these events in the console.

## Prerequisites

You have completed the [GSE Application Form](https://intl.cloud.tencent.com/apply/p/k0b6pvbhs6), your application has been approved, and you have created a server fleet.

## Directions

1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse/asset) and create a server fleet. For more information, please see [Creating Server Fleets](https://intl.cloud.tencent.com/document/product/1055/36675).
2. Click the **ID** of the created server fleet to enter the fleet details page. Click the **Event** tab to enter the event page.
   The event details list contains the following information: time, code, message, and operation.
   - **Time**: event occurrence time in the format of `yyyy-mm-dd hh:mm:ss`.
   - **Code**: event type. For specific event types, please see the relevant description below.
   - **Message**: event message.
   - **Operation**: download log.
   - **Event type**: currently, there are [deployment and creation events](#.E9.83.A8.E7.BD.B2.E5.88.9B.E5.BB.BA.E4.BA.8B.E4.BB.B6), [VPC peering connection events](#vpc-.E5.AF.B9.E7.AD.89.E4.BA.8B.E4.BB.B6), and [other fleet events](#.E5.85.B6.E4.BB.96.E8.88.B0.E9.98.9F.E4.BA.8B.E4.BB.B6).
![](https://main.qcloudimg.com/raw/2e0240c11acca72a51a07f0c8a511b60.png)




#### Deployment and creation events

| Code | Description |
| ------------------------------------------- | ------------------------------------------------------------ |
| FLEET_CREATED                               | A fleet has been successfully created with status NEW. The event message contains the fleet ID                    |
| FLEET_STATE_DOWNLOADING-FLEET               | The status has changed from NEW to DOWNLOADING, and the asset package is being downloaded onto the fleet instances for installation |
| FLEET_BINARY_DOWNLOAD_FAILED                | Unable to download the asset package onto the fleet instances                                     |
| FLEET_CREATION_EXTRACTING_ASSET             | The asset package has been successfully downloaded onto the instances. The asset package files have been extracted from the uploaded zip file and stored onto the instances. If this stage fails, the fleet cannot enter the ACTIVE status. The logs of this stage display the extracted instance list and are stored on the instances. You can access the logs using the URL in **PreSignedLogUrl**  |
| FLEET_CREATION_RUNNING_INSTALLER            | The asset package has been successfully extracted, and GSE is running the built installation script (if any). If this stage fails, the fleet cannot enter the ACTIVE status. The logs of this stage list the installation steps and whether the installation has been successfully completed. You can access the logs using the URL in **PreSignedLogUrl** |
| FLEET_CREATION_VALIDATING_RUNTIME_CONFIG    | The building process has been successfully completed, and GSE is verifying the game server launch paths specified in the runtime configuration of the fleet. If a launch path is listed, GSE will try launching the game server process and wait for the process to report its readiness. If this stage fails, the fleet cannot enter the ACTIVE status. The logs of this stage list the launch paths in the runtime configuration and whether each launch path has been found. You can access the logs using the URL in **PreSignedLogUrl** |
| FLEET_STATE_VALIDATING- FLEET               | The status has changed from DOWNLOADING to VALIDATING                           |
| FLEET_VALIDATION_LAUNCH_PATH_NOT_FOUND      | Runtime configuration verification failed, as the executable file specified in the launch path does not exist on the instance |
| FLEET_STATE_ASSETING- FLEET                 | The status has changed from VALIDATING to ASSETING                               |
| FLEET_VALIDATION_EXECUTABLE_RUNTIME_FAILURE | Runtime configuration verification failed, as the executable file specified in the launch path cannot run on the fleet instance |
| FLEET_STATE_ACTIVATING- FLEET               | The fleet status has changed from ASSETING to ACTIVATING                          |
| FLEET_ACTIVATION_FAILED- FLEET              | A step in fleet activation failed. This event code indicates that the asset package has been successfully downloaded onto the fleet instances, built, and verified, but the server process cannot be launched |
| FLEET_STATE_ACTIVE-FLEET                    | The status has changed from ACTIVATING to ACTIVE                                 |


#### VPC peering connection events


| Code | Description |
| ----------------------------- | ------------------------------------------------------------ |
| FLEET_VPC_PEERING_SUCCEEDED   | A peering connection has been established between the VPCs of the GSE fleet and the VPC in your Tencent Cloud account |
| FLEET_VPC_PEERING_FAILED      | The requested VPC peering connection failed. For more information, please see the details and status information of the event. A common cause is that two VPCs have overlapping CIDR blocks of IPv4 addresses. To fix this problem, please change the CIDR block of the VPC under your Tencent Cloud account |
| FLEET_VPC_PEERING_DELETED-VPC | The peering connection has been successfully deleted                                           |


#### Other fleet events


| Code | Description |
| ------------------------------------------------ | ------------------------------------------------------------ |
| FLEET_SCALING_EVENT                              | The fleet capacity settings (number of required instances and expansion/reduction limits) have been changed. The event message contains the new capacity settings |
| FLEET_NEW_GAME_SESSION_PROTECTION_POLICY_UPDATED | The settings of the game server session protection policy of the fleet have been changed. The event message contains the old and new policy settings |
| FLEET_DELETED                                    | A fleet deletion request was initiated                                           |
| GENERIC_EVENT                                    | An unspecified event occurred                                           |
| FLEET_STATE_ERROR                                | Status failure                                                     |
| FLEET_INITIALIZATION_FAILED                      | Initialization failed                                                   |
| FLEET_VALIDATION_TIMED_OUT                       | Verification timed out                                                     |
| FLEET_ACTIVATION_FAILED_NO_INSTANCES             | No instance                                                     |
| SERVER_PROCESS_INVALID_PATH                      | Invalid process path                                                 |
| SERVER_PROCESS_SDK_INITIALIZATION_TIMEOUT        | Process SDK initialization timed out                                            |
| SERVER_PROCESS_PROCESS_READY_TIMEOUT             | Process preparation timed out                                                 |
| SERVER_PROCESS_CRASHED                           | The process crashed                                                     |
| SERVER_PROCESS_TERMINATED_UNHEALTHY              | The process is unhealthy                                                   |
| SERVER_PROCESS_FORCE_TERMINATED                  | The process was forcibly terminated                                                 |
| SERVER_PROCESS_PROCESS_EXIT_TIMEOUT              | Process exit timed out                                                 |
| GAME_SESSION_ACTIVATION_TIMEOUT                  | Game server session activation timed out                                       |
| SERVER_PROCESS_PULL_FAILED                      | Failed to pull the process                                                 |
| SERVER_DOWN                                      | The server is down                                                   |





