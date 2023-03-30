This document describes how to modify the system time zone when creating a TencentDB for SQL Server instance.
>!
>- **As modifying the system time zone requires separately configuring physical machine resources**, [submit a ticket](https://console.cloud.tencent.com/workorder/category) and specify the desired system time zone before purchase.
>- For instances with the modified system time zone, **data is stored on the backend in the modified UTC time**, while **backups, rollbacks, and slow logs are displayed in the console in Beijing time (UTC +8), and the monitoring time is Beijing time**.
>- If you have modified the system time zone for your instance, and a subsequent **scale-out involves data migration**, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>- The system time zone for instances is China Standard Time (Beijing time) by default.

## Prerequisites
You have [submitted a ticket](https://console.cloud.tencent.com/workorder/category) to apply for changing the system time zone.

## Use limits
- **Limits on instance architecture and specification**
 - Only 90-core 720 GB MEM two-node (formerly High Availability/Cluster Edition) instances support modifying the system time zone.
 - All single-node (formerly Basic Edition) instances support modifying the system time zone.

- **Limits on time zone modification**
The system time zone can be modified only during instance purchase.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/).
2. In the instance list, click **Create Database Instance**.
3. On the instance purchase page, set the **System Time Zone** under the **Tag** parameter.
![](https://qcloudimg.tencent-cloud.cn/raw/0856e92abe8826d7a22dedc5a3cb9d2c.png)
4. For more information on how to configure other parameters on the purchase page, see [Creating TencentDB for SQL Server Instance](https://www.tencentcloud.com/document/product/238/31571). After setting all the parameters, click **Buy Now**.
5. You can query the configured system time zone under **Basic Info** on the **Instance Details** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/0fe1e244f068170145570aa61a99fa1d.png)

## List of time zones and UTC offsets

| Time Zone | UTC Offset | Remarks |
|---------|---------|---------|
| Afghanistan Standard Time | (UTC+04:30) | Kabul |
| Alaskan Standard Time | (UTC–09:00) | Alaska |
| Arabian Standard Time | (UTC+04:00) | Abu Dhabi, Muscat |
| Atlantic Standard Time | (UTC–04:00) | Atlantic Time (Canada) |
| AUS Central Standard Time | (UTC+09:30) | Darwin |
| AUS Eastern Standard Time | (UTC+10:00) | Canberra, Melbourne, Sydney |
| Belarus Standard Time | (UTC+03:00) | Minsk |
| Canada Central Standard Time | (UTC–06:00) | Saskatchewan |
| Cape Verde Standard Time | (UTC–01:00) | Cabo Verde Is. |
| Cen. Australia Standard Time | (UTC+09:30) | Adelaide |
| Adelaide | (UTC–06:00) | Central America |
| Central Asia Standard Time | (UTC+06:00) | Astana |
| Central Brazilian Standard Time | (UTC–04:00) | Cuiaba |
| Central Europe Standard Time | (UTC+01:00) | Belgrade, Bratislava, Budapest, Ljubljana, Prague |
| Central European Standard Time | (UTC+01:00) | Sarajevo, Skopje, Warsaw, Zagreb |
| Central Pacific Standard Time | (UTC+11:00) | Solomon Islands, New Caledonia |
| Central Standard Time | (UTC–06:00) | Central Time (US and Canada) |
| Central Standard Time (Mexico) | (UTC–06:00) | Guadalajara, Mexico City, Monterrey |
| China Standard Time | (UTC+08:00) | Beijing, Chongqing, Hong Kong, Urumqi |
| E. Africa Standard Time | (UTC+03:00) | Nairobi |
| E. Australia Standard Time | (UTC+10:00) | Brisbane |
| E. Europe Standard Time | (UTC+02:00) | Chisinau |
| E. South America Standard Time | (UTC–03:00) | Brasilia |
| Eastern Standard Time | (UTC–05:00) | Eastern Time (US and Canada) |
| Georgian Standard Time | (UTC+04:00) | Tbilisi |
| GMT Standard Time | (UTC) | Dublin, Edinburgh, Lisbon, London |
| Greenland Standard Time | (UTC–03:00) | Greenland |
| Greenwich Standard Time | (UTC) | Monrovia, Reykjavik |
| GTB Standard Time | (UTC+02:00) | Athens, Bucharest |
| Hawaiian Standard Time | (UTC–10:00) | Hawaii |
| India Standard Time | (UTC+05:30) | Chennai, Kolkata, Mumbai, New Delhi |
| Jordan Standard Time | (UTC+02:00) | Amman |
| Korea Standard Time | (UTC+09:00) | Seoul |
| Middle East Standard Time | (UTC+02:00) | Beirut |
| Mountain Standard Time | (UTC–07:00) | Mountain Time (US and Canada) |
| Mountain Standard Time (Mexico) | (UTC–07:00) | Chihuahua, La Paz, Mazatlan |
| US Mountain Standard Time | (UTC–07:00) | Arizona |
| New Zealand Standard Time | (UTC+12:00) | Auckland, Wellington |
| Newfoundland Standard Time | (UTC–03:30) | Newfoundland |
| Pacific SA Standard Time | (UTC–03:00) | Santiago |
| Pacific Standard Time | (UTC–08:00) | Pacific Time (US and Canada) |
| Pacific Standard Time (Mexico) | (UTC–08:00) | Baja California |
| Russian Standard Time | (UTC+03:00) | Moscow, St. Petersburg, Volgograd |
| SA Pacific Standard Time | (UTC–05:00) | Bogota, Lima, Quito, Rio Branco |
| SE Asia Standard Time | (UTC+07:00) | Bangkok, Hanoi, Jakarta |
| China Standard Time | (UTC+08:00) | Kuala Lumpur, Singapore |
| Tokyo Standard Time | (UTC+09:00) | Osaka, Sapporo, Tokyo |
| US Eastern Standard Time | (UTC–05:00) | Indiana (East) |
| UTC | UTC | Coordinated Universal Time |
| UTC–02 | (UTC–02:00) | Coordinated Universal Time–02 |
| UTC–08 | (UTC–08:00) | Coordinated Universal Time–08 |
| UTC–09 | (UTC–09:00) | Coordinated Universal Time–09 |
| UTC–11 | (UTC–11:00) | Coordinated Universal Time–11 |
| UTC+12 | (UTC+12:00) | Coordinated Universal Time+12 |
| W. Australia Standard Time | (UTC+08:00) | Perth |
| W. Central Africa Standard Time | (UTC+01:00) | West Central Africa |
| W. Europe Standard Time | (UTC+01:00) | Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna |
