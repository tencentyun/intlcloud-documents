
## Methods of native types in Python
To help you manipulate native types in Python, Dataway supports the following common Python methods:
<table>
    <tr>
        <th>Data Type</th>
        <th>Method</th>
				<th>Method Type</th>
				<th>Feature</th>
				<th>Output Type</th>
    </tr>
		<tr>
        <td rowspan="15">str</td>
        <td>endswith(suffix[, start[, end]])</td>
				<td>Method</td>
				<td>Compares suffixes.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>split(sep=None, maxsplit=-1)</td>
				<td>Method</td>
				<td>Splits data.</td>
				<td>list</td>
    </tr>
		<tr>
        <td>startswith(prefix[, start[, end]])</td>
				<td>Method</td>
				<td>Compares the prefixes.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>count(sub[, start[, end]])</td>
				<td>Method</td>
				<td>Counts substrings.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>find(sub[, start[, end]])</td>
				<td>Method</td>
				<td>Searches for matched substrings.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>format(*args, **kwargs)</td>
				<td>Method</td>
				<td>Formatting.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>index(sub[, start[, end]])</td>
				<td>Method</td>
				<td>Indexes matched substrings.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>isascii()</td>
				<td>Method</td>
				<td>Returns whether the data has only ASCII characters.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>isspace()</td>
				<td>Method</td>
				<td>Returns whether the data is non-empty and has only whitespace characters.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>encode(encoding="utf-8", errors="strict")</td>
				<td>Method</td>
				<td>Encodes the data.</td>
				<td>bytes</td>
    </tr>
		<tr>
        <td>join(iterable)</td>
				<td>Method</td>
				<td>Concatenation.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>lower()</td>
				<td>Method</td>
				<td>Converts the data into lowercase letters.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>replace(old, new[, count])</td>
				<td>Method</td>
				<td>Replaces data.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>strip([chars])</td>
				<td>Method</td>
				<td>Removes the prefix and suffix consisting of the specified characters.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>upper()</td>
				<td>Method</td>
				<td>Converts the data into uppercase letters.</td>
				<td>str</td>
		</tr>
		<tr>
        <td rowspan="10">bytes</td>
        <td>count(sub[, start[, end]])</td>
				<td>Method</td>
				<td>Counts substrings.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>find(sub[, start[, end]])</td>
				<td>Method</td>
				<td>Searches for matched substrings.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>index(sub[, start[, end]])</td>
				<td>Method</td>
				<td>Indexes matched substrings.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>decode(encoding="utf-8", errors="strict")</td>
				<td>Method</td>
				<td>Decodes the data.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>replace(old, new[, count])</td>
				<td>Method</td>
				<td>Replaces the data.</td>
				<td>bytes</td>
    </tr>
		<tr>
        <td>rstrip([chars])</td>
				<td>Method</td>
				<td>Removes the suffix consisting of the specified characters.</td>
				<td>bytes</td>
    </tr>
		<tr>
        <td>strip([chars])</td>
				<td>Method</td>
				<td>Removes the prefix and suffix consisting of the specified characters.</td>
				<td>bytes</td>
    </tr>
		<tr>
        <td>split(sep=None, maxsplit=-1)</td>
				<td>Method</td>
				<td>Splits data.</td>
				<td>list</td>
    </tr>
		<tr>
        <td>startswith(prefix[, start[, end]])</td>
				<td>Method</td>
				<td>Compares the prefixes.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>endswith(prefix[, start[, end]])</td>
				<td>Method</td>
				<td>Compares the suffixes.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>float</td>
        <td>is_integer()</td>
				<td>Method</td>
				<td>Returns whether the data is an integer.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td rowspan="2">list</td>
        <td>count(x)</td>
				<td>Method</td>
				<td>Counts elements.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>index(sub[, start[, end]])</td>
				<td>Method</td>
				<td>Indexes elements.</td>
				<td>int</td>
    </tr>
		<tr>
        <td rowspan="2">tuple</td>
        <td>count(x)</td>
				<td>Method</td>
				<td>Counts elements.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>index(sub[, start[, end]])</td>
				<td>Method</td>
				<td>Indexes elements.</td>
				<td>int</td>
    </tr>
		<tr>
        <td rowspan="2">dict</td>
        <td>get(key[, default])</td>
				<td>Method</td>
				<td>Gets the `key` value.</td>
				<td>any</td>
    </tr>
		<tr>
        <td>items</td>
				<td>Method</td>
				<td>Gets the key-value pair list.</td>
				<td>list</td>
    </tr>
		<tr>
        <td>set</td>
        <td>union(*others)</td>
				<td>Method</td>
				<td>Returns the new set, which is a union of the specified sets.</td>
				<td>set</td>
    </tr>
		<tr>
        <td rowspan="7">datetime.datetime</td>
        <td>today()</td>
				<td>Class method</td>
				<td>Gets the current time without a time zone.</td>
				<td>datetime.datetime</td>
		</tr>
		<tr>
        <td>fromtimestamp(timestamp, tz=None)</td>
				<td>Class method</td>
				<td>Constructs the time based on a timestamp.</td>
				<td>datetime.datetime</td>
    </tr>
		<tr>
        <td>now()</td>
				<td>Class method</td>
				<td>Gets the current time with a time zone.</td>
				<td>datetime.datetime</td>
    </tr>
		<tr>
        <td>strptime(date_string, format)</td>
				<td>Class method</td>
				<td>Constructs the formatted time.</td>
				<td>datetime.datetime</td>
    </tr>
		<tr>
        <td>time()</td>
				<td>Method</td>
				<td>Converts the data into a time point.</td>
				<td>datetime.time</td>
    </tr>
		<tr>
        <td>date()</td>
				<td>Method</td>
				<td>Converts the data into a date.</td>
				<td>datetime.date</td>
    </tr>
		<tr>
        <td>strftime(format)</td>
				<td>Method</td>
				<td>Formatting.</td>
				<td>str</td>
    </tr>
		<tr>
        <td rowspan="2">datetime.date</td>
        <td>today()</td>
				<td>Class method</td>
				<td>Gets the current date.</td>
				<td>datetime.date</td>
		</tr>
		<tr>
        <td>strftime(format)</td>
				<td>Method</td>
				<td>Formatting.</td>
				<td>str</td>
    </tr>
		<tr>
        <td rowspan="1">datetime.time</td>
        <td>strftime(format)</td>
				<td>Method</td>
				<td>Formatting.</td>
				<td>str</td>
    </tr>
		<tr>
        <td rowspan="3">DataSet</td>
        <td>id()</td>
				<td>Method</td>
				<td>Gets the data set ID.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>partitions()</td>
				<td>Method</td>
				<td>Gets the number of data set partitions.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>schema()</td>
				<td>Method</td>
				<td>Gets the data set schema.</td>
				<td>Schema</td>
    </tr>
		<tr>
        <td rowspan="3">Record</td>
        <td>data()</td>
				<td>Method</td>
				<td>Returns the elements as a list.</td>
				<td>list</td>
    </tr>
		<tr>
        <td>get(name, default=None)</td>
				<td>Method</td>
				<td>Gets the data of the specified field name.</td>
				<td>any</td>
    </tr>
		<tr>
        <td>schema()</td>
				<td>Method</td>
				<td>Gets the data set schema.</td>
				<td>Schema</td>
    </tr>
</table>


## Built-in constants and functions
The expression mode supports constants `None`, `True`, and `False`. In addition, for ease of use, the expression mode has many built-in functions, which you can call to quickly implement the corresponding features and get the required data.

| Built-in Function | Description | 
|---------|---------|
| abs(x) | Returns the absolute value of an integer or floating-point number. |
| all(iterable) | Returns whether all elements are `True` or `None`. |
| any(iterable) | Returns whether any elements are `True`. |
| ascii(object) | Prints the `object` without processing non-ASCII characters. |
| bool([x]) | Converts the data into a boolean value. |
| bytes([source[,encoding[,errors]]]) | Converts the data into a `bytes` object. |
| chr(i) | Returns the Unicode of an integer. |
| dict(kwarg)/dict(mapping,kwarg)/dict(iterable,kwarg) | Converts the data into a `dict` object. |
| float([x]) | Converts the data into a float. | 
| int(x)/int(x,base) | Converts the data into an integer. |
| len(s) | Returns the length. |
| list([iterable]) | Converts the data into a list. |
| max(iterable,[,key,default])/max(arg1,arg2,args[,key]) | Returns the maximum value. |
| min(iterable,[,key,default])/min(arg1,arg2,args[,key]) | Returns the minimum value. |
| ord(c) | Returns the code of a `char` object. | 
| pow(x,y[,z]) | Returns the value of `x` to the power of `y`, modulus `z`. |
| range(stop)/(start,stop[,step]) | Returns an immutable list. |
| repr(object) | Returns the information of the specified printable object. |
| round(number[,ndigits]) | Returns the number rounded to `ndigits` precision after the decimal point. |
| set([iterable]) | Converts the data into a set. |
| str(object)/(object,encoding,errors) | Converts the data into a string. |
| sum(iterable[,start]) | Calculates the sum. |
| tuple([iterable]) | Converts the data into a tuple. |
| type(object) | Returns the data type. |



## Other third-party modules
The expression mode supports some common third-party Python modules.

<table>
    <tr>
        <th>Module</th>
				<th>Feature</th>
				<th>Feature Type</th>
				<th>Description</th>
				<th>Feature Output</th>
		</tr>
		<tr>
        <td rowspan="9">time</td>
        <td>asctime([t])</td>
				<td>Function</td>
				<td>Formats `struct_time`.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>ctime([secs])</td>
				<td>Function</td>
				<td>Formats a timestamp.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>gmtime([secs])</td>
				<td>Function</td>
				<td>Generates the `struct_time` with a UTC time zone.</td>
				<td>struct_time</td>
    </tr>
		<tr>
        <td>localtime([secs])</td>
				<td>Function</td>
				<td>Generates the local `struct_time`.</td>
				<td>struct_time</td>
    </tr>
		<tr>
        <td>mktime(t)</td>
				<td>Function</td>
				<td>Generates a timestamp for `struct_time`.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>strftime(format[,t])</td>
				<td>Function</td>
				<td>Converts `struct_time` into a custom format.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>strptime(string[,format])</td>
				<td>Function</td>
				<td>Converts `struct_time` into a string.</td>
				<td>struct_time</td>
    </tr>
		<tr>
        <td>time()</td>
				<td>Function</td>
				<td>Generates the current timestamp.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>time_ns()</td>
				<td>Function</td>
				<td>Generates the current timestamp in nanoseconds.</td>
				<td>int</td>
    </tr>
    <tr>
        <td rowspan="13">math</td>
        <td>e</td>
				<td>Constant</td>
				<td>Value of Euler's number.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>pi</td>
				<td>Constant</td>
				<td>Value of Pi.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>sqrt(x)</td>
				<td>Function</td>
				<td>Returns the square root.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>log([x,base])</td>
				<td>Function</td>
				<td>Returns the logarithm.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>ceil(x)</td>
				<td>Function</td>
				<td>Returns the smallest integer greater than or equal to `x`.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>floor(x)</td>
				<td>Function</td>
				<td>Returns the greatest integer less than or equal to `x`.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>cos(x)</td>
				<td>Function</td>
				<td>Returns the cosine.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>fabs(x)</td>
				<td>Function</td>
				<td>Returns the absolute value.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>log2(x)</td>
				<td>Function</td>
				<td>Returns the base-2 logarithm of `x`.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>log10(x)</td>
				<td>Function</td>
				<td>Returns the base-10 logarithm of `x`.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>pow(x,y)</td>
				<td>Function</td>
				<td>Returns the value of `x` raised to the power `y`.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>sin(x)</td>
				<td>Function</td>
				<td>Returns the sine.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>tan(x)</td>
				<td>Function</td>
				<td>Returns the tangent.</td>
				<td>float</td>
    </tr>
		<tr>
        <td rowspan="2">json</td>
        <td>dumps(obj, *, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, default=None, sort_keys=False, **kw)</td>
				<td>Function</td>
				<td>Encodes the data into JSON format.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>loads(s, *, encoding=None, cls=None, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, object_pairs_hook=None, **kw)</td>
				<td>Function</td>
				<td>Decodes the JSON data.</td>
				<td>any</td>
    </tr>
		<tr>
        <td rowspan="2">base64</td>
        <td>b64encode(s, altchars=None)</td>
				<td>Function</td>
				<td>Encodes the data into Base64 format.</td>
				<td>bytes</td>
    </tr>
		<tr>
        <td>b64decode(s, altchars=None, validate=False)</td>
				<td>Function</td>
				<td>Decodes the Base64 data.</td>
				<td>bytes</td>
    </tr>
		<tr>
        <td rowspan="2">random</td>
        <td>randint(a, b)</td>
				<td>Function</td>
				<td>Returns a random integer in the range of [a,b].</td>
				<td>int</td>
    </tr>
		<tr>
        <td>random()</td>
				<td>Function</td>
				<td>Returns a random floating-point number in the range of [0,1).</td>
				<td>float</td>
    </tr>
		<tr>
        <td rowspan="2">urllib</td>
        <td>parse.quote(string, safe='/', encoding=None, errors=None)</td>
				<td>Function</td>
				<td>Transcodes symbols.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>parse.urlencode(query, doseq=False, safe='', encoding=None, errors=None)</td>
				<td>Function</td>
				<td>Encodes the URL.</td>
				<td>float</td>
    </tr>
</table>
