
### Basic Type
A basic type is simple and not composed of any other types. All basic types in Terraform are represented by the `type` keyword. Available basic types include:
- `string`: represents a Unicode character sequence of some text (such as "hello").
- `number`: represents a number, which can be an integer or a decimal.
- `bool`: represents a Boolean value, which can be `true` or `false`.

Below is an example:
```bash
id = 123
vpc_id = "123"
status = true
```


### Composite Type
A composite type is a set of values.

#### Collection type
A collection contains a set of values of the same type:
- `list(...)`: is a sequence of values identified by consecutive integers starting from 0.
- `map(...)`: is a set of values, each of which is identified by a string label.
- `set(...)`: is a set of unique values.

#### Structure type
- `object(...)`: is a custom type that contains its own named attributes.
- `tuple(...)`: is a sequence of elements identified by consecutive integers starting from 0, where each element has its own type.

#### Special type
- `null`: an argument set to null is considered not entered. Terraform will automatically ignore the argument and use the default value.
- `any`: it is a very special type constraint in Terraform. It is not a type but simply a placeholder. Whenever a value is given a complex type constrained by `any`, Terraform will try to calculate the most accurate type to replace `any`.

### Argument
Argument assignment means assigning a value to a specific argument, whose name can contain letters, digits, underscores, and hyphens and cannot begin with a digit, such as:
```bash
id = "123"
```

### Block
A block is a container containing a set of arguments, such as:
```bash
resource "tencentcloud_instance" "foo" {
    tags                                    = {}
    vpc_id                                  = "vpc-5bt2ix8p"
}

```

### Comment
Terraform supports the following three types of comments:
- `#`: a single-line comment followed by the comment content.
- `//`: a single-line comment followed by the comment content.
- `/*` and `*/`: multi-line comments, which should be across multiple lines.
