**Suggestions on configuring node cache validity rules for a site built based on WordPress:** 

- For resources under the domain name `/wp-admin` directory for backend login, you need to set **Cache Option** to **Do not cache**; otherwise, backend login resources will be cached and login errors will occur. If there are any API resources, you also need to set **Cache Option** to **Do not cache** for them.
- For .php, .jsp, .asp, and .aspx dynamic files, you need to set **Cache Option** to **Do not cache** (default cache rule of CDN).

- Other files are cached for 30 days (default cache rule of CDN).

 

**Add cache rules while retaining the default CDN cache rules:** 

1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn).
2. Click **Domain Management** on the left sidebar to enter the domain name management list.
3. Select the target domain name and click **Manage** to enter the domain name configuration page.
4. Click **Cache Configuration** to switch to the **Cache Configuration** tab, and you can view the **Node Cache Validity**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/aGPc944_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230320153520.png)
1. Click **Add Rule**, set **Type** to **File Directory**, **Content** to `/wp-admin`, and **Cache Option** to **Do not cache**, and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/39ik988_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230320153629.png)
6. Click **Add Rule**, set **Type** to **File Extension**, **Content** to `html;js;css`, **Cache Option** to **Cache**, **Cache Validity** to **7 days**, and **Force Cache** to **No**, and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/rQuP652_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230320153810.png)
7. As the lower the rule position, the higher the priority, click **Adjust Priority** and drag and drop the rule of not caching files in the `/wp-admin` directory to the bottom to grant it the highest priority.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/TWgU760_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230320154352.png)
8. After the adjustment, the cache rules are:
 - All resources under the `/wp-admin` directory will not be cached.
 - .php, .jsp, .asp, and .aspx won't be cached.
 - .html, .js, and .css files will be cached for 7 days.
 - Other files will be cached for 30 days.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/IMGv994_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230320154539.png)
