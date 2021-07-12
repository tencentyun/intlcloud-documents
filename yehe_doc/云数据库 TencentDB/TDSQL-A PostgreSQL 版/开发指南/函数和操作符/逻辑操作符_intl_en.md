Usual logical operators include `AND`, `OR`, `NOT`, and their results can be true, false, and `null`, with `null` representing "unknown". The calculation rules are as listed below:

| **a** | **b** | **a AND b** | **a OR b** | **NOT a** |
| ----- | ----- | ----------- | ---------- | --------- |
| TRUE  | TRUE  | TRUE        | TRUE       | FALSE     |
| TRUE  | FALSE | FALSE       | TRUE       | FALSE     |
| TRUE  | NULL  | NULL        | TRUE       | FALSE     |
| FALSE | FALSE | FALSE       | FALSE      | TRUE      |
| FALSE | NULL  | FALSE       | NULL       | TRUE      |
| NULL  | NULL  | NULL        | NULL       | NULL      |
