## Mathematical Operators
| **Operator** | **Description**               | **Example** | **Result** |
| ---------- | ---------------------- | -------- | -------- |
| +          | Addition                     | 3  + 4   | 7        |
| -          | Subtraction                     | 10  - 9  | 1        |
| *          | Multiplication                     | 3  * 5   | 15       |
| /          | Division (integer division truncates the result) | 10  / 4  | 2        |
| %          | Modulo (remainder)             | 6  % 4   | 2        |
| ^          | Exponentiation                   | 2  ^ 3   | 8        |
| \|/        | Square root                 | \|/  16  | 4        |
| \|\|/      | Cube root                 | \|\|/  8 | 2        |
| !          | Factorial                   | 5  !     | 120      |
| !!         | Factorial as a prefix operator     | !!  5    | 120      |
| @          | Absolute value                 | @  (-5)  | 5        |
| &          | Bitwise AND                 | 2  & 3   | 2        |
| \|         | Bitwise OR                 | 2  \| 3  | 3        |
| #          | Bitwise XOR               | 2  # 3   | 1        |
| ~          | Bitwise NOT               | ~  2     | -3       |
| <<         | Bitwise shift left               | 2  << 3  | 16       |
| >>         |  Bitwise shift right               | 8  >> 2  | 2        |

The bitwise operators work only on integral data types and are also available for the bit string types `bit` and `bit varying`. Other operators work on all numeric data types.

## Mathematical Functions
| **Function**                         | **Description**                          | **Example**          | **Result**             |
| ----------------------- | ----------------------------- | -------------------------- | -------------------- |
| abs(x)                         | Absolute value                         | abs(-17.4)                       | 17.4                 |
| cbrt(dp)                             | Cube root                                | cbrt(27.0)                     | 3                    |
| ceil(dp or numeric)             | Nearest integer greater than or equal to argument                | ceil(-42.8)                                 | -42                  |
| ceiling(dp or numeric)           | Nearest integer greater than or equal to argument (same as `ceil`)    | ceiling(-95.3)               | -95                  |
| degrees(dp)                           | Radians to degrees                | degrees(0.5)                              | 28.6478897565412     |
| div(y numeric, x numeric)         | Integer quotient of `y/x`                         | div(9,4)                        | 2                    |
| exp(dp or numeric)                   | Exponential                         | exp(1.0)                    | 2.7182818284590452   |
| floor(dp or numeric)                   | Nearest integer less than or equal to argument               | floor(-42.8)                          | -43                  |
| ln(dp or numeric)                        | Natural logarithm                              | ln(2.0)                                  | 0.6931471805599453   |
| log(dp or numeric)                      | Base 10 logarithm             | log(100.0)                | 2.0000000000000000   |
| log(b numeric, x numeric)            | Logarithm to base `b`              | log(2.0,  64.0)           | 6.0000000000000000   |
| mod(y, x)                                      | Remainder of `y/x`                | mod(9,4)                       | 1                    |
| pi()                                             | "π" constant                       | pi()                      | 3.14159265358979     |
| power(a dp, b dp)                       | `a` raised to the power of `b`              | power(9.0,  3.0)                | 729.0000000000000000 |
| power(a numeric, b numeric)             | `a` raised to the power of `b`              | power(9.0,  3.0)       | 729.0000000000000000 |
| radians(dp)                               | Degrees to radians             | radians(45.0)              | 0.785398163397448    |
| round(dp or numeric)                    | Rounds to nearest integer        | round(42.4)            | 42                   |
| round(v numeric, s int)               | Rounds to `s` decimal places            | round(42.4382,  2)        | 42.44            |
| scale(numeric)                        | Scale of the argument (the number of decimal digits in the fractional part)    | scale(8.41)          | 2                    |
| sign(dp or numeric)                       | Sign of the argument (-1, 0, +1)        | sign(-8.4)         | -1                   |
| sqrt(dp or numeric)                      | Square root                     | sqrt(2.0)                    | 1.414213562373095    |
| trunc(dp or numeric)                 | Truncates toward zero            | trunc(42.8)                | 42                   |
| trunc(v numeric, s int)              | Truncates to `s` decimal places      | trunc(42.4382,  2)         | 42.43                |
| width_bucket(operand dp, b1dp, b2 dp, count int)             | Returns the bucket number to which `operand` would be assigned in a histogram having `count` equal-width buckets spanning the range `b1` to `b2`; returns `0` or `count+1` for an input outside the range | width_bucket(5.35,  0.024, 10.06, 5)                         | 3                    |
| width_bucket(operand numeric, b1 numeric, b2 numeric, countint) | Returns the bucket number to which `operand` would be assigned in a histogram having `count` equal-width buckets spanning the range `b1` to `b2`; returns `0` or `count+1` for an input outside the range  | width_bucket(5.35,  0.024, 10.06, 5)                         | 3                    |
| width_bucket(operandanyelement, thresholdsanyarray)          | Returns the bucket number to which `operand` would be assigned given an array listing the lower bounds of the buckets; returns `0` for an input less than the first lower bound; the `thresholds` array must be sorted, smallest first, or unexpected results will be obtained | width_bucket(now(),  array['yesterday', 'today', 'tomorrow']::timestamptz[]) | 2                    |

## Random Functions
| **Function**    | **Return Type** | **Description**                                                     |
| ----------- | ------------ | ------------------------------------------------------------ |
| random()    | dp           | Random value in the range 0.0 <= x < 1.0                                 |
| setseed(dp) | viod         | Sets seed for subsequent `random()` calls (value between -1.0 and 1.0, inclusive) |

## Trigonometric Functions
All trigonometric functions take arguments and return values of type `double precision`.
Trigonometric function augments are in radians.
Returned values of inverse functions are in radians.

| **Function (Radians)** | **Function (Degrees) ** | **Description**    |
| ---------------- | ---------------- | ----------- |
| acos(x)          | acosd(x)         | Inverse cosine        |
| asin(x)          | asind(x)         | Inverse sine      |
| atan(x)          | atand(x)         | Inverse tangent      |
| atan2(y,  x)     | atan2d(y,  x)    | Inverse tangent of `y/x` |
| cos(x)           | cosd(x)          | Cosine        |
| cot(x)           | cotd(x)          | Cotangent        |
| sin(x)           | sind(x)          | Sine        |
| tan(x)           | tand(x)          | Tangent        |

