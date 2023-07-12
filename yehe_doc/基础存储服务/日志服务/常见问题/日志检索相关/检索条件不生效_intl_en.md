When you use the search and analysis feature, you may encounter situations where many of the logs in the search results "do not meet" the search criteria, as if the search criteria were not in effect. This is often because the search statement does not use appropriate syntax. Several typical cases are as follows:

### What should I do if search criteria connected by spaces do not take effect?

If the search statement is in the format of `string1 string2 string3` or `key1:value1 key2:value2 key3:value3`, where the search criteria are connected by spaces, any raw log that meets any of these criteria, rather than all of them, will be included in the research result.

This is because search criteria connected by spaces are treated with the "or" logic. If you want all search criteria to be met, use `AND` to connect them, such as `string1 AND string2 AND string3` and `key1:value1 AND key2:value2 AND key3:value3`.



### What should I do if search criteria containing English symbols do not take effect?

If the search statement contains an English symbol, such as `\/online\/login` and `URL:\/online\/login` (the `/` symbol is a reserved symbol of the syntax and therefore needs to be escaped), any raw log that contains `online` or `login`, instead of both `online` and `login`, will be included in the search result.

This is because the search criteria contain an English symbol, and if the full-text index or the corresponding key-value index field in the index configuration contains the English symbol, the search condition will also be segmented. Any raw log that contains any of the words obtained after segmentation will be included in the search result. If you want to search for logs that contain all the words in the search criteria, use double quotation marks to wrap the search criteria, for example, `"/online/login"` and `URL:"/online/login"`. In this case, special symbols in the quotation marks do not need to be escaped.

For more information about segments, see [Segment and Index](https://intl.cloud.tencent.com/document/product/614/45409).



### What should I do if search criteria containing Chinese characters do not take effect?

If the search statement is in Chinese, and the **Allow Chinese Characters** option in the index configuration is selected, any raw log that contains any of the Chinese characters, instead of all the Chinese characters, specified in the search statement will be included in the search result.

This is because if the **Allow Chinese Characters** option in the index configuration is selected, the Chinese words are segmented into individual words. Any raw log that contains any of the words obtained after segmentation will be included in the search result. If you want to search for logs that contain all the words in the search criteria, use double quotation marks to wrap the search criteria.
