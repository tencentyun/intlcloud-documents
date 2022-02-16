## Kueri Berbasis Indeks
Setelah fitur indeks global diaktifkan, TcaplusDB mendukung kueri bidang, asalkan bidang dalam kondisi kueri harus memiliki indeks global yang dibuat.
Bidang dalam kueri gabungan juga memerlukan indeks global.
Kueri berbasis indeks mengembalikan hingga 3.000 hasil.

### Pernyataan yang didukung
#### Kondisi kueri
Kondisi kueri berikut didukung, termasuk `=, >, >=, <, <=, !=, between, in, not in, like, not like, and, or`.

>!
>- Dua nilai `between` disertakan dalam rentang. Misalnya, jika Anda menggunakan `between 1 and 100`, termasuk 1 dan 100. Dengan kata lain, rentang kueri harus [1,100].
>- Kueri `like` mendukung pencocokan fuzzy. Kartu bebas % cocok dengan nol atau beberapa karakter, sedangkan kartu bebas _ cocok dengan satu karakter.

```
tcaplus> pilih * dari pb_generic_index_shardingkey dengan openid>10 dan tconndid<1000;
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
 
 
total 5 catatan
 
tcaplus> pilih * dari pb_generic_index_shardingkey dengan openid antara 1 dan 300 dan tconndid<1000;
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
 
 
total 5 catatan
 
tcaplus> pilih * dari pb_generic_index_shardingkey dengan openid>10 atau tconndid<1000;
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
 
 
total 5 catatan
```


#### Kueri yang diberi halaman
Kueri yang diberi halaman `limit offset` didukung.

>!Kueri yang diberi halaman harus menggunakan `limit offset`. Baik `batas 1` maupun `batas 0,1` tidak dapat digunakan.

```
tcaplus> pilih * dari pb_generic_index_shardingkey dengan openid>10 limit 3 offset 0;
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


#### Kueri gabungan
Fungsi kueri gabungan berikut didukung, termasuk `sum, count, max, min, avg`.
>!
>- Kueri gabungan tidak mendukung `limit offset`.
>- Saat ini, hanya fungsi `count` yang dapat digunakan dengan `distinct`. Misalnya, `select count(distinct(a)) from table where a > 1000`.

```
tcaplus> pilih sum(openid), count(*), max(openid), avg(openid) dari pb_generic_index_shardingkey dengan openid>10 ;
1010,5,204,202
```


#### Kueri bidang yang ditentukan
Nilai bidang tertentu dapat dikueri.
>?Anda juga dapat membuat kueri bidang nested di tabel Protobuf. Misalnya, `select field1.field2.field3, a, b from table where a > 1000`.
>
```
tcaplus> pilih svrid,gamesvrid dari pb_generic_index_shardingkey dengan openid>10 atau tconndid<1000;
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
 
 
total 5 catatan
```



### Pernyataan SQL tidak didukung
#### Menggunakan kueri gabungan dengan kueri non-gabungan
```
pilih *, a, b dari tabel dengan a > 1000;

pilih sum(a), a, b dari tabel dengan a > 1000;

pilih count(*), * dari tabel dengan a > 1000;
```

#### Mengkueri berdasarkan `order by`
```
pilih * dari tabel dengan a > 1000 limit 100 offset 0;
```

#### Mengkueri berdasarkan `group by`
```
pilih * dari tabel dengan a > 1000 dikelompokkan berdasarkan a;
```

#### Mengkueri berdasarkan `having`
```
pilih sum(a) dari tabel dengan a > 1000 dikelompokkan berdasarkan a having sum(a) > 10000;
```

#### Kueri multi-tabel
```
pilih * dari table1 dengan table1.a > 1000 dan table1.a = table2.b;
```

#### Kueri SELECT nested
```
pilih * dari tabel dengan a > 1000 dan b di (pilih b dari tabel dengan b < 5000);
```

#### Kueri AS
```
pilih sum(a) sebagai sum_a dari tabel dengan a > 1000;
```

#### Kueri lain tidak didukung
- JOIN
- UNION
- Kueri seperti `select a+b from table where a > 1000`
- Kueri seperti `select * from table where a+b > 1000`
- Kueri seperti `select * from table where a >= b`
- Lainnya

