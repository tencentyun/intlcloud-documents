
## Numeric Functions
<table>
<thead>
<tr>
<th width="25%">Function Name</th>
<th width="30%">Feature</th>
<th width="30%">Example</th>
<th width="15%">Result</th>
</tr>
</thead>
<tbody><tr>
<td>abs</td>
<td>Returns an absolute value</td>
<td>abs(-1024)</td>
<td>1024</td>
</tr>
<tr>
<td>ceil</td>
<td>Rounds up</td>
<td>ceil(5.1)</td>
<td>6</td>
</tr>
<tr>
<td>floor</td>
<td>Rounds down</td>
<td>floor(4.9)</td>
<td>4</td>
</tr>
<tr>
<td>log</td>
<td>Calculates a logarithm</td>
<td>log(16, 2)</td>
<td>4</td>
</tr>
<tr>
<td>pow</td>
<td>Calculates an exponential power</td>
<td>pow(3,2)</td>
<td>9</td>
</tr>
<tr>
<td>max</td>
<td>Returns the maximum value</td>
<td>max(12,54,3)</td>
<td>54</td>
</tr>
<tr>
<td>min</td>
<td>Returns the minimum value</td>
<td>min(12, 54, 3)</td>
<td>3</td>
</tr>
</tbody></table>

## String Functions
<table>
<thead>
<tr>
<th width="25%">Function Name</th>
<th width="30%">Feature</th>
<th width="30%">Example</th>
<th width="15%">Result</th>
</tr>
</thead>
<tbody><tr>
<td>chomp</td>
<td>Removes newline characters at the end of a string</td>
<td>chomp("hello\n")</td>
<td>"hello"</td>
</tr>
<tr>
<td>format</td>
<td>Formats a string</td>
<td>format("Hello, %s!", "Ander")</td>
<td>"Hello, Ander!"</td>
</tr>
<tr>
<td>lower</td>
<td>Converts a string to lowercase letters</td>
<td>lower("HELLO")</td>
<td>"hello"</td>
</tr>
<tr>
<td>upper</td>
<td>Converts a string to uppercase letters</td>
<td>upper("hello")</td>
<td>"HELLO"</td>
</tr>
<tr>
<td>join</td>
<td>Concatenates a string list by using a specified delimiter</td>
<td>join(", ", ["foo", "bar", "baz"])</td>
<td>"foo, bar, baz"</td>
</tr>
<tr>
<td>replace</td>
<td>Replaces specified characters in a string</td>
<td>replace("1 + 2 + 3", "+", "-")</td>
<td>"1 - 2 - 3"</td>
</tr>
</tbody></table>

For more information on functions, see [Built-in Functions](https://www.terraform.io/language/functions).
