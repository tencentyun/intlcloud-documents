## Operation Scenarios
You can use the domain name search feature to find a specific domain name. You can filter by different criteria such as domain name, origin server, tag, projects and multiple keywords.

## Directions
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page.
2. Click the domain name search box to activate the search feature, select one or more resource attributes such as domain name, origin server, tag or project, and enter a value to filter domain names.
![](https://main.qcloudimg.com/raw/5f77724408026bd05f2d1ac14b9f8b86.png)
3. If you have questions about the input resource attribute or input format, click the **i** icon for [help with search](#help).
![](https://main.qcloudimg.com/raw/a102d06a64427fd3e171d99ba1c4040a.png)

>
>+ You can only search for master origin servers, not slave ones.
>+ Use semicolon (;) to separate origin server IP addresses when searching for multiple origin servers.
>+ Only single-keyword search is supported for domain names and origin servers.

## Search Description
+ Search by domain name: Enter a complete or partial domain name. Fuzzy search is supported.
  ![](https://main.qcloudimg.com/raw/438647b2478de9df7d204d23639d6b87.png)
+ Search by origin server: Enter a complete or partial origin server name. Fuzzy search is supported.
+ Search by tag: Enter a complete tag and a list of domain names containing the entered tag will be returned. Fuzzy search is not supported.
+ Search by project: You can select multiple projects as a filter.
  ![Project](https://main.qcloudimg.com/raw/8b15327f7125150a2cb78342839f41b5.png)
- Filter by multiple criteria: You can filter by selecting one or more criteria such as tag, domain name, origin server, and project. Use the enter key to separate multiple criteria.
- Filter by multiple keywords: You can enter multiple keywords for each filter criterion. Use vertical bar (|) to separate multiple keywords.

<span id=help></span>
## Search Help
<style>
table th:first-of-type {
    width: 110px;
}
table th:nth-of-type(2) {  
width: 240px;
}
</style>

| Type               | Input Format                                             | Example                    | Search Box Example                                                  | Description                                                         |
| ----------------- | --------------------------------------------------- |----------------------- | ----------------------------------------------------------- | ------------------------------------------------------------ |
|   Single keyword      | **Keyword**                                           | www.test.com             |  ![Single Keyword](https://main.qcloudimg.com/raw/af1f1771fd42f0a38df5c7a0bc9bc861.png)| Filters domain names containing `www.test.com`                           |
| Single domain name attribute        | **Attribute**:**keyword**                                  | Origin server:1.1.1.1            | ![Single domain name attribute](https://main.qcloudimg.com/raw/95eab4659fde0526a6ff7b82b4dae03b.png) | Filters domain names where the origin server contains 1.1.1.1                                  |
| Multiple domain name attributes       | **Attribute**:**keyword** **carriage return**<br>**Attribute**:**keyword** | Domain name:text<br>Origin server:1.1.1.1 | ![Multiple domain name attributes](https://main.qcloudimg.com/raw/1e199e5b7a5268ee3e0b458b7db1fa76.png) | Filters domain names where the domain name contains "text" and origin server contains "1.1.1.1"              |
| Single domain name attribute with multiple keywords | **Attribute**:**keyword**\|**keyword**                      | Project:test1\|test2   | ![Single domain name with multiple keywords](https://main.qcloudimg.com/raw/22a61295630849332aac815db4a6a039.png) | Filters domain names from the selected project where the domain name contains "test1" or "test2." The domain name and origin server attributes currently do not support multi-keyword search |
| Copied character           | (Pasted character)                                       | test abc                 | ![Copy](https://main.qcloudimg.com/raw/823aeda4c1e1f43dc2fa3cec34b8c29f.png) | Filters domain names containing "text" or "abc"                               |

>CDN cannot make global searches if no attribute is entered. Therefore, the **domain name** attribute is added for search by default. In other words, when you enter a single keyword, the content in the search box will be `domain name:www.test.com`; When you copy characters, the content in the search box will be `domain name:test|abc`.

