## Overview
>? You can use the [VOD Price Calculator](https://buy.cloud.tencent.com/price/vod/calculator) or refer to [Billing Examples](https://www.tencentcloud.com/document/product/266/38163) to estimate your VOD costs.

 [VOD packages](https://buy.tencentcloud.com/vod) are resource-specific prepaid packages that **can only deduct your usage of the corresponding resources**.

## Must-Knows

- A package becomes valid immediately after purchase and expires one year later. Expired packages cannot be used for deduction.
- A package can be used for deduction only if you are billed daily. If you switch to monthly billing, your packages will be frozen, and their validity period will not be extended.
- Your usage each day will be deducted by your packages first. **The additional usage** will be billed at [pay-as-you-go rates](https://www.tencentcloud.com/document/product/266/14666). To avoid service suspension caused by overdue payments, please pay attention to your package balance and buy new packages or top up your account in a timely manner.
- You can buy multiple packages. The one that was purchased first will be used first.
- If you have multiple packages, their validity periods will not be added up.
- VOD’s packages can only deduct usage of the corresponding VOD services.
- **Traffic packages** and **storage packages** deduct **usage outside the Chinese mainland** at different ratios.
- Your usage each day is billed the following day between 12:00 and 18:00. A package cannot deduct usage that occurs the day before the package is purchased.
- To view your package balance and other details, go to [Package Management](https://console.cloud.tencent.com/vod/assets/packages) (admin privileges required). 


## Package Types

| Type                  | Description                                                         |
| --------------------------- | ------------------------------------------------------------ |
| [Storage package](#storage_page) | A storage package is valid for one year and can deduct your usage of **media storage** based on the **peak storage space** used each day. Usage outside the Chinese mainland is deducted at different ratios. |
| [Traffic package](#flow_page)    | A traffic package can deduct your usage of the **acceleration service** based on the **traffic** consumed. Usage outside the Chinese mainland is deducted at different ratios.|
| [General transcoding](#ntrans_page)  | A general transcoding package can deduct your usage of VOD’s **general transcoding, adaptive bitrate streaming, and video editing** services based on **duration**. The same deduction ratio applies to all regions. |
| [TSC transcoding package](#strans_page)  | A Top Speed Codec (TSC) transcoding package can deduct your usage of **TSC transcoding** based on **duration**. The same deduction ratio applies to all regions. |
| [Moderation package](#check_page)   | A moderation package can deduct your usage of VOD’s **moderation service** based on **duration**. The same deduction ratio applies to all regions. |

You can view your usage of VOD resources in the [VOD console](https://console.cloud.tencent.com/vod/overview). To buy a package, go to the [VOD purchase page](https://www.tencentcloud.com/pricing/vod).

>! The conversion factor for units of traffic is 1,000. For example, 1 TB = 1,000 GB.

[](id:storage_page)

## Storage Packages
A VOD storage package can deduct your usage of storage space with VOD. If you have multiple storage packages, their storage spaces will be added up. The system calculates your peak storage usage each day. If it is lower than the sum of your storage packages, no additional fees will be incurred. If it is higher, the additional usage will be billed at [pay-as-you-go rates](https://www.tencentcloud.com/document/product/266/14666#media_storage). To learn more about billing, see [Billing Examples](https://www.tencentcloud.com/document/product/266/38163).

**About deduction**: Usage inside and outside the Chinese mainland is deducted at a ratio of 1:1 and 1:1.2 respectively. Usage inside the Chinese mainland is deducted first.

### Pricing

| Specification         | Price (USD) |
| ------------------ | ------------ |
| Storage package - 10 GB  | 1.36         |
| Storage package - 50 GB  | 6.83         |
| Storage package - 100 GB  | 13.52         |
| Storage package - 500 GB  | 66.9         |
| Storage package - 1 TB  | 133.66         |
| Storage package - 5 TB  | 654.94         |
| Storage package - 10 TB  | 1,308.49         |
| Storage package - 50 TB  | 6,536.86         |

### Deduction ratios

The deduction ratios of storage packages vary with the type of storage space used. **To make deduction easy, you can convert all other storage usages to STANDARD.**

| Storage Type   | Deduction Ratio    |
| ------ | ------- |
| STANDARD   | 1:1     |
| STANDARD_IA    | 1:0.5   |
| ARCHIVE   | 1:0.25  |
| DEEP ARCHIVE   | 1:0.125  |

### Billing examples

- A 100 GB storage package can deduct 100 GB of STANDARD storage space **or** 200 GB of STANDARD_IA storage space.
- A storage package can deduct usage of different types of storage space at the same time. For example, a 100 GB storage package can deduct 50 GB of STANDARD storage space **and** 100 GB of STANDARD_IA storage space.
  [](id:flow_page)

## Traffic Packages

A VOD traffic package can deduct your usage of VOD’s **acceleration service**. If you have multiple traffic packages, the one that was purchased first will be used first. The system calculates the playback traffic you consume each day and deducts it from your packages. If your actual traffic exceeds the amount available in your packages, the additional usage will be billed at [pay-as-you-go rates](https://www.tencentcloud.com/document/product/266/14666#speed).

**About deduction**: Usage inside and outside the Chinese mainland is deducted at a ratio of 1:1 and 1:1.8 respectively. Usage inside the Chinese mainland is deducted first.

### Pricing

| Specification         | Price (USD) |
| :----------------- | :----------- |
| Traffic package - 10 GB  | 0.27         |
| Traffic package - 100 GB  | 2.66         |
| Traffic package - 500 GB  | 12.32         |
| Traffic package - 1 TB  | 24.5         |
| Traffic package - 5 TB  | 121.66         |
| Traffic package - 10 TB  | 237.86         |
| Traffic package - 50 TB  | 1,175.86         |
| Traffic package - 200 TB  | 3,079.86         |
| Traffic package - 1 PB  | 15,399.86         |

[](id:ntrans_page)

## General Transcoding Packages

A VOD general transcoding package can deduct your usage of **general transcoding, adaptive bitrate streaming, and video editing** (the same deduction ratio applies to all regions). If you have multiple general transcoding packages, the one that was purchased first will be used first. The system calculates your total transcoding duration each day and deducts the portion that applies from your general transcoding packages. If your actual usage exceeds the amount available in your packages, the additional usage will be billed at pay-as-you-go rates. For details, see [Daily Pay-As-You-Go - General transcoding](https://www.tencentcloud.com/document/product/266/14666#trans), [Daily Pay-As-You-Go - Adaptive bitrate streaming](https://www.tencentcloud.com/document/product/266/14666#.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81), and [Daily Pay-As-You-Go - Video editing](https://www.tencentcloud.com/document/product/266/14666#media_edit).

**About deduction**: Usage inside and outside the Chinese mainland is both deducted at a ratio of 1:1.

### Pricing

| Specification          | Price (USD) |
| :------------------ | :----------- |
| General transcoding - 1 hour      | 0.13        |
| General transcoding - 5 hours      | 0.672        |
| General transcoding - 100 hours      | 12.6        |
| General transcoding - 1,000 hours      | 120.26        |
| General transcoding - 10,000 hours      | 839.86        |
| General transcoding - 50,000 hours      | 3,219.86        |

### Deduction ratios

The deduction ratios of VOD general transcoding packages vary with the codec used and output resolution.

| Codec | Resolution                      | Deduction Ratio                         |
| :------- | :-------------------------- | :------------------------------- |
| Audio transcoding | -                           | 1 **:** 0.25                     |
| Remuxing   | -                           | 1 **:** 0.5                      |
| H.264    | SD (short side ≤ 480 px)     | 1 **:** 1                        |
| H.264    | HD (short side ≤ 720 px)     | 1 **:** 2                        |
| H.264    | FHD (short side ≤ 1080 px) | 1 **:** 4                        |
| H.264    | 2K (short side ≤ 1440 px)         | 1 **:** 8                        |
| H.264    | 4K (short side ≤ 2160 px)         | 1 **:** 16                       |
| H.265      | SD (short side ≤ 480 px)             | 1 **:** 5           |
| H.265      | HD (short side ≤ 720 px)        | 1 **:** 10          |
| H.265      | FHD (short side ≤ 1080 px)       | 1 **:** 20         |
| H.265    | 2K (short side ≤ 1440 px)         | 1 **:** 40                       |
| H.265    | 4K (short side ≤ 2160 px)         | 1 **:** 80                       |
| Video editing | -        | Depends on the output resolution. |

### Billing examples

- Suppose the general transcoding feature was used to transcode a video of one minute. The H.264 codec was used and the output resolution was 640 x 480 px. One minute would be deducted from a general transcoding package.
- Suppose the general transcoding feature was used to transcode a video of one minute. The H.264 codec was used and the output resolution was 1280 x 720 px. Two minutes would be deducted from a general transcoding package.
- For adaptive bitrate streaming, the duration of each output stream is deducted separately according to the codec and output resolution.

The higher the output resolution, the faster your package will be used up. 

[](id:strans_page)

## TSC Transcoding Packages

A VOD TSC transcoding package can deduct your usage of **TSC transcoding** (the same deduction ratio applies to all regions). If you have multiple TSC transcoding packages, the one that was purchased first will be used first. The system calculates your total TSC transcoding duration each day and deducts it from your TSC transcoding packages. If your packages cannot deduct all your usage, the additional usage will be billed at [pay-as-you-go rates](https://www.tencentcloud.com/document/product/266/14666#topspeed).

**About deduction**: Usage inside and outside the Chinese mainland is both deducted at a ratio of 1:1.

### Pricing

| Specification         | Price (USD) |
| :----------------- | :----------- |
| TSC transcoding - 2 hours    | 0.83         |
| TSC transcoding - 50 hours    | 20.86         |
| TSC transcoding - 100 hours    | 41.86         |
| TSC transcoding - 1,000 hours    | 247.66         |

### Deduction ratios

The deduction ratios of VOD TSC transcoding packages vary with the codec used and output resolution.

| Codec | Resolution                      | Deduction Ratio                         |
| :------- | :-------------------------- | :--------- |
| H.264    | SD (short side ≤ 480 px)     | 1 **:** 1                        |
| H.264    | HD (short side ≤ 720 px)     | 1 **:** 2                        |
| H.264    | FHD (short side ≤ 1080 px) | 1 **:** 4                        |
| H.264    | 2K (short side ≤ 1440 px)         | 1 **:** 8                        |
| H.264    | 4K (short side ≤ 2160 px)         | 1 **:** 16                       |
| H.265      | SD (short side ≤ 480 px)             | 1 **:** 5           |
| H.265      | HD (short side ≤ 720 px)        | 1 **:** 10          |
| H.265      | FHD (short side ≤ 1080 px)       | 1 **:** 20         |
| H.265    | 2K (short side ≤ 1440 px)         | 1 **:** 40                       |
| H.265    | 4K (short side ≤ 2160 px)         | 1 **:** 80                       |

### Billing examples

- Suppose the TSC transcoding feature was used to transcode a video of one minute. The H.264 codec was used and the output resolution was 640 x 480 px. One minute would be deducted from a TSC transcoding package.
- Suppose the TSC transcoding feature was used to transcode a video of one minute. The H.264 codec was used and the output resolution was 1280 x 720 px. Two minutes would be deducted from a TSC transcoding package.

The higher the output resolution, the faster your package will be used up. 

[](id:check_page)

## Moderation Packages

A VOD moderation package can deduct your usage of **moderation** (the same deduction ratio applies to all regions). If you have multiple moderation packages, the one that was purchased first will be used first. The system calculates your moderation duration each day and deducts it from your moderation packages. If your actual usage exceeds the amount available in your packages, the additional usage will be billed at [pay-as-you-go rates](https://www.tencentcloud.com/document/product/266/14666#media_AI).

**About deduction**: Usage inside and outside the Chinese mainland is both deducted at a ratio of 1:1.

### Pricing

| Specification          | Price (USD) |
| :---------| :--------- |
|Moderation - 1 hour|0.672|
|Moderation - 5 hours|3.36|
|Moderation - 100 hours|65.8|
|Moderation - 1,000 hours|588|
|Moderation - 10,000 hours|4,704|
|Moderation - 50,000 hours|22,848|
