## Overview

 MPS resource packs are resource-specific prepaid packs that can be used to **deduct the corresponding resources you use**.

## Notes

- A resource pack becomes valid immediately after purchase and expires one year later. Expired resource packs cannot be used for deductions.
- Only accounts that are billed daily can purchase resource packs. If you switch to monthly billing, your existing resource packs will be frozen and can no longer be used.
- The resources you use each day will be deducted from your resource packs first. **The remaining resource usage** will be billed at [pay-as-you-go rates](https://intl.cloud.tencent.com/document/product/1041/33478). To avoid service suspension caused by overdue payments, please pay attention to the remaining minutes in your resource packs and buy new packs or top up your account in a timely manner.
- You can buy multiple resource packs. The one that expires first will be used first.
- Each resource pack has its own validity period. If you buy multiple packs, their validity periods will not be added up.
- Each MPS resource pack can only deduct a specific type of MPS resources.
- Resource packs are refundable within five days of purchase (provided that certain conditions are met). For details, see [Refunds](https://intl.cloud.tencent.com/document/product/1041/33481).
- Your usage each day is billed the following day. A resource pack cannot be used to deduct the resources billed on the same day the resource pack is purchased (usage for the previous day).
- To view your resource packs and their usage, log in to the MPS console as admin and go to [Resource Pack Management](https://console.intl.cloud.tencent.com/mps/resources?tab=package).


## Resource Pack Types

| Type                  | Description                                                         |
| --------------------------- | ------------------------------------------------------------ |
| [General transcoding](#ntrans_page)  | Each general transcoding resource pack contains **a certain number of minutes** and can be used to deduct **general transcoding and adaptive bitrate streaming durations**, regardless of the region. |
| [Top Speed Codec transcoding](#strans_page)  | Each TSC transcoding resource pack contains **a certain number of minutes** and can be used to deduct **TSC transcoding durations**, regardless of the region. |

You can view your media processing usages in the [MPS console](https://console.cloud.tencent.com/mps). To buy a resource pack, go to the [MPS purchase page](https://buy.cloud.tencent.com/mps).

[](id:ntrans_page)

## General Transcoding Resource Pack

A general transcoding resource pack can deduct your usage of the **general transcoding and adaptive bitrate streaming** features of MPS. If you have bought multiple packs, the one that expires first will be used first. The system will calculate your total usage of general transcoding and adaptive bitrate streaming each day and will deduct some or all of it (depending on the remaining minutes of your resource packs) from the applicable resource packs. The usage not deducted by resource packs will be billed at [pay-as-you-go rates](https://intl.cloud.tencent.com/document/product/1041/33478).

**Deduction rules**: The same deduction ratios apply to transcoding usage inside and outside the Chinese mainland.

### Pricing

| Resource Pack           | Price (USD) |
| :------------------- | :--------- |
| General transcoding - 5 hours      | 0.8        |
| General transcoding - 100 hours    | 16         |
| General transcoding - 1,000 hours   | 151        |
| General transcoding - 10,000 hours  | 1,058       |
| General transcoding - 50,000 hours  | 4,056       |
| General transcoding - 100,000 hours | 7,760       |

### Deduction ratios

A general transcoding pack can be used to deduct durations for different general transcoding types, but at different ratios.

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
| AV1      | SD (short side ≤ 480 px)             | 1 **:** 10                       |
| AV1      | HD (short side ≤ 720 px)        | 1 **:** 20          |
| AV1      | FHD (short side ≤ 1080 px)     | 1 **:** 40          |
| AV1    | 2K (short side ≤ 1440 px)         | 1 **:** 80                        |
| AV1    | 4K (short side ≤ 2160 px)         | 1 **:** 160                        |

### Examples

- Suppose the general transcoding feature was used to transcode a video of one minute. The H.264 codec was used and the output resolution was 640 x 480 px. One minute would be deducted from a general transcoding resource pack.
- Suppose a the general transcoding feature was used to transcode a video of one minute. The H.264 codec was used and the output resolution was 1280 x 720 px. Two minutes would be deducted from a general transcoding resource pack.
- For adaptive bitrate streaming, the deduction for each output stream is calculated separately according to the codec and output resolution, and then the deductions are added up.

The higher the output video resolution, the faster your resource pack will be used up. 


[](id:strans_page)

## TSC Transcoding Resource Pack

A TSC transcoding resource pack can deduct your usage of the **TSC transcoding** feature of MPS. If you have bought multiple packs, the one that expires first will be used first. The system will calculate your total usage of TSC transcoding each day and will deduct some or all of it (depending on the remaining minutes of your resource packs) from the applicable resource packs. The usage not deducted by resource packs will be billed at [pay-as-you-go rates](https://intl.cloud.tencent.com/document/product/1041/33478).

**Deduction rules**: The same deduction ratios apply to transcoding usage inside and outside the Chinese mainland.

### Pricing

| Resource Pack           | Price (USD) |
| :------------------- | :--------- |
| TSC transcoding - 50 hours     | 26         |
| TSC transcoding - 100 hours     | 53         |
| TSC transcoding - 1,000 hours     | 312         |
| TSC transcoding - 10,000 hours     | 2,645         |
| TSC transcoding - 100,000 hours     | 17,637         |

### Deduction ratios

A TSC transcoding pack can be used to deduct durations for different TSC transcoding types, but at different ratios.

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
| H.265      | 2K (short side ≤ 1440 px)           | 1 **:** 40           |
| H.265    | 4K (short side ≤ 2160 px)         | 1 **:** 80                       |
| AV1      | SD (short side ≤ 480 px)             | 1 **:** 10                       |
| AV1      | HD (short side ≤ 720 px)        | 1 **:** 20          |
| AV1      | FHD (short side ≤ 1080 px)     | 1 **:** 40          |
| AV1    | 2K (short side ≤ 1440 px)         | 1 **:** 80                        |
| AV1    | 4K (short side ≤ 2160 px)         | 1 **:** 160                        |

### Examples

- Suppose the TSC transcoding feature was used to transcode a video of one minute. The H.264 codec was used and the output resolution was 640 x 480 px. One minute would be deducted from a TSC transcoding resource pack.
- Suppose the TSC transcoding feature was used to transcode a video of one minute. The H.264 codec was used and the output resolution was 1280 x 720 px. Two minutes would be deducted from a TSC transcoding resource pack.

The higher the output video resolution, the faster your resource pack will be used up. 
