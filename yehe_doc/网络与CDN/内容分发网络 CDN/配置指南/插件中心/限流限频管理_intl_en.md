
## Feature Overview
The rate and speed limiting management feature allows you to set the threshold for the total edge bandwidth of the domain name. After the threshold is exceeded, the system will perform the corresponding limiting operation based on the configured limiting method or set a threshold for the queries per second (QPS) of the domain name.

## Use Cases
1. You can control the access traffic to your business by time period as needed.
2. If your website is suffered from malicious requests or CC/DDoS attacks, you can configure rate and speed limiting to effectively control malicious traffic and avoid incurring high bandwidth and traffic costs.

## Directions
### Step 1. Enable rate and speed limiting and enter the configuration page
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Plugin Center** on the left sidebar, find the rate and speed limiting feature section, and toggle it on. After you enable it for the first time, click **View more** at the bottom of the section to enter the configuration list page.
![]()
![]()
![]()

### Step 2. Create a rate and speed limiting configuration
![]()

#### 2-1. Select a target domain name
The configuration can take effect for one or multiple domain names. You can select the target domain name in the drop-down list.

#### 2-2. Create a rate limiting configuration
Set the threshold for the total edge bandwidth of the domain name.
- Effective Period
	1. Unspecified: The configuration always takes effect.
	2. Specified: The configuration takes effect during the specified time period, such as 12:00–24:00 or 23:00–1:00.
- Bandwidth Cap: If the total edge bandwidth exceeds this cap, the rate will be limited based on the configured limiting method. The minimum cap is 1,024 Mbps (1 Gbps).
- Limiting Method:
	1. Undifferentiated: After the bandwidth cap is exceeded, the rate will be limited based on the specified **Max Speed**, which can be 100 KB/s at the minimum.
	2. Dynamic: After the bandwidth cap is exceeded, the specified proportion of new requests will be denied to keep the total edge bandwidth below the cap. `429` will be returned for denied requests.
	3. PID-based: After the bandwidth cap is exceeded, the limit for all resources (such as URLs) under the domain name will be calculated dynamically based on the PID algorithm and global bandwidth, so that the rate will be limited accordingly below the bandwidth cap.

>?Multiple limiting policies: The rate and speed limiting feature allows tiered configuration of limiting policies. The threshold of a policy at a higher tier should be greater than that of the policy at the current tier.

#### 2-3. Create a frequency limiting configuration
Set the maximum QPS supported by the domain name. If this threshold is exceeded, new requests will be denied, and `429` will be returned.
- Threshold: The value range is 100–5000000 requests/second.
- Effective Period
	1. Unspecified: The configuration always takes effect.
	2. Specified: The configuration takes effect during the specified time period, such as 12:00–24:00 or 23:00–1:00.

### Step 3. Enter the management page to manage the created rule
After a rule is created successfully, it will be in **Running** status by default, and you can perform the following operations on the management page:
- Enable/Disable: When the plugin feature is enabled, you can disable a running rule or enable a disabled rule at any time. 
- Modify: You can modify the target domain name or rate and speed limiting configuration.
- Delete: You can delete rules in **Not enabled** status.
![]()

>?Validation time: A rate and speed limiting rule takes effect globally and needs to be deployed on multiple edge servers when distributed; therefore, there will be a certain delay for it to take effect. It takes about 10 minutes for a rule to take effect after initial enablement or 5 minutes after subsequent modification, disablement, or enablement. To guarantee the stable operations of your business, do not enable/disable a rule frequently.

## Billing Description

Currently, the rate and speed limiting feature is free of charge.
