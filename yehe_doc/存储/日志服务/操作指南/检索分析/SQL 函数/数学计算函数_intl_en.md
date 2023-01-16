This document introduces the basic syntax and examples of mathematical calculation functions.

CLS's log analysis feature allows you to analyze logs by analyzing fields of int, long, and double types via mathematical calculation functions and mathematical statistical functions.

>?
> - Mathematical calculation functions support operators +-\*/%.
> - `x` and `y` in the following functions can be numbers, log fields, or expressions with numerical calculation results.
> 

## Basic Syntax

| Function                   | Description                                                         |
| -------------------------- | -------------------------------- |
| abs(x) [](id:abs)                    | Returns the absolute value of `x`.               |
| cbrt(x)   [](id:cbrt)                 | Returns the cube root of `x`.               |
| sqrt(x)   [](id:sqrt)                 | Returns the square root of `x`.               |
| cosine_similarity(x,y) [](id:cosine_similarity)    | Returns the cosine similarity between the vectors `x` and `y`.</br>For example, `* \| SELECT cosine_similarity(MAP(ARRAY['x','y'], ARRAY[1.0,0.0]), MAP(ARRAY['x','y'], ARRAY[0.0,1.0]))` returns 0.       |
| degrees(x)  [](id:degrees)               | Converts angle `x` in radians to degrees.                 |
| radians(x)   [](id:radians)              | Converts angle `x` in degrees to radians.                 |
| e()  [](id:e)                      | Returns the natural logarithm of the number.             |
| exp(x) [](id:exp)                    | Returns the exponent of the natural logarithm.             |
| ln(x)  [](id:ln)                    | Returns the natural logarithm of `x`.             |
| log2(x)  [](id:log2)                  | Returns the base-2 logarithm of `x`.              |
| log10(x) [](id:log10)                  | Returns the base-10 logarithm of `x`.              |
| log(x,b)    [](id:log)               | Returns the base-b logarithm of `x`.              |
| pi() [](id:pi)                      | Returns the value of Pi, accurate to 14 decimal places.        |
| pow(x,b) [](id:pow)                  | Returns `x` raised to the power of `b`.                |
| rand() [](id:rand)                    | Returns a random value.                     |
| random(0,n)[](id:random)                | Returns a random number within the [0,n) range.          |
| round(x) [](id:round_1)                  | Returns the rounded value of `x`.           |
| round(x, N)   [](id:round_2)             | Returns `x` rounded to `N` decimal places.              |
| floor(x) [](id:floor)                  | Returns `x` rounded down to the nearest integer.                     |
| ceiling(x）[](id:ceiling)                | Returns `x` rounded up to the nearest integer.                     |
| from_base(varchar, bigint)[](id:from_base) | Converts a string into a number based on BASE encoding.   |
| to_base(x, radix)[](id:to_base)          | Converts a number into a string based on BASE encoding.   |
| truncate(x)  [](id:truncate)              | Returns `x` rounded to an integer by dropping digits after the decimal point.             |
| acos(x)  [](id:acos)                  | Returns the arc cosine of `x`.               |
| asin(x)  [](id:asin)                  | Returns the arc sine of `x`.               |
| atan(x) [](id:atan)                   | Returns the arc tangent of `x`.               |
| atan2(y,x)  [](id:atan2)               | Returns the arc tangent of the result of dividing `y` by `x`. |
| cos(x) [](id:cos)                    | Returns the cosine of `x`.                 |
| sin(x) [](id:sin)                    | Returns the sine of `x`.                 |
| cosh(x) [](id:cosh)                  | Returns the hyperbolic cosine of `x`.             |
| tan(x) [](id:tan)                    | Returns the tangent of `x`.                 |
| tanh(x) [](id:tanh)                   | Returns the hyperbolic tangent of `x`.             |
| infinity()  [](id:infinity)               | Returns the constant representing positive infinity.               |
| is_nan(x)  [](id:is_nan)                | Determines if the target value is Not a Number (NaN).         |
| nan()   [](id:nan)             |  Returns a "Not a Number" (NaN) value.        ||
| mod(x, y) [](id:mod)               | Returns the remainder when `x` is divided by `y`.         |
| sign(x) [](id:sign)               | Returns the sign of `x` represented by 1, 0, or -1.         |
| width_bucket(x, bound1, bound2, n) [](id:width_bucket_1)               |  Returns the bucket number of `x` in an equi-width histogram, with `n` buckets within bounds of bound1 and bound2. </br>For example, `* \| select timeCost,width_bucket(timeCost,10,1000,5)`        |
| width_bucket(x, bins)[](id:width_bucket_2)                | Returns the bin number of `x` with specific bins specified by the array `bins`. </br>For example, `* \| select timeCost,width_bucket(timeCost,array[10,100,1000])`        |


## Examples

To compare the PV values of today and yesterday and express the result as a percentage, the query and analysis statement is as follows:
```
* | SELECT diff [1] AS today, round((diff [3] -1.0) * 100, 2) AS growth FROM (SELECT compare(pv, 86400) as diff FROM (SELECT COUNT(*) as pv FROM log))
```

