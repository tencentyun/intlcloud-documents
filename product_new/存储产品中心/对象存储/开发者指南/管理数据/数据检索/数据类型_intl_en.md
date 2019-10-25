## Overview

COS Select supports a wide variety of primitive data types.

> The data type directly supported by a compiler is called a **primitive data type**.

## Data Type Conversion

COS Select uses the CAST function to determine the data type of your input data. In general, if you do not specify a data type through the CAST function, COS Select will treat the input data as string type.

For more information on the CAST function, see the [CAST](https://intl.cloud.tencent.com/document/product/436/32474#cast) section in the SQL function documentation.

## Supported Data Types

COS Select supports the following primitive data types:

| Name | Description | Example |
| :--------------- | :----------------------------------------------------------- | :--------------------------------------- |
| bool | TRUE/FALSE | FALSE |
| int, integer | An 8-byte signed integer <br>Value range: -9,223,372,036,854,775,808 - 9,223,372,036,854,775,807 | 100000 |
| string | A UTF-8-encoded string with a character length in the range of 1 - 2,147,483,647 | 'xyz' |
| float | An 8-byte floating point | CAST(0.456 AS FLOAT) |
| decimal, numeric | A decimal value with a maximum precision of 38 decimal places and in the range of $-2^{31}$ - $2^{31}-1$ | 123.456 |
| timestamp | A timestamp represents a certain moment and can be expressed with any precision. A timestamp in text format follows the [W3C](https://www.w3.org/TR/NOTE-datetime) specification but needs to end with "T" (unless recorded in days).<br>When a fractional second is used, it should be accurate to at least one decimal place (with no upper limit on the number of decimal places).<br>The offset of local time can be expressed by the offset expressed by hours and minutes when compared to UTC, or "Z" can be used to express the offset of local time from UTC. The time offset does not need to be displayed when only the date is recorded. | CAST('2007-04-05T14:30Z' AS TIMESTAMP) |
