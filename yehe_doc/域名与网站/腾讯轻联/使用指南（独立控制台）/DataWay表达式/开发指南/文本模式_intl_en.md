
In text mode, you can generate the required data through simple operations.

## Use of IDE
1. Hover over any Dataway textbox, and the mode selection buttons will pop up automatically. Click **Text** to enter the text mode.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/TQxd420_1.png" width="80%">>
2. Click the data type drop-down list on the left and select the target data type, and Dataway will display a dedicated input interactive UI.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/RNGd469_2.png" width="80%">


## Data types
<dx-accordion>
::: Any type (`any`, which is the default type)
You can directly enter text to generate a string or reference the flow context data on the [flow data panel](https://www.tencentcloud.com/document/product/1165/51655#dataref). If there are multiple items of text data or data referenced on the flow data panel, such data items will be used as elements to form a list.

:::
::: Integer (`int`), float (`float`), string (`string`), decimal (`decimal`), and Boolean (`bool`)
You can directly enter a literal to generate the data or reference the flow context data on the [flow data panel](https://www.tencentcloud.com/document/product/1165/51655#dataref). The data referenced on the flow data panel will be converted into a string and added to the literal.

:::
::: Date and time (`datetime`), date (`date`), and time (`time`)
Click the textbox, and the corresponding visual interactive UI will be displayed. You can click the target time data to select it on the UI.
Date and time:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ww3B486_8.png)
Date:
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/CbHC059_897d13ebc424719da2e5d0a087cc7666.png" width="60%">
Time:
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/4Pin469_963a8a91e520dc62d157eb8414faf3dc.png" width="60%">
:::
::: Null (`None`)
This type indicates that the input data is null, for which the textbox is grayed out.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/UIj5524_9.png)

:::
::: Dictionary (`dict`), list (`list`), message (`Message`), and form (`FormData`)

1. Click the textbox, and the corresponding interactive UI will be displayed.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Y83v622_55c6cc1e164870911993951565ff80c7.png" width="80%">
2. On the interactive UI, add data items one by one and confirm the content.

:::
::: Binary JSON (`Entity.json`) and binary XML (`Entity.xml`)
1. Click the textbox, and the corresponding text input UI will be displayed.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/6uUJ066_5777c31eb67eb33404ef39c5ab30e278.png" width="80%">
2. On the text input UI, enter the text and click **Confirm**, and a UTF-8 encoded `Entity` object of the specified MIME type (`json` or `xml`) will be generated automatically.

:::
::: Data set (`DataSet`) and single data record (`Record`)
In text mode, you can reference data integration data in the flow context on the [flow data panel](https://www.tencentcloud.com/document/product/1165/51655#dataref): data set (`DataSet`) and single data record (`Record`). As `DataSet` and `Record` are data types unique to data integration, you need to generate data of such types through certain components such as **RecordSet Encoder**, and Dataway doesn't provide any generation method.

:::
</dx-accordion>

