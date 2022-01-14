
## Operators
Operators are used for arithmetic or logical operations.

### Arithmetic operators
- **a + b**: returns the result of adding `a` and `b` together.
- **a - b**: returns the result of subtracting `b` from `a`.
- **a * b**: returns the result of multiplying `a` and `b`.
- **a / b**: returns the result of dividing `a` by `b`.
- **a % b**: returns the remainder of dividing `a` by `b`. This operator is generally useful only when used with whole numbers.
- **-a**: returns the result of multiplying `a` by -1.

### Comparison operators
- **a == b**: returns `true` if `a` and `b` both have the same type and the same value, or `false` otherwise.
- **a != b**: is the opposite of `a == b`.
- **a < b**: returns `true` if `a` is less than `b`, or `false` otherwise.
- **a > b**: returns `true` if `a` is greater than `b`, or `false` otherwise.
- **a <= b**: returns `true` if `a` is less than or equal to `b`, or `false` otherwise.
- **a >= b**: returns `true` if `a` is greater than or equal to `b`, or `false` otherwise.


### Logical operators
- **a || b**: returns `true` if either `a` or `b` is `true`, or `false` if both are `false`.
- **a && b**: returns `true` if both `a` and `b` are `true`, or `false` if either one is `false`.
- **!a**: returns `true` if `a` is `false`, or `false` if `a` is `true`.


## Conditional Expression
A conditional expression uses the value of a Boolean expression to select one of two values. For example:
```bash
condition ? one_value : two_value
```


## for Expression
A `for` expression can be used to traverse a set of collections and map one collection type to another. For example:
```bash
[for item in items : upper(item)]
```


## Expanded Expression
An expanded expression is a concise expression similar to a `for` expression. For example:
```bash
[for o in var.list : o.id]
is equivalent to
var.list[*].id
```

## Function Expression
Terraform supports the use of some built-in functions when expressions are calculated. An expression to call a function is similar to an operator. For example:
```bash
upper("123")
```
