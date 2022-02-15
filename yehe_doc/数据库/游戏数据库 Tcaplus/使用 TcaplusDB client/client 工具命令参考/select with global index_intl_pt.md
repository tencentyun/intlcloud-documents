## Consulta baseada em índice
Após a ativação da funcionalidade de índice global, o TcaplusDB permite a consulta de campos, desde que o campo na condição de consulta tenha o índice global criado.
Os campos em uma consulta agregada também exigem o índice global.
Uma consulta baseada em índice gera até 3 mil resultados.

### Instruções aceitas
#### Condições de consulta
As seguintes condições de consulta são aceitas, incluindo `=, >, >=, <, <=, !=, between, in, not in, like, not like, and, or`.

>!
>- Os dois valores de `between` estão incluídos no intervalo. Por exemplo, se você usar `between 1 and 100`, 1 e 100 estão incluídos. Em outras palavras, o intervalo de consulta deve ser [1,100].
>- A consulta `like` aceita a correspondência difusa. O curinga % corresponde a zero ou vários caracteres, já o curinga _ corresponde a um caractere.

```
tcaplus> select * from pb_generic_index_shardingkey where openid>10 and tconndid<1000;
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|openid|timekey  |tconndid|svrid  |gamesvrid  |other_property                           |items|lockid   |pay|id_uint32|id_int32|
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|201   |"timekey"|201     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|200   |"timekey"|200     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|203   |"timekey"|203     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|204   |"timekey"|204     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|202   |"timekey"|202     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
 
 
total 5 records
 
tcaplus> select * from pb_generic_index_shardingkey where openid between 1 and 300  and tconndid<1000;
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|openid|timekey  |tconndid|svrid  |gamesvrid  |other_property                           |items|lockid   |pay|id_uint32|id_int32|
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|203   |"timekey"|203     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|204   |"timekey"|204     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|201   |"timekey"|201     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|200   |"timekey"|200     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|202   |"timekey"|202     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
 
 
total 5 records
 
tcaplus> select * from pb_generic_index_shardingkey where openid>10 or tconndid<1000;
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|openid|timekey  |tconndid|svrid  |gamesvrid  |other_property                           |items|lockid   |pay|id_uint32|id_int32|
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|202   |"timekey"|202     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|203   |"timekey"|203     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|201   |"timekey"|201     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|200   |"timekey"|200     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|204   |"timekey"|204     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
 
 
total 5 records
```


#### Consulta paginada
A consulta paginada `limit offset` é aceita.

>!A consulta paginada deve usar `limit offset`. Nem `limit 1` nem `limit 0,1` podem ser usados.

```
tcaplus> select * from pb_generic_index_shardingkey where openid>10 limit 3 offset 0;
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|openid|timekey  |tconndid|svrid  |gamesvrid  |other_property                           |items|lockid   |pay|id_uint32|id_int32|
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|200   |"timekey"|200     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|201   |"timekey"|201     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|202   |"timekey"|202     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
```


#### Consulta agregada
As seguintes funções de consulta agregada são aceitas, incluindo `sum, count, max, min, avg`.
>!
>- A consulta agregada não aceita `limit offset`.
>- Atualmente, apenas a função `count` pode ser usada com `distinct`. Por exemplo, `select count(distinct(a)) from table where a > 1000`.

```
tcaplus> select sum(openid), count(*), max(openid), avg(openid) from pb_generic_index_shardingkey where openid>10 ;
1010,5,204,202
```


#### Consulta de campo especificado
Os valores dos campos especificados podem ser consultados.
>?Você também pode consultar campos aninhados na tabela do Protobuf. Por exemplo, `select field1.field2.field3, a, b from table where a > 1000`.
>
```
tcaplus> select svrid,gamesvrid from pb_generic_index_shardingkey where openid>10 or tconndid<1000;
+------+---------+--------+-------+-----------+
|openid|timekey  |tconndid|svrid  |gamesvrid  |
+------+---------+--------+-------+-----------+
|204   |"timekey"|204     |"svrid"|"gamesvrid"|
+------+---------+--------+-------+-----------+
|203   |"timekey"|203     |"svrid"|"gamesvrid"|
+------+---------+--------+-------+-----------+
|202   |"timekey"|202     |"svrid"|"gamesvrid"|
+------+---------+--------+-------+-----------+
|200   |"timekey"|200     |"svrid"|"gamesvrid"|
+------+---------+--------+-------+-----------+
|201   |"timekey"|201     |"svrid"|"gamesvrid"|
+------+---------+--------+-------+-----------+
 
 
total 5 records
```



### Instruções SQL não aceitas
#### Uso de uma consulta agregada com consulta não agregada
```
select *, a, b from table where a > 1000;

select sum(a), a, b from table where a  > 1000;

select count(*), * from table where a  > 1000;
```

#### Consulta por `order by`
```
select * from table where a > 1000 limit 100 offset 0;
```

#### Consulta por `group by`
```
select * from table where a > 1000 group by a;
```

#### Consulta por `having`
```
select sum(a) from table where  a > 1000 group by a having sum(a) > 10000;
```

#### Consulta de várias tabelas
```
select * from table1 where table1.a > 1000 and table1.a = table2.b;
```

#### Consulta de SELECT aninhada
```
select * from table where a > 1000 and b in (select b from table where b < 5000);
```

#### Consulta de AS
```
select sum(a) as sum_a from table where a > 1000;
```

#### Outras consultas não aceitas
- JOIN
- UNION
- Consultas como `select a+b from table where a > 1000`
- Consultas como `select * from table where a+b > 1000`
- Consultas como `select * from table where a >= b`
- Outras

