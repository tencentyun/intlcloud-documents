This document introduces the basic syntax and examples of logic functions.

### Logical operators

| Operator | Description                                     | Example    |
| ------ | ---------------------------------------- | ------- |
| AND    | The result is TRUE only if both the left and right operands are TRUE. | a AND b |
| OR     | The result is TRUE if either of the left and right operands is TRUE.   | a OR b  |
| NOT    | The result is FALSE only if the right operand is FALSE.     | NOT a   |

### NULL-related logical operations
The following truth tables demonstrate the processing of cases where `a` and `b` are TRUE, FALSE, and NULL:

**AND and OR truth table**

| a     | b     | a AND b | a OR b |
| ----- | ----- | ------- | ------ |
| TRUE  | TRUE  | TRUE    | TRUE   |
| TRUE  | FALSE | FALSE   | TRUE   |
| TRUE  | NULL  | NULL    | TRUE   |
| FALSE | TRUE  | FALSE   | TRUE   |
| FALSE | FALSE | FALSE   | FALSE  |
| FALSE | NULL  | FALSE   | NULL   |
| NULL  | TRUE  | NULL    | TRUE   |
| NULL  | FALSE | FALSE   | NULL   |
| NULL  | NULL  | NULL    | NULL   |

**NOT truth table**

| a     | NOT a |
| ----- | ----- |
| TRUE  | FALSE |
| FALSE | TRUE  |
| NULL  | NULL  |

