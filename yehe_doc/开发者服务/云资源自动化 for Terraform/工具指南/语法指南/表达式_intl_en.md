## Operators

Operators are used for arithmetic or logical operations.

### Arithmetic operators
<table>
<tr>
<td rowspan="1" colSpan="1" ><b>Operator</b></td><td rowspan="1" colSpan="1" ><b>Description</b></td>
</tr><tr>
<td rowspan="1" colSpan="1" >a + b</td><td rowspan="1" colSpan="1" >Returns the result of adding `a` and `b` together.</td>
</tr><tr>
<td rowspan="1" colSpan="1" >a - b</td><td rowspan="1" colSpan="1" >Returns the result of subtracting `b` from `a`.</td>
</tr><tr>
<td rowspan="1" colSpan="1" >a * b</td><td rowspan="1" colSpan="1" >Returns the result of multiplying `a` and `b`.</td>
</tr><tr>
<td rowspan="1" colSpan="1" >a / b</td><td rowspan="1" colSpan="1" >Returns the result of dividing `a` by `b`.</td>
</tr><tr>
<td rowspan="1" colSpan="1" >a % b</td><td rowspan="1" colSpan="1" >Returns the remainder of dividing `a` by `b`. This operator is generally useful only when used with whole numbers.</td>
</tr><tr>
<td rowspan="1" colSpan="1" >-a</td><td rowspan="1" colSpan="1" >Returns the result of multiplying `a` by -1.</td>
</tr>
</table>


### Comparison operators
<table>
<tr>
<td rowspan="1" colSpan="1" ><b>Operator</b></td><td rowspan="1" colSpan="1" ><b>Description</b></td>
</tr><tr>
<td rowspan="1" colSpan="1" >a == b</td><td rowspan="1" colSpan="1" >Returns `true` if `a` and `b` both have the same type and the same value, or `false` otherwise.</td>
</tr><tr>
<td rowspan="1" colSpan="1" >a != b</td><td rowspan="1" colSpan="1" >Contrary to `==`.</td>
</tr><tr>
<td rowspan="1" colSpan="1" >a < b</td><td rowspan="1" colSpan="1" >Returns `true` if `a` is less than `b`, or `false` otherwise.</td>
</tr><tr>
<td rowspan="1" colSpan="1" >a > b</td><td rowspan="1" colSpan="1" >Returns `true` if `a` is greater than `b`, or `false` otherwise.</td>
</tr><tr>
<td rowspan="1" colSpan="1" >a <= b</td><td rowspan="1" colSpan="1" >Returns `true` if `a` is less than or equal to `b`, or `false` otherwise.</td>
</tr><tr>
<td rowspan="1" colSpan="1" >a >= b</td><td rowspan="1" colSpan="1" >Returns `true` if `a` is greater than or equal to `b`, or `false` otherwise.</td>
</tr>
</table>


### Logical operators
<table>
<tr>
<td rowspan="1" colSpan="1" ><b>Operator</b></td><td rowspan="1" colSpan="1" ><b>Description</b></td>
</tr><tr>
<td rowspan="1" colSpan="1" >a || b</td><td rowspan="1" colSpan="1" >Returns `true` if either `a` or `b` is `true`, or `false` if both are `false`.</td>
</tr><tr>
<td rowspan="1" colSpan="1" >a && b</td><td rowspan="1" colSpan="1" >Returns `true` if both `a` and `b` are `true`, or `false` if either one is `false`.</td>
</tr><tr>
<td rowspan="1" colSpan="1" >!a</td><td rowspan="1" colSpan="1" >Returns `true` if `a` is `false`, or `false` if `a` is `true`.</td>
</tr>
</table>


## Conditional Expression

A conditional expression uses the value of a Boolean expression to select one of two values. For example:
``` bash
condition ? one_value : two_value
```

## for Expression

A `for` expression can be used to traverse a set of collections and map one collection type to another. For example:
``` bash
[for item in items : upper(item)]
```

## Splat Expression

A splat expression provides a more concise way to express a common operation that could otherwise be performed with a for expression. For example:
``` bash
[for o in var.list : o.id]
is equivalent to
var.list[*].id
```

## Function Expression

Terraform supports the use of some built-in functions when expressions are calculated. An expression to call a function is similar to an operator. For example:
``` html
upper("123")
```

