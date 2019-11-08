## Limits on tag keys
- A tag key starting with `qcs:` or `project` is a system reserved tag key, so these prefixes cannot be used when creating a tag key.
- Can only contain characters encoded in UTF-8, spaces, numbers, or special characters including  `+ - = ._ : / @`.
- Tag key length is 127 characters (encoded in UTF-8). 
- A tag key is case sensitive.

## Limits on tag values
- Can only contain characters encoded in UTF-8, spaces, numbers, or special characters including `+ - = ._ : / @ `.
- Tag value length is 255 characters (encoded in UTF-8).
- A tag value is case sensitive.

### Limits on the number of tags
- Resource dimension: A resource can have at most 50 different keys. 
- Tag dimension:
 - A user can have at most 1,000 different keys.
 - A key can have at most 1,000 values. 
