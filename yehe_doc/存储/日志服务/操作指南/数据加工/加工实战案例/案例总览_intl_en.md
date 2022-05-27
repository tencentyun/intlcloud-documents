## Overview

The cases in this document will help you get a general and perceptual understanding of data processing. You can also copy the functions in these cases for your own data processing.

## Limits

- `v` function: **v("Field A")** indicates the value of field A. The parameter is **Field** or **Field value** in some functions. The common error is that: the function parameter is **Field value** but the `v` function is not used to get the field value, which leads to function execution failure.     
- If you need to distribute logs to multiple log topics, you need to configure the **target log topic** and its **target name** in advance. The target name is used by the **distribution function**.   
- `fields_set` function: the `fields_set` function is used to set field values and store the content processed by data processing function. For example, `fields_set("A+B",op_add(v("Field A"),v("Field B")))` is to add the values of fields A and B, and the `op_add` function needs to leverage the `fields_set` function to complete result writing and storage.

## Overview

You can refer to the following cases to complete your data processing:
- [Filtering and Distributing Logs](https://intl.cloud.tencent.com/document/product/614/46135)
- [Structuring Single-Line Text Logs](https://intl.cloud.tencent.com/document/product/614/46136)
- [Masking Data](https://intl.cloud.tencent.com/document/product/614/46137)
- [Processing Logs in Nested JSON Format](https://intl.cloud.tencent.com/document/product/614/46138)
- [Structuring Logs in Multiple Formats](https://intl.cloud.tencent.com/document/product/614/46139)
- [Using Separators to Extract Specified Content from Logs](https://intl.cloud.tencent.com/document/product/614/46140)
