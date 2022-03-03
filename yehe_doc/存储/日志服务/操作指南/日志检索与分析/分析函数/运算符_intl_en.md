
An operator is a reserved word or a character used primarily to specify conditions in a SQL statement and to serve as conjunctions for multiple conditions in a SQL statement.

- [Mathematical operators](#.E7.AE.97.E6.9C.AF.E8.BF.90.E7.AE.97.E7.AC.A6)
- [Comparison operators](#.E6.AF.94.E8.BE.83.E8.BF.90.E7.AE.97.E7.AC.A6)
- [Logical operators](#.E9.80.BB.E8.BE.91.E8.BF.90.E7.AE.97.E7.AC.A6)

## Mathematical Operators

Mathematical operators are symbols used to process four arithmetic operations. They are the simplest and most commonly used operators, especially for number processing. Almost all number processing involves mathematical operators.

Assume variable `a` holds 1 and variable `b` holds 2, then:

| Operator | Description                                          | Instance  |
| ------ | --------------------------------------------- | ----- |
| + (Addition)      | Adds values on either side of the operator.                      | a + b |
| - (Subtraction)     | Subtracts the right hand operand from the left hand operand.                | a - b |
| * (Multiplication)     | Multiplies values on either side of the operator.                   | a * b |
| / (Division)     | Divides the left hand operand by the right hand operand.             | b / a |
| % (Modulus)     | Divides the left hand operand by the right hand operand and returns the remainder. | b % a |

## Comparison Operators

Comparison operators are used to determine the size relationships of values and support any value type that can be compared, such as int, long, double, and text.

Assume variable `a` holds 1 and variable `b` holds 2, then:

| Operator | Description                                                         | Instance              |
| :----- | :----------------------------------------------------------- | :---------------- |
| =      | Checks if the values of two operands are equal or not. If yes, the condition is true.             | a = b             |
| !=      | Checks if the values of two operands are equal or not. If no, the condition is true.             | a != b             |
| <>      | Checks if the values of two operands are equal or not. If no, the condition is true.             | a <> b             |
| >      | Checks if the value of the left operand is greater than the value of the right operand. If yes, the condition is true. | a > b |
| <      | Checks if the value of the left operand is less than the value of the right operand. If yes, the condition is true. | a < b |
| >=      | Checks if the value of the left operand is greater than or equal to the value of the right operand. If yes, the condition is true. | a >= b |
| <=      | Checks if the value of the left operand is less than or equal to the value of the right operand. If yes, the condition is true. | a <= b |
| IN      | The IN operator is used to compare a value with a specified list of values.          |  status IN (200,206,404) |
| NOT IN  | The NOT IN operator is used to compare a value with values that are not in a specified list. It is the opposite of the IN operator. | status NOT IN (200,206,404)  |
| BETWEEN AND | The BETWEEN operator tests if a value is within a specified range (BETWEEN min AND max). | status between 200 AND 400 |
| LIKE    | The LIKE operator is used to compare a value with a similar value using the wildcard operator. The percent sign (%) represents zero, one, or multiple characters. The underscore (_) represents a single digit or character.  | url LIKE '%.mp4' |
| IS NULL | The NULL operator compares a value with NULL. If the value is null, the condition is true. | status IS NULL |
| IS NOT NULL | The NULL operator compares a value with NULL. If the value is not null, the condition is true. | status IS NOT NULL |


## Logical Operators

| Operator  | Description                                                         |
| :------ | :----------------------------------------------------------- |
| AND     | The AND operator determines that the result is true if the conditions on both sides of the operator exist at the same time.                   |
| OR      | The OR operator determines that the result is true if either of the conditions on both sides of the operator exists.                  |
| NOT     | The NOT operator is the opposite of the logical operator used. Examples: NOT EXISTS, NOT BETWEEN, NOT IN |
