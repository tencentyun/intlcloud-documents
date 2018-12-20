Welcome to Tencent Cloud DNS!
With its high processing capabilities, elastic scalability and robust security protection, Tencent Cloud DNS provides free intelligent resolution services to all domain names on the Internet, bringing a stable, secure and fast resolution experience to your websites. The APIs provided in the documentation allow you to manipulate domain name resolutions by means of request calls. Please make sure you have familiarized yourself with the domain name resolution products and how they are used before using these APIs.

In the API descriptions, if the value ranges of any parameters conflict with those listed on Tencent Cloud's official website, **the ranges on the website shall prevail**.

## 1. Glossary

| Term | Full Name | Description |
|---------|---------|---------|
| domain | Domain | A network name corresponding to an IP address, such as cloud.tencent.com. In the API documentation, generally the primary domain name (e.g., qcloud.com) is used |
| subDomain | Subdomain | The part in a domain name that excludes the primary domain name, such as www |
| record | Record | Resolution record; common types include host record (A record), alias record (CNAME record) and so on |


## 2. Getting Started with APIs
In order to use Tencent Cloud DNS, you need to perform the following two basic operations:

1. Add a domain name resolution
You can add your domain name to Tencent Cloud DNS using the [domain name-adding](https://cloud.tencent.com/document/product/302/8504) API.
2. Add a resolution record
After adding your domain name, you need to use the [resolution record-adding](https://cloud.tencent.com/document/product/302/8516) API to add a resolution record for it, where you can specify the host, record type, TTL, line type and record value.

## 3. Usage Restrictions
Currently, all users can use the free edition of Tencent Cloud DNS services under any circumstances.
