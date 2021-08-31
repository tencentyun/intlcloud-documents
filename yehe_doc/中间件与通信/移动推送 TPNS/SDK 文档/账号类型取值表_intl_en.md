

| Account Type | Number Type   | Description | Sample |
| ----------- | ---------- | ------------------------------------------------------------ | ------------------------------------ |
| 0           | Default | It will be categorized as this type when `accountType` is not passed in. | - |
| 1-16        | Custom | The business side binds a custom account with a token, such as uin.  | - |
| 989         | TAID       | Unique device fingerprint ID created by Tencent | -                                    |
| 990         | QIMEI      | Unique device ID provided by Tencent | -                                    |
| 991         | QQ account number       | Five to 12 digits | 12345                                |
| 992         | QQ account number - MD5 | Encrypted QQ account number. Before encryption, a QQ account number is a 5- to 12-character numeric string; after encryption, it becomes a 32-character case-insensitive alphanumeric string. | -                                    |
| 993         | IDFA       | Apple device ID, which is a 32-character uppercase alphanumeric string and divided into several parts by `-`.   | 49E2084A-290C-41EF-AD20-E540CD6AE841 |
| 994 | IDFA - MD5 | Encrypted IDFA. Before encryption, it must be converted into a 32-character uppercase alphanumeric string; after encryption, it becomes a 32-character case-insensitive alphanumeric string. | Before encryption: FF1999CD-7177-4937-A474-74937A102630 <br>After encryption: 2c010ed96aef2fc34983e1e7e9176b7e
| 995 | MAC address | Hardware identifier. Its format: six sets of hexadecimal numbers, separated by `:`; the letters are uppercase. | 08:00:20:0A:8C:6D |
| 996 | MAC address - MD5 | Encrypted MAC address. Before encryption, the separator `:` must be removed and letters converted to uppercase. | Before encryption: a000002c9060f7 <br>After encryption: f2d5a650733ca8c27d502b1c08da14e5
| 997 | OAID | Anonymous device identifier set by the Mobile Security Alliance (MSA). Keep the original value without changing the case, and do not encode it with MD5. It is composed of numbers, letters, and hyphens. The format and length vary depending on the collection vendor and system version. For ID details, please see the MSA website. | - |
| 998 | OAID - MD5 | Encrypted OAID. It is a 32-character case-insensitive string. Directly process the original value of OAID with MD5, without changing the case or removing hyphens. | - |
| 999 | WeChat Union ID | Encrypted account ID of WeChat Open Platform, which is the unique WeChat Union ID of all Official Accounts/Mini Programs/mobile applications under an account on WeChat Open Platform | - |
| 1000 | IMEI | Android device ID, which is a 14- or 15-character numeric string, or a 14- or 15-character lowercase alphanumeric string | - |
| 1001 | IMEI - MD5 | Encrypted IMEI. Before encryption, it must be converted into a 14- or 15-character lowercase alphanumeric string; after encryption: it becomes a 32-character case-insensitive numeric strings. | Before encryption: a000002c9060f7 <br>After encryption: f2d5a650733ca8c27d502b1c08da14e5 |
| 1002 | Mobile number | Mobile number in E.164 format `[+][country code or area code][subscriber number]` | +8613711112222, where there is a `+` sign in the front, `86` is the country code, and `13711112222` is the subscriber number |
| 1003 | WeChat OpenID | Unique identifier of a WeChat user under a WeChat Official account/ Mini Program AppID. The obtained OpenID varies depending on AppID. | - |
| 1004 | QQ OpenID |- |- |
| 1005 | Email |- |- |
| 1006 | Sina Weibo|- |- |
| 1007 | Alipay |- |- |
| 1008 | Taobao |- |- |
| 1009 | Douban |- |- |
| 1010 | Facebook |- |- |
| 1011 | Twitter |- |- |
| 1012 | Google |- |- |
| 1013 | Baidu |- |- |
| 1014 | JD |- |- |
| 1015 | LinkedIn |- |- |
