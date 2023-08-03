## Overview

In expression mode, you can enter a valid Python expression to return the required data. The expression mode is specifically optimized to provide a smart prompt feature which simplifies your input and outperform the code mode.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/MmZ7078_1.png)

## Use of IDE

Hover over any Dataway textbox, and the mode selection buttons will pop up automatically. Click **Expression** and then click the textbox to enter an expression.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/HBst170_2.png)


- **Syntax check**
On the Dataway interactive UI, you can check the syntax of the expression in real time. If an error occurs, the border of the textbox will turn red, and an error message will be displayed below the textbox.
You can modify the expression based on the error message. A flow can be published only after all its expressions pass syntax check.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/isY4217_3.png)


- **Autocomplete**
When you input content in the textbox, the Dataway interactive UI will automatically display the syntax prompts and viable completion options based on the current context below or above the textbox. You can select an appropriate tag to quickly complete your expression. The syntax prompts include attributes, methods, built-in functions, and third-party modules.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ShkL984_4.png)

- **Reference on the flow data panel**
In expression mode, you can reference data on the [flow data](https://www.tencentcloud.com/document/product/1165/51655#dataref) panel. For more information, see [Flow Data Panel](https://www.tencentcloud.com/document/product/1165/51655#dataref).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Vv3a029_5.png)

- **Type conversion**
Other than certain components with special requirements, the expression mode supports convenient type conversion for the Dataway interactive UI. You can click the target data type in the drop-down list on the left of the textbox to convert the type of the expression output result explicitly, so as to forcibly change the data type. The default type is `any`, i.e., no type conversion.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9pHL049_6.png)

## Syntax

The expression mode is based on the `eval()` function in Python 3 syntax to make it easier to use. Like the code mode, the expression mode allows you to use `msg` (`Message` type) to reference the message of the current flow. In addition, in expression mode, you can quickly reference the output data of previous components quickly on the [flow data panel](https://www.tencentcloud.com/document/product/1165/51655#dataref).

The expression mode supports the following syntax structures:

<table>
    <tr>
        <th>Expression Group</th>
        <th>Expression Type</th>
				<th>Description</th>
				<th>Example</th>
				<th>Remarks</th>
    </tr>
    <tr>
        <td rowspan="10">Atomic expression</td>
        <td>literal</td>
				<td>Literal</td>
				<td>"abc", 123, True, b'abc'</td>
				<td>Literal of a data type such as `string`, `int`, `float`, `bool`, or `bytes`.</td>
    </tr>
    <tr>
        <td>name</td>
				<td>Identifier</td>
				<td>abc</td>
				<td>A variable used to read the specified name from global context.</td>
    </tr>
		<tr>
        <td>tuple</td>
				<td>Tuple</td>
				<td>('a', 'b', 'c'), (str(1))</td>
				<td>Returns a tuple if there is at least one comma; otherwise, returns the value of a single expression.</td>
    </tr>
		<tr>
        <td>list</td>
				<td>List</td>
				<td>[1,2,3]</td>
				<td>Enumerates elements to construct a list.</td>
    </tr>
		<tr>
        <td>list-comp</td>
				<td>List comprehension</td>
				<td>[i for i in 'abc']</td>
				<td>Constructs a list through comprehension.</td>
    </tr>
		<tr>
        <td>set</td>
				<td>Set</td>
				<td>{1,2,'a'}</td>
				<td>Enumerates elements to construct a set.</td>
    </tr>
		<tr>
        <td>set-comp</td>
				<td>Set comprehension</td>
				<td>{i for in 'abc'}</td>
				<td>Constructs a set through comprehension.</td>
    </tr>
		<tr>
        <td>dict</td>
				<td>Dictionary</td>
				<td>{1:2, 'a':'b', 3.0:True}</td>
				<td>Enumerates elements to construct a dictionary.</td>
    </tr>
		<tr>
        <td>dict-comp</td>
				<td>Dictionary comprehension</td>
				<td>{i:i*i for i in range(10)}</td>
				<td>Constructs a dictionary through comprehension.</td>
    </tr>
		<tr>
        <td>generator</td>
				<td>Generator</td>
				<td>(k*k for k in range(10))</td>
				<td>Returns a generator.</td>
    </tr>
		 <tr>
        <td rowspan="4">Primary expression</td>
        <td>attr</td>
				<td>Attribute reference</td>
				<td>msg.payload</td>
				<td>Returns an attribute.</td>
    </tr>
		<tr>
        <td>index</td>
				<td>Container subscript value</td>
				<td>msg.payload[1], msg.vars['a']</td>
				<td>Gets the value by subscript.</td>
    </tr>
		<tr>
        <td>slice</td>
				<td>Slice subscript</td>
				<td>msg.payload[1:3]</td>
				<td>Gets the value by subscript.</td>
    </tr>
		<tr>
        <td>call</td>
				<td>Call</td>
				<td>str('a')</td>
				<td>Calls a function.</td>
    </tr>
		 <tr>
        <td rowspan="2">Mathematical expression</td>
        <td>binop</td>
				<td>Binary operator</td>
				<td>3**3, 3+3, 'a' is not in msg.vars</td>
				<td>Exponentiation (**), arithmetic operations (+, -, *, /, //, %), shift operations (&gt;&gt;, &lt;&lt;), bitwise operations (&amp;, ^, |), and comparison operations (&gt;, &gt;=, &lt;, &lt;=, ==, !=, is, is not, in, not in) are supported.</td>
    </tr>
		<tr>
        <td>uniop</td>
				<td>Unary operator</td>
				<td>not msg.vars, ~msg.vars['no']</td>
				<td>`+` (keeps the value of the operand), `-` (produces the negative value), `~` (indicates bitwise negation), and `not` (indicates logical NOT).</td>
    </tr>
		<tr>
        <td rowspan="2">Conditional expression</td>
        <td>if-expr</td>
				<td>Conditional expression</td>
				<td>'a' if 's' in msg.vars else 'b'</td>
				<td>xx if True else xx.</td>
    </tr>
		<tr>
        <td>logical</td>
				<td>Logical expression</td>
				<td>a and b, not True</td>
				<td>Boolean operations (`and`, `not`, `or`) are supported.</td>
    </tr>
    <tr>
        <td>Special expression</td>
        <td>dataref</td>
				<td>Data reference</td>
				<td>Tags generated automatically after you click data in the drop-down list</td>
				<td>References the data in the specified path from the context.</td>
    </tr>
</table>

## Data types
The expression mode fully supports the [core types](https://www.tencentcloud.com/document/product/1165/51655#core-types) in iPaaS based on native types in Python. Data of types bound to the core types in iPaaS can freely flow between components and Dataway.
<table>
    <tr>
        <th>Data Type</th>
				<th>Core Type in iPaaS</th>
        <th>Feature</th>
				<th>Feature Type</th>
				<th>Feature Functionality</th>
				<th>Output Type</th>
    </tr>
		<tr>
        <td rowspan="19">int</td>
				<td rowspan="19">Integer</td>
        <td>+</td>
				<td>Operator</td>
				<td>Addition.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>-</td>
				<td>Operator</td>
				<td>Subtraction.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>*</td>
				<td>Operator</td>
				<td>Multiplication.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>/</td>
				<td>Operator</td>
				<td>Division.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>//</td>
				<td>Operator</td>
				<td>Floor division.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>%</td>
				<td>Operator</td>
				<td>Modulus.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>-x</td>
				<td>Operator</td>
				<td>Negative value.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>&</td>
				<td>Operator</td>
				<td>Bitwise AND.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>|</td>
				<td>Operator</td>
				<td>Bitwise OR.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>^</td>
				<td>Operator</td>
				<td>Bitwise XOR.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>~</td>
				<td>Operator</td>
				<td>Bitwise negation.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>&lt;&lt;</td>
				<td>Operator</td>
				<td>Left shift.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>&gt;&gt;</td>
				<td>Operator</td>
				<td>Right shift.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>&lt;</td>
				<td>Operator</td>
				<td>Less than.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;</td>
				<td>Operator</td>
				<td>Greater than.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&lt;=</td>
				<td>Operator</td>
				<td>Less than or equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;=</td>
				<td>Operator</td>
				<td>Greater than or equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>==</td>
				<td>Operator</td>
				<td>Equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>!=</td>
				<td>Operator</td>
				<td>Not equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td rowspan="9">str</td>
				<td rowspan="9">String</td>
        <td>+</td>
				<td>Operator</td>
				<td>Concatenation.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>*</td>
				<td>Operator</td>
				<td>Repetition.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>[index]</td>
				<td>Subscript operation</td>
				<td>Gets the value of the specified index.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>[index1:index2]</td>
				<td>Subscript operation</td>
				<td>Splices the data.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>[index1:index2:step]</td>
				<td>Subscript operation</td>
				<td>Splices the data by step.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>in</td>
				<td>Operator</td>
				<td>Returns whether the data is a substring.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>%</td>
				<td>Operator</td>
				<td>Formatting.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>==</td>
				<td>Operator</td>
				<td>Equal to</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>!=</td>
				<td>Operator</td>
				<td>Not equal to</td>
				<td>bool</td>
    </tr>
		<tr>
        <td rowspan="5">bool</td>
				<td rowspan="5">Boolean</td>
        <td>or</td>
				<td>Operator</td>
				<td>OR</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>and</td>
				<td>Operator</td>
				<td>AND</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>not</td>
				<td>Operator</td>
				<td>NOT</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>==</td>
				<td>Operator</td>
				<td>Equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>!=</td>
				<td>Operator</td>
				<td>Not equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td rowspan="13">float</td>
				<td rowspan="13">Float</td>
        <td>+</td>
				<td>Operator</td>
				<td>Addition.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>-</td>
				<td>Operator</td>
				<td>Subtraction.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>*</td>
				<td>Operator</td>
				<td>Multiplication.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>/</td>
				<td>Operator</td>
				<td>Division.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>//</td>
				<td>Operator</td>
				<td>Floor division.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>%</td>
				<td>Operator</td>
				<td>Modulus.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>-x</td>
				<td>Operator</td>
				<td>Negative value.</td>
				<td>float</td>
    </tr>
		<tr>
        <td>&lt;</td>
				<td>Operator</td>
				<td>Less than.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;</td>
				<td>Operator</td>
				<td>Greater than.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&lt;=</td>
				<td>Operator</td>
				<td>Less than or equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;=</td>
				<td>Operator</td>
				<td>Greater than or equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>==</td>
				<td>Operator</td>
				<td>Equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>!=</td>
				<td>Operator</td>
				<td>Not equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td rowspan="9">bytes</td>
				<td rowspan="9">Non-core types</td>
        <td>+</td>
				<td>Operator</td>
				<td>Concatenation.</td>
				<td>bytes</td>
    </tr>
		<tr>
        <td>*</td>
				<td>Operator</td>
				<td>Repetition.</td>
				<td>bytes</td>
    </tr>
		<tr>
        <td>[index]</td>
				<td>Subscript operation</td>
				<td>Gets the value of the specified index.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>[index1:index2]</td>
				<td>Subscript operation</td>
				<td>Splices the data.</td>
				<td>bytes</td>
    </tr>
		<tr>
        <td>[index1:index2:step]</td>
				<td>Subscript operation</td>
				<td>Splices the data by step.</td>
				<td>bytes</td>
    </tr>
		<tr>
        <td>in</td>
				<td>Operator</td>
				<td>Returns whether the data is a substring.</td>
				<td>bool</td>
    </tr>
    <tr>
        <td>%</td>
        <td>Operator</td>
        <td>Formatting.</td>
        <td>bytes</td>
    </tr>
		<tr>
        <td>==</td>
				<td>Operator</td>
				<td>Equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>!=</td>
				<td>Operator</td>
				<td>Not equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td rowspan="12">list</td>
				<td rowspan="12">List</td>
        <td>+</td>
				<td>Operator</td>
				<td>Concatenation.</td>
				<td>list</td>
    </tr>
		<tr>
        <td>*</td>
				<td>Operator</td>
				<td>Repetition.</td>
				<td>list</td>
    </tr>
		<tr>
        <td>[index]</td>
				<td>Subscript operation</td>
				<td>Gets the value of the specified index.</td>
				<td>any</td>
    </tr>
		<tr>
        <td>[index1:index2]</td>
				<td>Subscript operation</td>
				<td>Splices the data.</td>
				<td>list</td>
    </tr>
		<tr>
        <td>[index1:index2:step]</td>
				<td>Subscript operation</td>
				<td>Splices the data by step.</td>
				<td>list</td>
    </tr>
		<tr>
        <td>in</td>
				<td>Operator</td>
				<td>Returns whether the data is an element in the list.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&lt;</td>
				<td>Operator</td>
				<td>Returns whether each element in the former list is less than the corresponding element in the latter list.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;</td>
				<td>Operator</td>
				<td>Returns whether each element in the former list is greater than the corresponding element in the latter list.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&lt;=</td>
				<td>Operator</td>
				<td>Returns whether each element in the former list is less than or equal to the corresponding element in the latter list.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;=</td>
				<td>Operator</td>
				<td>Returns whether each element in the former list is greater than or equal to the corresponding element in the latter list.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>==</td>
				<td>Operator</td>
				<td>Equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>!=</td>
				<td>Operator</td>
				<td>Not equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td rowspan="3">dict</td>
				<td rowspan="3">Dictionary</td>
        <td>[key]</td>
				<td>Subscript operation</td>
				<td>Gets the value of the specified `key`.</td>
				<td>any</td>
    </tr>
		<tr>
        <td>==</td>
				<td>Operator</td>
				<td>Equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>!=</td>
				<td>Operator</td>
				<td>Not equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td rowspan="10">set</td>
				<td rowspan="10">Non-core types</td>
        <td>&</td>
				<td>Operator</td>
				<td>Intersection.</td>
				<td>set</td>
    </tr>
		<tr>
        <td>|</td>
				<td>Operator</td>
				<td>Union.</td>
				<td>set</td>
    </tr>
		<tr>
        <td>-</td>
				<td>Operator</td>
				<td>Subtraction.</td>
				<td>set</td>
    </tr>
		<tr>
        <td>&lt;</td>
				<td>Operator</td>
				<td>Returns whether the data is a proper subset.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;</td>
				<td>Operator</td>
				<td>Returns whether the data is a proper superset.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&lt;=</td>
				<td>Operator</td>
				<td>Returns whether the data is a subset.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;=</td>
				<td>Operator</td>
				<td>Returns whether the data is a superset.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>in</td>
				<td>Operator</td>
				<td>Returns whether the data is an element in the list.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>==</td>
				<td>Operator</td>
				<td>Equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>!=</td>
				<td>Operator</td>
				<td>Not equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td rowspan="12">decimal.Decimal</td>
				<td rowspan="12">Decimal</td>
        <td>+</td>
				<td>Operator</td>
				<td>Addition.</td>
				<td>decimal</td>
    </tr>
		<tr>
        <td>-</td>
				<td>Operator</td>
				<td>Subtraction.</td>
				<td>decimal</td>
    </tr>
		<tr>
        <td>*</td>
				<td>Operator</td>
				<td>Multiplication.</td>
				<td>decimal</td>
    </tr>
		<tr>
        <td>/</td>
				<td>Operator</td>
				<td>Division.</td>
				<td>decimal</td>
    </tr>
		<tr>
        <td>%</td>
				<td>Operator</td>
				<td>Modulus.</td>
				<td>decimal</td>
    </tr>
		<tr>
        <td>-x</td>
				<td>Operator</td>
				<td>Negative value.</td>
				<td>decimal</td>
    </tr>
		<tr>
        <td>&lt;</td>
				<td>Operator</td>
				<td>Less than.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;</td>
				<td>Operator</td>
				<td>Greater than.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&lt;=</td>
				<td>Operator</td>
				<td>Less than or equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;=</td>
				<td>Operator</td>
				<td>Greater than or equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>==</td>
				<td>Operator</td>
				<td>Equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>!=</td>
				<td>Operator</td>
				<td>Not equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td rowspan="15">datetime.datetime</td>
				<td rowspan="15">Date and time</td>
        <td>year</td>
				<td>Attribute</td>
				<td>Year.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>month</td>
				<td>Attribute</td>
				<td>Month.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>day</td>
				<td>Attribute</td>
				<td>Day.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>hour</td>
				<td>Attribute</td>
				<td>Hour.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>minute</td>
				<td>Attribute</td>
				<td>Minute.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>second</td>
				<td>Attribute</td>
				<td>Second.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>microsecond</td>
				<td>Attribute</td>
				<td>Microsecond.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>+</td>
				<td>Operator</td>
				<td>Moves forward the date.</td>
				<td>datetime.datetime</td>
    </tr>
		<tr>
        <td>-</td>
				<td>Operator</td>
				<td>Calculates the time interval.</td>
				<td>datetime.timedelta</td>
    </tr>
		<tr>
        <td>&lt;</td>
				<td>Operator</td>
				<td>Less than.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;</td>
				<td>Operator</td>
				<td>Greater than.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&lt;=</td>
				<td>Operator</td>
				<td>Less than or equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;=</td>
				<td>Operator</td>
				<td>Greater than or equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>==</td>
				<td>Operator</td>
				<td>Equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>!=</td>
				<td>Operator</td>
				<td>Not equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td rowspan="12">datetime.date</td>
				<td rowspan="12">Date</td>
        <td>year</td>
				<td>Attribute</td>
				<td>Year.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>month</td>
				<td>Attribute</td>
				<td>Month.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>day</td>
				<td>Attribute</td>
				<td>Day.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>strftime(format)</td>
				<td>Method</td>
				<td>Formatting.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>+</td>
				<td>Operator</td>
				<td>Moves forward the date.</td>
				<td>datetime.date</td>
    </tr>
		<tr>
        <td>-</td>
				<td>Operator</td>
				<td>Calculates the time interval.</td>
				<td>datetime.timedelta</td>
    </tr>
		<tr>
        <td>&lt;</td>
				<td>Operator</td>
				<td>Less than.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;</td>
				<td>Operator</td>
				<td>Greater than.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&lt;=</td>
				<td>Operator</td>
				<td>Less than or equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;=</td>
				<td>Operator</td>
				<td>Greater than or equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>==</td>
				<td>Operator</td>
				<td>Equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>!=</td>
				<td>Operator</td>
				<td>Not equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td rowspan="10">datetime.time</td>
				<td rowspan="10">Time</td>
        <td>hour</td>
				<td>Attribute</td>
				<td>Hour.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>minute</td>
				<td>Attribute</td>
				<td>Minute.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>second</td>
				<td>Attribute</td>
				<td>Second.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>microsecond</td>
				<td>Attribute</td>
				<td>Microsecond.</td>
				<td>int</td>
    </tr>
		<tr>
        <td>&lt;</td>
				<td>Operator</td>
				<td>Less than.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;</td>
				<td>Operator</td>
				<td>Greater than.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&lt;=</td>
				<td>Operator</td>
				<td>Less than or equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>&gt;=</td>
				<td>Operator</td>
				<td>Greater than or equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>==</td>
				<td>Operator</td>
				<td>Equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td>!=</td>
				<td>Operator</td>
				<td>Not equal to.</td>
				<td>bool</td>
    </tr>
		<tr>
        <td rowspan="6">Entity</td>
				<td rowspan="6">Binary entity</td>
        <td>from_bytes(bs,mime_type=None, encoding="utf-8")</td>
				<td>Static method</td>
				<td>Constructs an `Entity` object based on the binary data.</td>
				<td>Entity</td>
    </tr>
		<tr>
        <td>from_value(obj,mime_type=None, encoding="utf-8")</td>
				<td>Static method</td>
				<td>Constructs an `Entity` object based on the data.</td>
				<td>Entity</td>
    </tr>
		<tr>
        <td>get(key,dafault=None)</td>
				<td>Method</td>
				<td>Gets the data.</td>
				<td>any</td>
    </tr>
		<tr>
        <td>[key]</td>
				<td>Subscript operation</td>
				<td>Gets the value of the specified `key`.</td>
				<td>any</td>
    </tr>
		<tr>
        <td>[^value]</td>
				<td>Subscript operation</td>
				<td>Gets the parsed value.</td>
				<td>any</td>
    </tr>
		<tr>
        <td>[^blob]</td>
				<td>Subscript operation</td>
				<td>Gets the binary raw data.</td>
				<td>bytes</td>
    </tr>
		<tr>
        <td>RecordSet</td>
				<td>Data set</td>
        <td>schema()</td>
				<td>Method</td>
				<td>Gets the schema.</td>
				<td>dict</td>
    </tr>
		<tr>
        <td>Record</td>
				<td>Single data record</td>
        <td>[key]</td>
				<td>Subscript operation</td>
				<td>Gets the value of the specified `key`.</td>
				<td>any</td>
    </tr>
		<tr>
        <td rowspan="7">Message</td>
				<td rowspan="7">Message</td>
        <td>payload</td>
				<td>Attribute</td>
				<td>Returns the output.</td>
				<td>any</td>
    </tr>
		<tr>
        <td>attrs</td>
				<td>Attribute</td>
				<td>Returns an attribute.</td>
				<td>dict</td>
    </tr>
		<tr>
        <td>vars</td>
				<td>Attribute</td>
				<td>Returns a variable.</td>
				<td>dict</td>
    </tr>
		<tr>
        <td>id</td>
				<td>Attribute</td>
				<td>Returns the unique identifier of the message.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>seq_id</td>
				<td>Attribute</td>
				<td>Returns the flow sequence number.</td>
				<td>str</td>
    </tr>
		<tr>
        <td>error</td>
				<td>Attribute</td>
				<td>Returns an error.</td>
				<td>dict</td>
    </tr>
		<tr>
        <td>isthrowing</td>
				<td>Attribute</td>
				<td>Specifies whether to throw an error.</td>
				<td>bool</td>
    </tr>
</table>

## Other support
The expression mode provides various type methods, built-in functions, and third-party modules for you to choose as needed to quickly implement predefined features. For more information, see [Expression Mode Appendix](https://www.tencentcloud.com/document/product/1165/51658).

