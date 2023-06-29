## Notes on adjustment

To meet the requirements of applicable laws and regulations in China, ECDN adjusts the offline log generation and shipping rules to generate different offline log packages for the Chinese mainland and regions outside the Chinese mainland respectively. If you use the acceleration service both in and outside the Chinese mainland, to download the complete log content, you need to use both the addresses for the Chinese mainland and regions outside the Chinese mainland to download the offline log packages.

## Adjustment time

The adjustment was officially made on July 4, 2022.

## Impact
This adjustment mainly affects users who use the offline log download API of ECDN.

>!Currently, the ECDN and CDN consoles are integrated into one console, so the [DescribeCdnDomainLogs](https://intl.cloud.tencent.com/document/product/228/33599) API is used to query and download offline logs of both CDN and ECDN. If you still use [DescribeEcdnDomainLogs](https://intl.cloud.tencent.com/document/product/570/36334), the legacy offline log download API of ECDN, you need to switch the API address to that of [DescribeCdnDomainLogs](https://intl.cloud.tencent.com/document/product/228/33599).

1. After this adjustment, if you use the [DescribeCdnDomainLogs](https://intl.cloud.tencent.com/document/product/228/33599) API to query offline logs of an offline ECDN domain name, and global acceleration is enabled, different offline log packages will be generated for the Chinese mainland and regions outside the Chinese mainland respectively, and the API will return the download links of offline log packages for the Chinese mainland and regions outside the Chinese mainland.
2. If you manually download ECDN offline logs in the console, and global acceleration is enabled, after this adjustment, two offline log packages for the Chinese mainland and regions outside the Chinese mainland will be returned respectively, which can be downloaded as needed.
3. If you find that logs are lost after this adjustment, you can call the `DescribeCdnDomainLogs` API again to request the lost offline logs within 30 days to recover them. If such logs are not recovered within 30 days, they may be lost permanently.

