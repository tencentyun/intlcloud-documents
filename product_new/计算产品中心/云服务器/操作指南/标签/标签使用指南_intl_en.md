## Overview

A **tag** is a key-value pair provided by Tencent Cloud which is used to identify resources on the cloud.

You can use tags to classify CVM resources based on various factors such as service, usage, and person in charge. With tags, you can quickly sift through the resource pool and find the corresponding resources. The value of the tag keys does not mean anything to Tencent Cloud semantically and will be parsed and matched strictly according to the string.

Here we use a specific case to describe how to use tags.

## Use Case Background

A company has 10 CVMs on Tencent Cloud, which are owned by three departments: e-commerce, games, and entertainment. The CVMs are used for services such as marketing campaigns, game A, game B, and post-production. The operation and maintenance managers of the three departments are Ada, Bob, and Chris.

## Setting Tags

For more efficient management, the company uses tags to categorize the CVM resources, and defines the following key/value pairs.

| Tag Key     | Tag Value                             |
| ---------- | ---------------------------------- |
| Department       | E-commerce, games, entertainment                   |
| Service       | Marketing campaigns, game A, game B, post production |
| Operation and Maintenance Manager | Ada, Bob, Chris                   |

After the key/value pairs are bound to the cloud services, the relationship between resources and key/value pairs will be as shown below:

| instance-id  | Department | Service     | Operation and maintenance manager |
| ------------ | ---- | -------- | ---------- |
| ins-abcdef1  | E-commerce | Marketing campaigns | Chris       |
| ins-abcdef2  | E-commerce | Marketing campaigns | Chris       |
| ins-abcdef3  | Games | Game A   | Ada       |
| ins-abcdef3  | Games | Game B   | Ada       |
| ins-abcdef4  | Games | Game B   | Ada       |
| ins-abcdef5  | Games | Game B   | Bob       |
| ins-abcdef6  | Games | Game B   | Bob       |
| ins-abcdef7  | Games | Game B   | Bob       |
| ins-abcdef8  | Entertainment | Post-production | Chris       |
| ins-abcdef9  | Entertainment | Post-production | Chris       |
| ins-abcdef10  | Entertainment | Post-production | Chris       |

## Using Tags

#### Looking for the CVM instances of which Chris is in charge

You can find the corresponding CVM instances by looking for the tag **Operation and maintenance manager: Chris** according to the filter rules. For specific filtering methods, see [Using Tags to Filter Resources](https://intl.cloud.tencent.com/document/product/213/17130).

#### Looking for the CVM Instances which Bob is in charge of and which are used by the Games Department

You can find the corresponding CVM instances by looking for the tags **Department: Games, Operation and maintenance manager: Bob** according to the filter rules. For specific filtering methods, see [Using Tags to Filter Resources](https://intl.cloud.tencent.com/document/product/213/17130).
