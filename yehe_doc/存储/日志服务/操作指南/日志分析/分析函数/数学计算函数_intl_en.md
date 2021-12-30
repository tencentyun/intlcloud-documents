This document introduces the basic syntax and examples of mathematical calculation functions.

CLS's log analysis feature allows you to analyze logs by analyzing fields of int, long, and double types via mathematical calculation functions and mathematical statistical functions.

>?
> - Mathematical calculation functions support operators +—\*/%.
> - `x` and `y` in the following functions can be numbers, log fields, or expressions whose calculation results are numbers.
> 

## Basic Syntax

| Function                   | Description                                                         |
| -------------------------- | -------------------------------- |
| abs(x)                     | Returns the absolute value of `x`.               |
| cbrt(x)                    | Returns the cube root of `x`.               |
| sqrt(x)                    | Returns the square root of `x`.               |
| cosine_similarity(x,y)     | Returns the cosine similarity between the sparse vectors `x` and `y`.       |
| degrees(x)                 | Converts angle `x` in radians to degrees.                 |
| radians(x)                 | Converts angle `x` in degrees to radians.                 |
| e()                        | Returns the natural logarithm of the number.             |
| exp(x)                     | Returns the exponent of the natural logarithm.             |
| ln(x)                      | Returns the natural logarithm of `x`.             |
| log2(x)                    | Returns the base-2 logarithm of `x`.              |
| log10(x)                    | Returns the base-10 logarithm of `x`.              |
| log(x,b)                   | Returns the base-b logarithm of `x`.              |
| pi()                       | Returns the value of Pi, accurate to 14 decimal places.        |
| pow(x,b)                   | Returns `x` raised to the power of `b`.                |
| rand()                     | Returns a random value.                     |
| random(0,n)                | Returns a random number within the [0,n) range.          |
| round(x)                   | Returns the rounded value of `x`.           |
| round(x, N)                | Returns `x` rounded to `N` decimal places.              |
| floor(x)                   | Returns `x` rounded down to the nearest integer.                     |
| ceiling(x)                | Returns `x` rounded up to the nearest integer.                     |
| from_base(varchar, bigint) | Converts a string into a number based on BASE encoding.   |
| to_base(x, radix)          | Converts a number into a string based on BASE encoding.   |
| truncate(x)                | Returns `x` rounded to an integer by dropping digits after the decimal point.             |
| acos(x)                    | Returns the arc cosine of `x`.               |
| asin(x)                    | Returns the arc sine of `x`.               |
| atan(x)                    | Returns the arc tangent of `x`.               |
| atan2(y,x)                 | Returns the arc tangent of the result of dividing `y` by `x`. |
| cos(x)                     | Returns the cosine of `x`.                 |
| sin(x)                     | Returns the sine of `x`.                 |
| cosh(x)                    | Returns the hyperbolic cosine of `x`.             |
| tan(x)                     | Returns the tangent of `x`.                 |
| tanh(x)                    | Returns the hyperbolic tangent of `x`.             |
| infinity()                 | Returns the constant representing positive infinity.               |
| is_nan(x)                  | Determines if `x` is not-a-number.         |

## Example

To compare the PV values of today and yesterday and express the result as a percentage, the query and analysis statement is as follows:
```
* | SELECT diff [1] AS today, round((diff [3] -1.0) * 100, 2) AS growth FROM (SELECT compare(pv, 86400) as diff FROM (SELECT COUNT(*) as pv FROM log))
```

