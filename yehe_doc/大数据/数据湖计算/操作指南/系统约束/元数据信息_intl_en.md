The following lists the limits on the numbers of databases, data tables, attribute columns, and partitions.

| Item | Maximum Number        |
| -------------------- | ---------- |
| Databases per account	| 1,000| 
| Data tables per account	| 10,000| 
| Tables per database | 	4,096| 
| Columns per data table	| 4,096| 
| Partitions per table	| 10,000| 
| Partitions per root account	| 1,000,000| 
| Fields per table | 	4,096| 
| Custom functions per account	| 100| 
| Catalogs that can be created | 	20| 

### Database
- Name: It can contain up to 127 characters and must be unique in a data link.
- Description: It can contain up to 2,048 characters.
- Data address of an external table (COS address): It can contain up to 888 characters (COS path length limit).
- Parameter: It is in the `Map<string:string>` format and can contain up to 127 characters. All parameters can contain up to 3,000 characters in total.

### Data table/View
- Name: It can contain up to 127 characters and must be unique in a database.
- Description: It can contain up to 1,000 characters.
- Data address of an external table (COS address): It can contain up to 888 characters (COS path length limit).
- Parameter: It is in the `Map<string:string>` format and can contain up to 127 characters. All parameters can contain up to 512,000 characters in total.

### Attribute column
- Name: It can contain up to 127 characters and must be unique in a data table.
- Description: It can contain up to 256 characters.
- Field value: It can contain up to 131,072 characters. Longer values cannot be created.

### Partition
- Partition field name: It can contain up to 127 characters.



