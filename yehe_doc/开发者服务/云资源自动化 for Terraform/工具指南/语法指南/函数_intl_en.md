## Numeric functions
<table>
<tr>
<td rowspan="1" colSpan="1" ><b>Function</b></td><td rowspan="1" colSpan="1" ><b>Feature</b></td><td rowspan="1" colSpan="1" ><b>Sample</b></td><td rowspan="1" colSpan="1" ><b>Result</b></td>
</tr><tr>
<td rowspan="1" colSpan="1" >abs</td><td rowspan="1" colSpan="1" >Returns an absolute value</td><td rowspan="1" colSpan="1" >abs(-1024)</td><td rowspan="1" colSpan="1" >1024</td>
</tr><tr>
<td rowspan="1" colSpan="1" >ceil</td><td rowspan="1" colSpan="1" >Rounds up</td><td rowspan="1" colSpan="1" >ceil(5.1)</td><td rowspan="1" colSpan="1" >6</td>
</tr><tr>
<td rowspan="1" colSpan="1" >floor</td><td rowspan="1" colSpan="1" >Rounds down</td><td rowspan="1" colSpan="1" >floor(4.9)</td><td rowspan="1" colSpan="1" >4</td>
</tr><tr>
<td rowspan="1" colSpan="1" >log</td><td rowspan="1" colSpan="1" >Calculates a logarithm</td><td rowspan="1" colSpan="1" >log(16, 2)</td><td rowspan="1" colSpan="1" >4</td>
</tr><tr>
<td rowspan="1" colSpan="1" >pow</td><td rowspan="1" colSpan="1" >Calculates an exponent</td><td rowspan="1" colSpan="1" >pow(3,2)</td><td rowspan="1" colSpan="1" >9</td>
</tr><tr>
<td rowspan="1" colSpan="1" >max</td><td rowspan="1" colSpan="1" >Returns the maximum value</td><td rowspan="1" colSpan="1" >max(12,54,3)</td><td rowspan="1" colSpan="1" >54</td>
</tr><tr>
<td rowspan="1" colSpan="1" >min</td><td rowspan="1" colSpan="1" >Returns the minimum value</td><td rowspan="1" colSpan="1" >min(12, 54, 3)</td><td rowspan="1" colSpan="1" >3</td>
</tr>
</table>


## String functions
<table>
<tr>
<td rowspan="1" colSpan="1" ><b>Function</b></td><td rowspan="1" colSpan="1" ><b>Feature</b></td><td rowspan="1" colSpan="1" ><b>Sample</b></td><td rowspan="1" colSpan="1" ><b>Result</b></td>
</tr><tr>
<td rowspan="1" colSpan="1" >chomp</td><td rowspan="1" colSpan="1" >Removes newline characters at the end of a string</td><td rowspan="1" colSpan="1" >chomp("hello\n")</td><td rowspan="1" colSpan="1" >"hello"</td>
</tr><tr>
<td rowspan="1" colSpan="1" >format</td><td rowspan="1" colSpan="1" >Formats a string</td><td rowspan="1" colSpan="1" >format("Hello, %s!", "Ander")</td><td rowspan="1" colSpan="1" >"Hello, Ander!"</td>
</tr><tr><td rowspan="1" colSpan="1" >lower</td><td rowspan="1" colSpan="1" >Converts all cased letters in a string to lowercase</td><td rowspan="1" colSpan="1" >lower("HELLO")</td><td rowspan="1" colSpan="1" >"hello"</td>
</tr><tr>
<td rowspan="1" colSpan="1" >upper</td><td rowspan="1" colSpan="1" >Converts all cased letters in a string to uppercase</td><td rowspan="1" colSpan="1" >upper("hello")</td><td rowspan="1" colSpan="1" >"HELLO"</td>
</tr><tr>
<td rowspan="1" colSpan="1" >join</td><td rowspan="1" colSpan="1" >Concatenates elements of a string list with the given delimiter</td><td rowspan="1" colSpan="1" >join(", ", ["foo", "bar", "baz"])</td><td rowspan="1" colSpan="1" >"foo, bar, baz"</td>
</tr><tr>
<td rowspan="1" colSpan="1" >replace</td><td rowspan="1" colSpan="1" >Replaces specified characters in a string</td><td rowspan="1" colSpan="1" >replace("1 + 2 + 3", "+", "-")</td><td rowspan="1" colSpan="1" >"1 - 2 - 3"</td>
</tr>
</table>


For more information on functions, see [Built-in Functions](https://www.terraform.io/language/functions).