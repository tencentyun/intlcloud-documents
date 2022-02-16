## Overview
A tag is a key-value pair provided by Tencent Cloud to identify a resource in the cloud. For more information, please see [Tag Overview](https://intl.cloud.tencent.com/document/product/651/13334).

You can manage TcaplusDB resources in a categorized manner by using tags in various dimensions such as business, purpose, and person-in-charge, making it easier to find the right resources. Tags have no semantic meaning for Tencent Cloud and are parsed and matched strictly based on strings. During the course of use, you only need to pay attention to applicable [use limits](https://intl.cloud.tencent.com/document/product/651/13354).

Below is a specific use case to show how a tag is used.

## Use Case Background
A company owns three TcaplusDB clusters in Tencent Cloud, which are distributed in three gaming businesses whose OPS owners are John, Jane, and Harry, respectively.

## Setting Tag
To facilitate management, the company categorizes its TcaplusDB resources with tags and defines the following tag key-value pairs:

| Tag Key | Tag Value |
| :---------- | ---------------------------------- |
| Business | Game 1, game 2, and game 3 |
| OPS owner | John, Jane, and Harry |

These tags are bound to TcaplusDB resources in the following way:

| Resource ID		| Business	| OPS Owner |
|---------------------|----|--------------|
| tcaplus-abcdef1	| Game 1	| Harry |
| tcaplus-abcdef2	| Game 2 | Jane |
| tcaplus-abcdef3	| Game 3	| John |

## Using Tag
- For more information on how to create and delete a tag, please see [Getting Started with Tag](https://intl.cloud.tencent.com/document/product/651/32582).
- For more information on how to edit a tag in TcaplusDB, please see [Editing Tag](https://intl.cloud.tencent.com/document/product/1016/36551).
