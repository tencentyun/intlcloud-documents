[](id:builtin-refs)
## Built-in Functions

Currently, the Python code mode supports the following built-in functions:

| No. | Built-in Function | Description |
| ---- | ------------ | ------------------------------------------------------------ |
| 1    | abs()        | Calculates the absolute value. |
| 2    | all()        | Checks whether all elements in a sequence (set, list, tuple, or dictionary) meet the specified condition. |
| 3    | any()        | Checks whether any elements in a set meet the specified condition. |
| 4    | bool()       | Constructs a Boolean value.  |
| 5    | bytearray()  | Constructs a byte array. |
| 6    | bytes()      | Constructs an empty `bytes` object. |
| 7    | chr()        | Returns the ASCII character of an integer within the range of 0–256.                                     |
| 8    | dict()       | Creates a dictionary. |
| 9    | enumerate()  | Lists the elements and element subscripts in a traversable data object. This function is generally used in a `for` loop. |
| 10   | filter()     | Filters a set. For example, the result of `list(filter(lambda   x:x>=100, [1,3,4,100,102]))` is `[100,102]`. |
| 11   | float()      | Constructs a floating-point number.                                                   |
| 12   | getattr()    | Calculates the attribute value of an object.                                           |
| 13   | hasattr()    | Checks whether an object has an attribute.                                   |
| 14   | hash()       | Calculates the hash value.                                                     |
| 15   | id()         | Returns the unique identifier of an object.                                             |
| 16   | int()        | Constructs an integer.                                                     |
| 17   | isinstance() | Checks whether an object is of a certain type.                                     |
| 18   | iter()       | Generates an iterator.                                               |
| 19   | len()        | Gets the number of elements in a set.                                             |
| 20   | list()       | Constructs a list.                                                     |
| 21   | map()        | Maps the specified sequence according to the function. For example, the result of `list(map(lambda x: x * 2, [1, 2, 3, 4, 5]))` is `[2, 4, 6, 8, 10]`. |
| 22   | max()        | Gets the maximum value.                                               |
| 23   | min()        | Gets the minimum value.                                                  |
| 24   | next()       | Returns the next item of an iterator. This function is used together with `iter()`.                   |
| 25   | objects()    | Returns an empty object.                                                   |
| 26   | ord()        | Returns the integer value of an ASCII character.                                      |
| 27   | pow()        | Calculates the power of a number.                                                       |
| 28   | print()      | Prints the relevant information during debugging in Python code mode (it takes effect only when you use the debugging feature when editing a Dataway expression). |
| 29   | range()      | Creates an iterable object. For example, the result of `list(range(5))` is `[0,   1, 2, 3, 4]`.       |
| 30   | reversed()   | Creates a revere iterator. For example, the result of `list(reversed('abcdefg'))` is `['g', 'f', 'e', 'd', 'c', 'b', 'a']`. |
| 31   | round()      | Returns the nearest integer of a value.                                           |
| 32   | set()        | Creates a set.                                                 |
| 33   | slice()      | Sets a slice of elements.                                           |
| 34   | sorted()     | Sorts.                                                         |
| 35   | str()        | Constructs a string.                                                   |
| 36   | sum()        | Gets the sum of values.                                                     |
| 37   | tuple()      | Constructs a tuple.                                                     |
| 38   | type()       | Returns the data type of an object.                                                 |
| 39   | zip()        | Zips elements in an iterable object into multiple tuples. For example, the result of `list(zip([1,2,3], [4,5,6]))` is `[(1, 4), (2, 5), (3, 6)]`. |


[](id:modules)
## Third-Party Module
### time
`time` is a library for time processing. For more information, see [16.3. time - Time access and conversions](https://docs.python.org/zh-cn/3.5/library/time.html). It has been built in the Python code mode and can be referenced directly.

Currently, the Python code mode supports the following library functions/types:

| No. | Library Function/Type | Description |
| ---- | ----------------- | ------------------------------------------------------------ |
| 1    | altzone           | Returns the offset of the local DST time zone from UTC in seconds.                  |
| 2    | asctime           | Converts a `struct_time` object into a time string.                          |
| 3    | ctime             | Converts a timestamp into a time string.                                 |
| 4    | mktime()          | Converts a `struct_time` object into a timestamp.                              |
| 5    | strftime()        | Formats a `struct_time` object.                                |
| 6    | strptime()        | Parses an event string in the specified format and returns a structured `struct_time` object. |
| 7    | timezone          | Returns the current time zone.                                                     |
| 8    | tzname            | Returns the name of the current time zone.                                                 |
| 9    | time()            | Returns the current time.                                                     |
| 10   | localtime         | Converts a timestamp into the local time of the local time zone and returns a `struct_time` object. |
   
	 
### json 
`json` is a library for JSON data processing. For more information, see [19.2. json - JSON encoder and decoder](https://docs.python.org/zh-cn/3.5/library/json.html). It has been built in the Python code mode and can be referenced directly.

Currently, the Python code mode supports the following `json` functions:

| No. | `json` Function | Description                                                     |
| ---- | ----------------- | ------------------------------------------------------------ |
|  1   |  dumps()   | Encodes a Python object into a JSON string.  |
|  2   |  loads()     | Parses a JSON string into a Python object.  | 


### math
`math` is a library for arithmetic operations. For more information, see [9.2. math - Mathematical functions](https://docs.python.org/zh-cn/3.5/library/math.html). It has been built in the Python code mode and can be referenced directly.

Currently, the Python code mode supports the following `math` functions:  

| No. | `math` Function | Description                                                     |
| ---- | ----------------- | ------------------------------------------------------------ |
|   1  | math.ceil(x)  | Returns the ceiling of `x`, i.e., the smallest integer greater than or equal to `x`. If `x` is not a floating-point number, delegates to `x.ceil()`, which should return an integer value. | 
|   2  | math.floor(x)   | Returns the floor of `x`, i.e., the largest integer less than or equal to `x`. If `x` is not a floating-point number, delegates to `x.floor()`, which should return an integer value.  | 
|   3  |  math.fabs(x)  | Returns the absolute value of `x`.  | 
|   4  | math.pow(x,y)  | Returns `x` raised to the power `y`.  | 
|   5  | math.sqrt(x)     |  Returns the square root of `x`.  | 

The following constants are supported:

| No. | Constant | Description                                                     |
| ---- | ----------------- | ------------------------------------------------------------ |
|1 |  math.pi | Mathematical constant π = 3.141592..., to available precision. | 
|2 |  math.e | Mathematical constant e = 2.718281..., to available precision. | 
|	3 | Floating-point positive infinity (for negative infinity, use `-math.inf`), which is equivalent to the output of `float('inf')`. | 
|	4 |  math.nan | Floating-point "not a number" (NaN) value, which is equivalent to the output of `float('nan')`.  | 


### base64
`base64` is a library for Base64 encoding/decoding. For more information, see [19.6. base64 - Base16, Base32, Base64, Base85 Data Encodings](https://docs.python.org/zh-cn/3.5/library/base64.html). It has been built in the Python code mode and can be referenced directly. The following functions are supported:

| No. | Supported Function | Description |
| ---- | ----------------- | ------------------------------------------------------------ |
|  1   |  base64.b64encode(s)  | Encodes the bytes-like object `s` using Base64 and returns the encoded bytes.  | 
|  2   | base64.b64decode(s)   |  Decodes the Base64 encoded bytes-like object or string `s` and returns the decoded bytes.      | 


### hmac
`hmac` is a library for HMAC encoding/decoding. For more information, see [15.2. hmac - Keyed-Hashing for Message Authentication](https://docs.python.org/zh-cn/3.5/library/hmac.html). It has been built in the Python code mode and can be referenced directly. The following functions are supported:
   
| No. | Supported Function | Description |
| ---- | ----------------- | ------------------------------------------------------------ |
|  1   |  hmac.new(key)  | Return a new `hmac` object. `key` is a `bytes` or `bytearray` object giving the secret key.  | 


### random
`random` is a library for random number generation. For more information, see [9.6. random - Generate pseudo-random numbers](https://docs.python.org/zh-cn/3.5/library/random.html). It has been built in the Python code mode and can be referenced directly. The following functions are supported:
  
| No. | Supported Function | Description |
| ---- | ----------------- | ------------------------------------------------------------ |
|  1   |  random.randint(a,b) | Returns a random integer `N` such that `a <= N <= b`.      | 


### hashlib  
`hashlib` is a library for hash value generation. For more information, see [15.1. hashlib - Secure hashes and message digests](https://docs.python.org/zh-cn/3.5/library/hashlib.html). It has been built in the Python code mode and can be referenced directly. The following functions/attributes are supported:

| No. | Supported Function/Attribute | Description                                                     |
| ---- | ----------------- | ------------------------------------------------------------ |
|  1   | hashlib.sha256()  | Creates a SHA-256 hash object.  | 
|  2   | hashlib.md5()  |  Creates an MD5 hash object.  | 
|  3   | hashlib.sha1()  | Creates a SHA-1 hash object.  | 
    

### datetime
`datetime` is a library for time and date processing. For more information, see [8.1. datetime - Basic date and time types](https://docs.python.org/zh-cn/3.5/library/datetime.html). It has been built in the Python code mode and can be referenced directly. The following functions/attributes are supported:

| No. | Supported Function/Attribute | Description                                                     |
| ---- | ----------------- | ------------------------------------------------------------ |
| 1   | datetime.date   | Idealized naive date, assuming the current Gregorian calendar always was, and always will be, in effect. Valid attributes: `year`, `month`, `day`.       |
| 2   | datetime.time    | Idealized time, independent of any particular day, assuming that every day has exactly 24 * 60 * 60 seconds. Valid attributes: `hour`, `minute`, `second`, `microsecond`, `tzinfo`.       |
| 3   | datetime.datetime   | Combination of a date and a time. Valid attributes: `year`, `month`, `day`, `hour`, `minute`, `second`, `microsecond`, `tzinfo`.   |
| 4   | datetime.timedelta   | Duration expressing the difference between two `date`, `time`, or `datetime` objects to microsecond resolution.   |
| 5   | datetime.timezone   | Offset from UTC.   |
| 6   | datetime.tzinfo   | Time zone information objects. These are used by the `datetime` and `time` classes to provide a customizable notion of time adjustment (for example, to account for time zone and/or DST).   |
	
	
### decimal
`decimal` is a library for floating-point number processing. For more information, see [9.4. decimal - Decimal fixed point and floating point arithmetic](https://docs.python.org/zh-cn/3.5/library/decimal.html). It has been built in the Python code mode and can be referenced directly. The following functions/attributes are supported:

| No. | Supported Function/Attribute | Description                                                     |
| ---- | ----------------- | ------------------------------------------------------------ |
|  1  | decimal.Decimal |  Constructs a decimal floating-point object. |


### socket
`socket` is the underlying implementation of TCP sockets in Python. For more information, see [18.1. socket - Low-level networking interface](https://docs.python.org/zh-cn/3.5/library/socket.html). It has been built in the Python code mode and can be referenced directly. The following functions/attributes are supported:

| No. | Supported Function/Attribute | Description                                                     |
| ---- | ----------------- | ------------------------------------------------------------ |
|   1  |  socket.htonl()  | Converts 32-bit positive integers from host to network byte order.     |
|   2  |  socket.ntohl()  | Converts 32-bit positive integers from network to host byte order.  |


### pycryptodome
`pycryptodome` is a dedicated third-party encryption tool library. For more information, see [Welcome to PyCryptodome's documentation](https://pycryptodome.readthedocs.io/en/latest/). It has been built in the Python code mode and can be referenced directly. The following functions/attributes are supported:

| No. | Supported Function/Attribute | Description                                                     |
| ---- | ----------------- | ------------------------------------------------------------ |
|   1  | Crypto.Util.Padding | Provides minimal support for adding and removing standard padding from data. This module provides the `pad()` and `unpad()` methods. |
|   2  | Crypto.Cipher.AES  | Implements AES encryption. This module has a fixed data block size of 16 bytes. Its keys can be 128, 192, or 256 bits long. It provides the `new()` method. |


### struct
`struct` is a library for binary file packing. For more information, see [7.1. struct - Interpret bytes as packed binary data](https://docs.python.org/zh-cn/3.5/library/struct.html). It has been built in the Python code mode and can be referenced directly. The following functions/attributes are supported:

| No. | Supported Function/Attribute | Description                                                     |
| ---- | ----------------- | ------------------------------------------------------------ |
|   1  |  struct.pack(format, v1, v2, ...) | Returns a `bytes` object containing the values `v1`, `v2`, ... packed according to the format string `format`. The arguments must match the values required by the format exactly. |
|   2  |   struct.unpack(format, buffer) | Unpacks from the buffer `buffer` according to the format string `format` and returns a tuple. |
  
	
### urllib	
`urllib` is a library for URL processing. For more information, see [21.5. urllib - URL handling modules](https://docs.python.org/zh-cn/3.5/library/urllib.html). It has been built in the Python code mode and can be referenced directly. The following functions/attributes are supported:

| No. | Supported Function/Attribute | Description                                                     |
| ---- | ----------------- | ------------------------------------------------------------ |
|   1  |  urllib.parse.urlparse()  | Gets URL parameters and parses the URL into a tuple of six strings: protocol, location, path, parameters, query, and fragment identifier. |
|   2  |  urllib.parse.unquote() |  Decodes the encoded URL. |


### csv
`csv` is a library for CSV file read/write. For more information, see [14.1. csv - CSV File Reading and Writing](#https://docs.python.org/zh-cn/3.5/library/csv.html). It has been built in the Python code mode and can be referenced directly. The following functions/attributes are supported:

| No. | Supported Function/Attribute | Description                                                     |
| ---- | ----------------- | ------------------------------------------------------------ |
|  1   | csv.reader()  | Creates a reader object, which will traverse over lines in a CSV file object. |
