## Overview
Many users require the invisibility of an index to assess if it can be deleted. By making an index as invisible, you can test the impact of its deletion on query performance before deleting it. If the index is being used by any program or database user, an error will occur or be reported. This feature is now available to MySQL 5.7 and later versions, not just limited to MySQL 8.0.

## Supported Versions
Kernel version: MySQL 5.7 20180918 and above.

## Use Cases
Before deleting an index, you can make it invisible to see if it is still in use. If not, it can be securely deleted.

## Instructions
Run the following statements to create an invisible index or make an index invisible:
```sql
CREATE TABLE t1 (
  i INT,
  j INT,
  k INT,
  INDEX i_idx (i) INVISIBLE
) ENGINE = InnoDB;
CREATE INDEX j_idx ON t1 (j) INVISIBLE;
ALTER TABLE t1 ADD INDEX k_idx (k) INVISIBLE;
```

Run the following statements to make an index visible:
```sql
ALTER TABLE t1 ALTER INDEX i_idx INVISIBLE;
ALTER TABLE t1 ALTER INDEX i_idx VISIBLE
```
