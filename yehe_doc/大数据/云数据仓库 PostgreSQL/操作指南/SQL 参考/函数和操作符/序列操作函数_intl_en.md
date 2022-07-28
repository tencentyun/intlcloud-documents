The database supports sequences. Sequence objects are special single-row tables created with `CREATE SEQUENCE`. A sequence is generally used to generate unique table data. For example, to create a sequence, run `CREATE SEQUENCE myseq START 101;`. Sequence functions are as listed below:

| Function | Return Type | Description | Result |
| ------------------- | ------ | ------------------------ | ---- |
| nextval('myseq')    | bigint | Advances sequence and returns new value | 101  |
| setval('myseq',102) | bigint | Sets sequence's current value         | 102  |
