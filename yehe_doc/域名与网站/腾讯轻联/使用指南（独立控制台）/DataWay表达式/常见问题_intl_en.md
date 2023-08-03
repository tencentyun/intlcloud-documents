
### What is the relationship between Dataway Python expressions and Python scripts?
Dataway Python expressions are encapsulated based on Python 3. Their features are also tailored based on Python, and you must define a valid entry function `dw_process(msg)`. Therefore, all Dataway expressions have a returned value after being executed normally, but Python scripts don't necessarily have a specific returned value.



### Where can I use Dataway expressions?
Currently, almost all core iPaaS components can calculate the value of expressions. Dataway plays a key role in implementing the dynamic value calculation capabilities of iPaaS.



### How do I troubleshoot a Dataway script execution error?
1. Check to make sure that the Dataway script contains no syntax errors and has passed the syntax check during editing.
2. View the execution error log to locate the cause of the Dataway script error and the line of the script which caused the error for further problem analysis and locating.
3. You can also [debug the Dataway script](https://www.tencentcloud.com/document/product/1165/51659) for troubleshooting.



### How do I use a third-party module?
By default, Dataway supports only the following built-in modules: `time`, `json`, `math`, `base64`, `hmac`, `random`, `hashlib`, `Crypto`, `socket`, `struct`, `decimal`, `urllib`, `csv`, and `datetime`.

Generally, such modules are enough for Dataway scripts. If you do need to use more third-party modules, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to request support for an additional third-party module.

