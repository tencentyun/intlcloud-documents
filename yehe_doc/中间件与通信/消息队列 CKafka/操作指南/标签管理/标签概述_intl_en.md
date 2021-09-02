## Overview
Tag is a key-value pair provided by Tencent Cloud which is used to identify resources on the cloud.

You can use tags to classify CKafka resources based on various factors such as service, usage, and person in charge. With tags, you can quickly filter out the corresponding resources. The key-value pair of the tag does not mean anything to Tencent Cloud semantically and will be parsed and matched strictly according to the string.

## Use Limits

### Quantity

Each cloud resource can have up to 50 tags.

### Tag key restrictions

- Tag keys cannot start with `qcloud`, `tencent`, or `project` because they are reserved by the system.
- Tag keys can only start with letters, figures, spaces, or Chinese characters, supporting `+`, `-`, `=`, `.`, `_`, `:`, `/`, and `@`.
- The maximum length of a tag key is 255 characters.

#### Tag value restrictions

- Tag values can only start with letters, figures, spaces, or Chinese characters, supporting `+`, `-`, `=`value, `.`, `_`, `:`, `/`, and `@`.
- The maximum length of a tag value is 127 characters.

## Examples
### Case background
A company has 10 CKafka instances on Tencent Cloud, which are owned by three departments: Ecommerce, Game, and Entertainment. The instances are used for services such as marketing, game A, game B, and post-production. The OPS owners of the three departments are John, Jane, and Harry, respectively.

### Setting tags
To facilitate management, the company categorizes its CKafka resources with tags and defines the following tag key-value pairs.

|Tag Key|Tag Value|
|----------|----------|
|Department|Ecommerce, Game, and Entertainment|
|Business|Marketing, Game A, Game B, and Post-production|
|OPS Owner|John, Jane, and Harry|

Bind the tag key-value pairs to CKafka. The relation between resources and the tag key-value pairs is shown in the table below.

|ID|Department|Service|OPS Owner|
|---|-------|--------|---------|
|  ckafka-1jqwv1|Ecommerce|Marketing|Harry|
|   ckafka-1jqwv12|Ecommerce|Marketing|Harry|
|   ckafka-1jqwv13|Game|Game A|John|
|   ckafka-1jqwv13|Game|Game B|John|
|   ckafka-1jqwv14|Game|Game B|John|
|   ckafka-1jqwv15|Game|Game B|Jane|
|   ckafka-1jqwv16|Game|Game B|Jane|
|   ckafka-1jqwv17|Game|Game B|Jane|
|   ckafka-1jqwv18|Entertainment|Post-production|Harry|
|   ckafka-1jqwv19|Entertainment|Post-production|Harry|
|   ckafka-1jqwv110|Entertainment|Post-production|Harry|

### Using tags
- Filter out the CKafka instances that Harry is in charge of: 
Filter out the CKafka resources OPS owner Harry is in charge of according to the filtering rules. For specific filtering steps, please see [Using Tags] (https://cloud.tencent.com/document/product/597/33356).

- Filter out the CKafka instances Jane of the game department is responsible for: 
Filter out the CKafka instances where the department is "Game" and the OPS owner is "Jane". For detailed directions, please see [Using Tags] (https://cloud.tencent.com/document/product/597/33356).
