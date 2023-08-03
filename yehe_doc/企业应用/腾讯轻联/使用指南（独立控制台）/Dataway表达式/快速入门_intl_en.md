## Overview

This document describes how to use a Dataway script to assist with flow design.

## Preparations
1. Sign up for a Tencent Cloud account and log in to the [iPaaS console](https://ipaas.tencentcloud.com/login).
2. After logging in successfully, create an integration app and a flow.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9jec667_17-en.png)


## Using a Dataway Expression (Taking a Script in Python Code Mode as an Example)
Here, concatenation of a simple string is used as an example:
1. On the [**Integration apps**](https://ipaas.tencentcloud.com/login) page in the iPaaS console, click **Create**, and create a **Set Payload** component.
2. The component configuration automatically pops up on the right. Here, you need to enter a Dataway expression for **Value**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/btEa722_18-en.png)
3. Hover over the **Value** textbox, and the mode selection buttons will pop up. Click **Code** to enter the code mode.
	![](https://staticintl.cloudcachetci.com/yehe/backend-news/x5M2781_19-en.png)
4. Click the textbox, and the code editor will pop up. Enter a Dataway script, during which the syntax is checked in real time, and errors will be prompted if there are any.
```python
def dw_process(msg):
    return 'Hello' + 'World'
```
	- A complete Python script in Dataway code mode must be a Python 3 code snippet in compliance with the syntax definitions, including the entry function definition `def dw_process(msg)`.
	- Dataway is implemented based on Python 3 syntax and has various built-in third-party modules like `time`, `json`, and `math`. To use a module, you can directly reference the module name.

5. Verify the Dataway script execution result: Before the Dataway script passes syntax check and you click **Confirm** to save the expression, you can verify whether the script is correct.

<br>Click **Debug** in the top-right corner of the editing window and click **Start test** in the pop-up window.

After the test is completed, the result will be output at the bottom of the Dataway code editing window. You can see that the Dataway script execution result is `HelloWorld`, which is as expected.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5DMw447_21-en.png)
You can switch to the **Log** tab to view the printed output result.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/HUKh613_22-en.png)
6. Click **Confirm** to save the Dataway script.

### Expression mode
You can enter simple expressions in expression mode.
1. Hover over the **Value** textbox, and the mode selection buttons will pop up. Click **Expression** to enter the expression mode.
2. Click the textbox to enter a Dataway expression.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Knfk949_23-en.png)

### Text mode
You can input simple data, such as creating literals or [referencing flow data](#dataref), in text mode.

Here, time data generation is used as an example:
1. Hover over the **Value** textbox, and the mode selection buttons will pop up. Click **Text** to enter the text mode.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/VZKb896_24-en.png)
2. Click the data type drop-down list on the left and find and click **datetime**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/puYV342_25-en.png)
3. Click the textbox, and the time configuration interactive UI will pop up. On the UI, configure the time information.
4. Then, click **Confirm**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/8e3t393_26-en.png)



### Script in Java code mode
In addition to Python syntax, Dataway also supports Java syntax. You can enter Java scripts in code mode.

1. Hover over the **Value** textbox, and the mode selection buttons will pop up. Click **Code** to enter the code mode.
	![](https://staticintl.cloudcachetci.com/yehe/backend-news/Afe6498_27-en.png)
2. Click the textbox to enter the code editing interactive UI. Click **Java** to edit your Java script.

3. Click **Confirm** to save the Java script.


[](id:dataref)
### Flow data panel and reference

Dataway allows you to reference the flow context data visually, so that data can flow between components without barriers. Currently, all Dataway modes support visual data reference on the flow data panel, including [text](https://www.tencentcloud.com/document/product/1165/51656), [expression](https://www.tencentcloud.com/document/product/1165/51657), [Python code](https://www.tencentcloud.com/document/product/1165/51659), and [Java code](https://www.tencentcloud.com/document/product/1165/51661) modes.

The **Flow data** panel will pop up automatically when you edit the content in the Dataway textbox. You can click a data button on the panel to import the data, and the data will be displayed as tags in the textbox.


