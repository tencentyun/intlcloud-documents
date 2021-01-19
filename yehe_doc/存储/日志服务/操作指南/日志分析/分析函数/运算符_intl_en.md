

An operator is a reserved word or character mainly used to specify conditions in an SQL statement and connect multiple conditions in the statement.

- [Arithmetic Operators](#.E7.AE.97.E6.9C.AF.E8.BF.90.E7.AE.97.E7.AC.A6)
- [Relational Operators](#.E6.AF.94.E8.BE.83.E8.BF.90.E7.AE.97.E7.AC.A6)
- [Logical Operators](#.E9.80.BB.E8.BE.91.E8.BF.90.E7.AE.97.E7.AC.A6)

## Arithmetic Operators

Arithmetic operators are the symbols used to process the four arithmetic operations. They are the simplest and most commonly used operators, especially when dealing with numbers.

Suppose variable a = 1 and variable b = 2, then:

| Operator | Description | Example |
| ------ | --------------------------------------------- | ----- |
| + | Addition: adds the values on both sides of the operator | a + b |
| - | Subtraction: subtracts the value on the right side of the operator from the value on the left side of the operator | a - b |
| * | Multiplication: multiplies the values on both sides of the operator | a * b |
| / | Division: divides the value on the left side of the operator by the value on the right side of the operator | b / a |
| % | Modulo: gets the remainder after dividing the value on the left side of the operator by the value on the right side of the operator | b % a |

## Relational Operators

Relational operators are used to determine the relation between values and support any comparable types such as `int`, `long`, `double`, and `text`.

Suppose variable a = 1 and variable b = 2, then:

| Operator | Description | Example |
| :----- | :----------------------------------------------------------- | :---------------- |
| = | Determines whether the values on both sides of the operator are equal, and if so, the condition is true. | a = b |
| != | Determines whether the values on both sides of the operator are equal, and if not, the condition is true. | a != b |
| <> | Determines whether the values on both sides of the operator are equal, and if not, the condition is true. | a <> b |
| > | Determines whether the value on the left side of the operator is greater than the value on the right side of the operator, and if so, the condition is true. | a > b |
| < | Determines whether the value on the left side of the operator is less than the value on the right side of the operator, and if so, the condition is true. | a < b |
| >= | Determines whether the value on the left side of the operator is greater than or equal to the value on the right side of the operator, and if so, the condition is true. | a >= b |
| <= | Determines whether the value on the left side of the operator is less than or equal to the value on the right side of the operator, and if so, the condition is true. | a <= b |
| IN | Compares a value with values in a specified series. | status IN (200,206,404) |
| NOT IN | Compares a value with values not in a specified series (i.e., the opposite of the IN operator). | status NOT IN (200,206,404) |
| BETWEEN AND | Searches for a value in a value range between the given minimum and maximum values. | status between 200 AND 400 |
| LIKE | Compares a value with similar values using wildcard operators. `%` represents zero, one, or more characters. `_` represents one single digit or character. | url LIKE '%.mp4' |
| IS NULL | Compares a value with the NULL value, and if null, the condition is true. | status IS NULL |
| IS NOT NULL | Compares a value with the NULL value, and if not null, the condition is true. | status IS NOT NULL |


## Logical Operators

| Operator | Description |
| :------ | :----------------------------------------------------------- |
| AND | The AND operator requires all conditions on both sides of the operator to be true for the result to be true. |
| OR | The OR operator requires any condition on either side of the operator to be true for the result to be true. |
| NOT | The NOT operator is the opposite of the logical operator used, such as NOT EXISTS, NOT BETWEEN, and NOT IN. |
