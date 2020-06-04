## Configuration
For services that have been connected to Tencent Cloud CDN, you can view information such as domain name creation time, corresponding CNAME domain name, service region, project, service type, and supported protocols on the basic information module of the domain name. You can also modify information such as service region, service type, and project as needed.

## Configuration Guide
### Viewing basic information
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to access its configuration page. The first module displays its basic information.
![](https://main.qcloudimg.com/raw/2273c600e31b35d12b9480ff74205962.png)

>
> + IPv6 is only supported in mainland China.
> + If you select "IPv4 + IPv6" when connecting the domain name, the node will support both IPv4 and IPv6 access requests.

### Modifying basic information

#### 1. Modify the project
Click **Modify** on the right of the project to modify the project to which the domain name belongs. Note that modifying the project will change the project statistics and sub-user permissions granted by the project.

>To create a project or manage existing projects, go to the [Project Management](https://console.cloud.tencent.com/project) page.

![](https://main.qcloudimg.com/raw/bb56a7b51526f256ccd5d98169861e98.png)

#### 2. Modify the domain name service region
**Definition of the domain name service region**:
+ If a domain name is configured for global acceleration, requests will be scheduled to the nearest global CDN cache node. In general, nodes in and outside of mainland China serve users in and outside of mainland China, respectively.
+ If a domain name is configured for acceleration in mainland China, access requests from global users will be served by cache nodes in mainland China.
+ If a domain name is configured for acceleration outside mainland China, access requests from global users will be served by cache nodes outside mainland China.

You can click **Modify** on the right of the service region to modify it:
![](https://main.qcloudimg.com/raw/bf59e0eccd001b5ccad6262063f032db.png)

> Acceleration services in and outside of mainland China are billed separately at different prices. For more information, please click [here](https://intl.cloud.tencent.com/document/product/228/2949).


#### 3. Modify the service type
CDN optimizes acceleration performance based on the service type. For the best acceleration result, we recommend you select the service type similar to that of your actual services. If you want to adjust the service type, click **Modify** on the right:

>
> + Modifying the service type will change the underlying CDN acceleration platform, which may generate a small number of failed requests and increase origin-pull bandwidth. We recommend you do this during off-peak hours.
> + If you cannot find **Modify** next to your domain name, it may have special configuration. You can [contact us](https://intl.cloud.tencent.com/support) for assistance.

