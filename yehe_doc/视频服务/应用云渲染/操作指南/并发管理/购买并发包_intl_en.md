In CAR, users access your application by connecting to concurrencies. Each concurrency supports access by only one user at a time. If you want your business to sustain 100 concurrent online users, you need to purchase 100 concurrencies.
To purchase and manage concurrencies for your application, you need to purchase a concurrency pack. Concurrency packs are configured with resources and concurrencies, and can then allocated to your projects.

### Directions
1. Go to the [CAR console](https://console.cloud.tencent.com/car).
2. Click **Concurrency management** on the left sidebar and click **Buy concurrency pack** on the **Concurrency management** page.
![](https://qcloudimg.tencent-cloud.cn/raw/bcffcfe3feb201d385411a2fa27d078c.jpg)
3. On the **purchase page**, set the following configuration items:
![](https://qcloudimg.tencent-cloud.cn/raw/47d894a750a9fe7070427a458528c7e5.jpg)

<table>
<tr><th style="width: 23%;">Configuration Item</th><th>Description</th></tr>
<tbody><tr>
<td>Project</td>
<td>Select the project of the concurrency pack based on your business needs. You can select **To be allocated** first and allocate the concurrency pack on the **Project management** or **Concurrency management** page later.</td>
</tr>
<tr>
<td>Billing mode</td>
<td>Currently, CAR concurrency packs support two prepayment modes: monthly and daily subscriptions. For more information, see <a href="">Billing Description</a>.</td>
</tr><tr>
<td>Region</td>
<td>As cross-region CAR concurrency scheduling severely affects the operation experience, you need to select regions based where your business and users are located. Each concurrency can be used by only one user at a time. You need to select the number of concurrencies and the region based on the expected number of concurrent users in each region.</td>
</tr>
<tr>
<td>Concurrency scale</td>
<td>When you purchase a CAR concurrency pack, select a concurrency scale based on the concurrency scale that you specified for your project. If a project is selected, that project’s concurrency scale will be selected.</td>
</tr><tr>
<td>Quantity</td>
<td>Select the number of concurrencies you want to purchase. You can purchase up to 100 concurrencies at a time.</td>
</tr><tr>
<td>Pack duration</a></td>
<td>Select the duration for the concurrency pack based on your business needs.</td>
</tr><tr>
<td>Auto-renew</td>
<td>If you enable <b>Auto-renew</b>, the concurrency pack will be automatically renewed monthly upon expiration if your Tencent Cloud account balance is sufficient.<b>Only monthly subscription supports automatic renewal.</b></td>
</tr><tr>
<td>Pack name</td>
<td>Name the concurrency pack.<br>If the pack contains multiple concurrencies, a number will be added to the end of the name of each CAR concurrency for identification.</td>
</tr></table>

4. Click **Buy Now** and confirm the information on the order details page.

