Common logical operators are AND, OR, NOT, with three result values TRUE, FALSE, and NULL, where NULL represents an unknown value.

| a     | b     | a AND b | a OR b | NOT a |
| ----- | ----- | ------- | ------ | ----- |
| TRUE  | TRUE  | TRUE    | TRUE   | FALSE |
| TRUE  | FALSE | FALSE   | TRUE   | FALSE |
| TRUE  | NULL  | NULL    | TRUE   | FALSE |
| FALSE | FALSE | FALSE   | FALSE  | TRUE  |
| FALSE | NULL  | FALSE   | NULL   | TRUE  |
| NULL  | NULL  | NULL    | NULL   | NULL  |
