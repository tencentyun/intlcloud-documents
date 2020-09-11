## Overview
When using programming languages such as Python and Node.js to develop SCF functions, errors may occur for function programs that run normally in the local environment after they are deployed into SCF, as the operating systems, system libraries, or programming language versions may be different. To solve the dependency installation problem, this document describes how to install dependencies with Docker. For more information, please see the following examples:
- [Installing nodejieba for Node.js 8.9](#node)
- [Installing pandas for Python 3.6](#python)


## Directions

### Installing Docker
Install Docker locally. For more information, please see [Get Docker](https://docs.docker.com/install/).

<span id="node"></span>
### Installing nodejieba for Node.js 8.9

This section uses the following code as an example:
```js
'use strict';

const jieba = require('nodejieba');

exports.main_handler = async (event, context, callback) => {
    return jieba.cut('hello world');
};
```
The sample code can run properly on Windows and macOS, but the following error message will be displayed when the code is deployed into SCF:
```plaintext
{"errorCode":1,"errorMessage":"user code exception caught","stackTrace":"/var/user/node_modules/nodejieba/build/Release/nodejieba.node: invalid ELF header"}
```
To solve this error, you can run the following command to install the dependency with Docker:
```plaintext
$ docker run -it --network=host -v /path/to/your-project:/tmp/your-project node:8.9 /bin/bash -c 'cd /tmp/your-project && npm install nodejieba --save'
```

Here, `/path/to/your-project` is the project path, which corresponds to the `/tmp/your-project` directory in the Docker container; therefore, you need to install nodejieba in the `/tmp/your-project` directory of the container (i.e., the project path).   
After installing the dependency, deploy the code into SCF again and the function will run normally.


<span id="python"></span>
### Installing pandas for Python 3.6
This section uses the following code as an example:
```plaintext
import pandas as pd

def main_handler(event, context):
    s = pd.Series([1, 3, 5, 6, 8])
    print(s)
    return len(s)
```

1. Run the following command to install pandas for Python 3.6:
```plaintext
$ docker run -it --network=host -v /path/to/your-project:/tmp/your-project python:3.6.1 /bin/bash -c 'cd /tmp/your-project && pip install pandas -t .'
```
2. After installing the dependency, deploy the code into SCF again and run it. The function can be executed, but a warning message "Could not import the lzma module. Your installed Python is incomplete. Attempting to use lzma compression will result in a RuntimeError." will be displayed. The log information is as follows:
```plaintext
/var/user/pandas/compat/__init__.py:84: UserWarning: Could not import the lzma module. Your installed Python is incomplete. Attempting to use lzma compression will result in a RuntimeError.
  warnings.warn(msg)
0    1
1    3
2    5
3    6
4    8
dtype: int64
```
3. To solve this problem, you need to enter the container and run the following command:
```plaintext
$ docker run -it --network=host -v /tmp/foo:/tmp/bar python:3.6.1 /bin/bash
```
4. Run the following command to install pandas:
```js
$ cd /tmp/bar
$ pip install pandas -t .
echo <<EOF >> index.py
> import pandas as pd
>
> def main_handler(event, context):
>     s = pd.Series([1, 3, 5, 6, 8])
>     print(s)
>     return len(s)
>
> main_handler({}, {})
> EOF
$ python -v index.py > run.log 2>&1
```
5. Run the following command to view the log. The sample code is as follows: <span id="step5"></span>
```js
$ grep lzma run.log
# /usr/local/lib/python3.6/__pycache__/lzma.cpython-36.pyc matches /usr/local/lib/python3.6/lzma.py
# code object from '/usr/local/lib/python3.6/__pycache__/lzma.cpython-36.pyc'
# extension module '_lzma' loaded from '/usr/local/lib/python3.6/lib-dynload/_lzma.cpython-36m-x86_64-linux-gnu.so'
# extension module '_lzma' executed from '/usr/local/lib/python3.6/lib-dynload/_lzma.cpython-36m-x86_64-linux-gnu.so'
import '_lzma' # <_frozen_importlib_external.ExtensionFileLoader object at 0x7f446c40db70>
import 'lzma' # <_frozen_importlib_external.SourceFileLoader object at 0x7f446c40d160>
# cleanup[2] removing lzma
# cleanup[2] removing _lzma
# cleanup[3] wiping lzma
# cleanup[3] wiping _lzma
# destroy _lzma
# destroy lzma
```
As indicated in the log, the function runtime needs to load LZMA and requires the following files:
	- `/usr/local/lib/python3.6/lzma.py`
	- `/usr/local/lib/python3.6/lib-dynload/_lzma.cpython-36m-x86_64-linux-gnu.so`
6. Run the following command to view the existing dependencies of the .so files:<span id="step6"></span>
```plaintext
$ ldd /usr/local/lib/python3.6/lib-dynload/_lzma.cpython-36m-x86_64-linux-gnu.so
	linux-vdso.so.1 (0x00007fff75bb1000)
	liblzma.so.5 => /lib/x86_64-linux-gnu/liblzma.so.5 (0x00007fc743370000)
	libpython3.6m.so.1.0 => /usr/local/lib/libpython3.6m.so.1.0 (0x00007fc742e36000)
	libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007fc742c19000)
	libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007fc74286e000)
	libdl.so.2 => /lib/x86_64-linux-gnu/libdl.so.2 (0x00007fc74266a000)
	libutil.so.1 => /lib/x86_64-linux-gnu/libutil.so.1 (0x00007fc742467000)
	libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007fc742166000)
	/lib64/ld-linux-x86-64.so.2 (0x00007fc74379c000)
```
As indicated in the command execution result, in addition to certain system libraries, the following files are also required:
	- `/lib/x86_64-linux-gnu/liblzma.so.5`
	- `/usr/local/lib/libpython3.6m.so.1.0`
7. Copy the four files obtained in [step 5](#step5) and [step 6](#step6) to the project path and modify the code as follows:
	```js
	import os

	os.environ['LD_LIBRARY_PATH'] = os.path.dirname(
			os.path.realpath(__file__)) + ':' + os.environ['LD_LIBRARY_PATH']

	import pandas as pd

	def main_handler(event, context):
			s = pd.Series([1, 3, 5, 6, 8])
			print(s)
			return len(s)
	```
	
8. Deploy the code into SCF again, and the function can run normally with no warnings reported.
