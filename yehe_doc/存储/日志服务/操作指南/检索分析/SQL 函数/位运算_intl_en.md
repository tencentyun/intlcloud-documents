This document introduces the basic syntax and examples of bitwise operation functions.

| Function     | Syntax                | Description                                                         |
| --------------- | ------------------ | --------------------------------------- |
| [bit_count](#bit_count)   | bit_count(x, bits) | Returns the number of ones in `x` in binary representation.            |
| [bitwise_and](#bitwise_and) | bitwise_and(x, y)  | Returns the result of the bitwise AND operation on `x` and `y` in binary representation.        |
| [bitwise_not](#bitwise_not) | bitwise_not(x)     | Inverts all bits of `x` in binary representation. |
| [bitwise_or](#bitwise_or)  | bitwise_or(x, y)   | Returns the result of the bitwise OR operation on `x` and `y` in binary representation.          |
| [bitwise_xor](#bitwise_xor) | bitwise_xor(x, y)  | Returns the result of the bitwise XOR operation on `x` and `y` in binary representation.        |


<span id="bit_count"></span>
## bit_count

The `bit_count` function is used to return the number of ones in `x`.

### Syntax

```
bit_count(x, bits)
```

### Parameter description

| Parameter         | Description              |
| ---- | -------------------- |
| x    | The parameter value is of the bigint type. |
| bits | Number of bits, for example, 64 bits.     |

### Return value type

Bigint

### Example

Compute the binary representation of the number 24 and return the number of ones in the binary number.

- Query and analysis statement
```
* | SELECT bit_count(24, 64)
```
- Query and analysis result


<span id="bitwise_and"></span>
## bitwise_and

The `bitwise_and` function is used to return the result of the bitwise AND operation on `x` and `y` in binary representation.

### Syntax

```
bitwise_and(x, y)
```

### Parameter description

| Parameter         | Description              |
| ---- | -------------------- |
| x    | The parameter value is of the bigint type. |
| y    | The parameter value is of the bigint type. |

### Return value type

Bigint

### Example

Perform an AND operation on numbers 3 and 5 in binary form.

- Query and analysis statement
```
* | SELECT bitwise_and(3, 5)
```
- Query and analysis result


<span id="bitwise_not"></span>
## bitwise_not

The `bitwise_not` function is used to invert all bits of `x` in binary representation.

### Syntax

```
bitwise_not(x)
```

### Parameter description

| Parameter         | Description              |
| ---- | -------------------- |
| x    | The parameter value is of the bigint type. |

### Return value type

Bigint

### Example

Invert all bits of the number 4 in binary form.

- Query and analysis statement
```
* | SELECT bitwise_not(4)
```
- Query and analysis result



<span id="bitwise_or"></span>
## bitwise_or

The `bitwise_or` function is used to return the result of the bitwise OR operation on `x` and `y` in binary representation.

### Syntax

```
bitwise_or(x, y)
```

### Parameter description

| Parameter         | Description              |
| ---- | -------------------- |
| x    | The parameter value is of the bigint type. |
| y    | The parameter value is of the bigint type. |

### Return value type

Bigint

### Example

Perform an OR operation on numbers 3 and 5 in binary representation.

- Query and analysis statement
```
* | SELECT bitwise_or(3, 5)
```
- Query and analysis result


<span id="bitwise_xor"></span>
## bitwise_xor

The `bitwise_xor` function is used to return the result of the bitwise XOR operation on `x` and `y` in binary representation.

### Syntax

```
bitwise_xor(x, y)
```

### Parameter description

| Parameter         | Description              |
| ---- | -------------------- |
| x    | The parameter value is of the bigint type. |
| y    | The parameter value is of the bigint type. |

### Return value type

Bigint

### Example

Perform an XOR operation on numbers 3 and 5 in binary representation.

- Query and analysis statement
```
* | SELECT bitwise_xor(3, 5)
```
- Query and analysis result


