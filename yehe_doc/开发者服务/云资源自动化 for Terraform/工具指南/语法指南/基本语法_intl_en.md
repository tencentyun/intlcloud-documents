### Basic Type

A primitive type is simple type that is not made from any other types. All primitive types in Terraform are represented by a type keyword. Available primitive types include:
- `string`: A sequence of Unicode characters representing some text (such as "hello").

- `number`: A numeric value, which can be an integer or a decimal.

- `bool`: A Boolean value, which can be `true` or `false`.


   Sample:

   ``` bash
   id = 123
   vpc_id = "123"
   status = true
   ```

### Complex Type

A complex type is a type that groups multiple values into a single value.

#### Collection type

A collection contains a set of values of the same type:
- `list(...)`: A sequence of values identified by consecutive integers starting with 0.

- `map(...)`: A set of values, each of which is identified by a string label.

- `set(...)`: A set of unique values.


#### Structural type
- `object(...)`: A custom type that contains its own named attributes.

- `tuple(...)`: A sequence of elements identified by consecutive integers starting with 0, where each element has its own type.


#### Special type
- `null`: An argument set to null is considered omitted. Terraform will automatically ignore the argument and use the default value.

- `any`: It is a very special type constraint in Terraform. It is not a type but simply a placeholder. Whenever a value is given a complex type constrained by `any`, Terraform will try to calculate the most accurate type to replace `any`.


### Argument

Argument assignment means assigning a value to a specific argument name. The name can contain letters, numbers, underscores, and hyphens and cannot begin with a number, such as:
``` html
id = "123"
```

### Block

A block is a container for a set of arguments, such as:
``` bash
resource "tencentcloud_instance" "foo" {
    tags                                    = {}
    vpc_id                                  = "vpc-5bt2ix8p"
}
```

### Comment

Terraform supports the following three types of comments:
- `#`: A single-line comment followed by the comment content.

- `//`: A single-line comment followed by the comment content.

- `/*` and `*/`: Multi-line comments that might be span over multiple lines.
