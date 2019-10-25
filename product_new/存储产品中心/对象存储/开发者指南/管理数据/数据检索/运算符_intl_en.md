
COS Select supports the following operators:

| Operator Type | Operator |
| -------------- | ------------------------------------------------------------ |
| Logical operator | AND, NOT, OR |
| Comparison operator | <, >, <= ,>= , = , <>, !=, BETWEEN, IN, such as `IN ('a', 'b', 'c')` |
| Pattern matching operator | LIKE |
| Mathematical operator | +, -, *, % |

## Priority of Operators

The following table shows the priority of operators in descending order:

| Operator/Element | Association | Use Case |
| :---------- | :----- | :------------- |
| - | Right | Unary subtraction |
| \*, /, % | Left | Multiplication, division, and modulo |
| +, - | Left | Addition and subtraction |
| IN | - | Setting membership |
| BETWEEN | - | In the range of () |
| LIKE | - | String pattern matching |
| <> | - | Less than and greater than |
| = | Right | Equivalence and assignment |
| NOT | Right | Logical NOT |
| AND | Left | Logical AND |
| OR | Left | Logical OR |
