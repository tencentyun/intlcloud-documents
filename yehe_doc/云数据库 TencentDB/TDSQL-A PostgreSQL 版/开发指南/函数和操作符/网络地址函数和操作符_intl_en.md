## `cidr` and `inet` Operators
The following operators are supported for `cidr` and `inet` types:

| **Operator** | **Description**         |
| ---------- | ---------------- |
| <          | Is less than             |
| <=         | Is less than or equals         |
| =          | Equals             |
| >=         | Is greater than or equals         |
| >          | Is greater than             |
| <>         | Does not equal           |
| <<         | Is contained by        |
| <<=        | Is contained by or equals |
| >>         | Contains             |
| >>=        | Contains or equals       |
| &&         | Contains or is contained by     |
| ~          | Bitwise NOT          |
| &          | Bitwise AND          |
| \|         | Bitwise OR           |
| +          | Addition               |
| -          | Subtraction               |

Sample code:
```
postgres=# SELECT inet '192.168.1.5' <= inet '192.168.1.5';
 ?column? 
----------
 t
(1 row)
 
postgres=# SELECT inet '192.168.1.5' << inet '192.168.1/24';
 ?column? 
----------
 t
(1 row)
 
postgres=# SELECT inet '192.168.1/24' && inet '192.168.1.80/28';
 ?column? 
----------
 t
(1 row)
 
postgres=# SELECT inet '192.168.1.6' + 25;
  ?column? 
--------------
 192.168.1.31
(1 row)
 
postgres=# SELECT inet '192.168.1.6' & inet '0.0.0.255';
 ?column? 
----------
 0.0.0.6
(1 row)
```

## `cidr` and `inet` Functions
| **Function**                         | **Return Type** | **Description**                         |
| -------------------------------- | ------------ | -------------------------------- |
| abbrev(inet)                   | text         | Abbreviated display format as text                 |
| abbrev(cidr)                   | text         | Abbreviated display format as text                 |
| broadcast(inet)                | inet         | Broadcast address for network                     |
| family(inet)                   | int          | Extracts the family of address; 4 for IPv4, 6 for IPv6 |
| host(inet)                     | text         | Extracts IP address as text               |
| hostmask(inet)                 | inet         | Constructs host mask for network               |
| masklen(inet)                  | int          | Extracts netmask length                 |
| netmask(inet)                  | inet         | Constructs netmask for network               |
| network(inet)                  | cidr         | Extracts the network part of address               |
| set_masklen(inet, int)       | inet         | Sets netmask length for `inet` value       |
| set_masklen(cidr, int)       | cidr         | Sets netmask length for `cidr` value       |
| text(inet)                     | text         | Extracts IP address and netmask length as text |
| inet_same_family(inet, inet) | bool         | Are the addresses from the same family?         |
| inet_merge(inet, inet)       | cidr         | The smallest network which includes both of the given networks     |

Sample code:
```
postgres=# SELECT abbrev(inet '10.1.0.0/16');
  abbrev  
-------------
 10.1.0.0/16
(1 row) 

postgres=# SELECT family('::1');
 family 
--------
   6
(1 row)
 
postgres=# SELECT hostmask('192.168.23.20/30');
 hostmask 
----------
 0.0.0.3

(1 row)
 
postgres=# SELECT set_masklen('192.168.1.5/24', 16);
 set_masklen 
----------------
 192.168.1.5/16
(1 row)
 
postgres=# SELECT netmask('192.168.1.5/24');
  netmask  
---------------
 255.255.255.0
(1 row)
```
For more network address functions and operators and their code samples, please see [Network Address Functions and Operators](http://www.postgres.cn/docs/10/functions-net.html).
