
The Terraform language has customary style conventions, and we recommend you always follow them to ensure file and module consistency between different teams. In addition, automatic formatting tools also need to conform to such conventions, and you can use `terraform fmt` for formatting.

## Code Constraint
- Indent two spaces for each nesting level.
- When multiple arguments with single-line values appear on consecutive lines at the same nesting level, align their equals signs:
```
  ami           = "abc123"
  instance_type = "t2.micro"
```
- When both arguments and blocks appear together inside a block body, place all of the arguments together at the top and then place nested blocks below them. Use one blank line to separate the arguments from the blocks.
- Use blank lines to separate logical groups of arguments within a block.
- For blocks that contain both arguments and "meta-arguments" (as defined by the Terraform language semantics), list meta-arguments first and separate them from other arguments with one blank line. Place meta-argument blocks last and separate them from other blocks with one blank line.
```
resource "tencentclould_instance" "example" {
  count = 2 # meta-argument first

  ami           = "abc123"
  instance_type = "t2.micro"

  network_interface {
    # ...
  }

  lifecycle { # meta-argument block last
    create_before_destroy = true
  }
}

```
- Top-Level blocks should always be separated from one another by one blank line. Nested blocks should also be separated by blank lines, except when grouping together related blocks of the same type (like multiple `provisioner` blocks in a resource).
- Avoid separating multiple blocks of the same type with other blocks of a different type, unless the block types are defined by semantics to form a family.
