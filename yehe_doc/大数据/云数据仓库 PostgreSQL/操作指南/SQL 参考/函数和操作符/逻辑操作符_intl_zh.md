常用的逻辑操作符有 AND、OR、NOT，有三个结果值 TRUE、FALSE、NULL。其中 NULL 代表未知值。

| a     | b     | a AND b | a OR b | NOT a |
| ----- | ----- | ------- | ------ | ----- |
| TRUE  | TRUE  | TRUE    | TRUE   | FALSE |
| TRUE  | FALSE | FALSE   | TRUE   | FALSE |
| TRUE  | NULL  | NULL    | TRUE   | FALSE |
| FALSE | FALSE | FALSE   | FALSE  | TRUE  |
| FALSE | NULL  | FALSE   | NULL   | TRUE  |
| NULL  | NULL  | NULL    | NULL   | NULL  |
