## Ikhtisar
Perintah ini digunakan untuk menanyakan seluruh catatan atau beberapa bidang yang disertakan dalam catatan. Jika tidak ada catatan yang cocok, kesalahan akan ditampilkan.

## Sintaksis
```
pilih key1, key2, key3, value1, value2 [into result.csv] dari tabel dengan key1 = 1 dan key2 = "abc" [dan -index = 1] [\P] [\G] [menggunakan tdr]
pilih * [into result.xml] dari tabel dengan key1 = 1 dan key2 = "abc" [dan -index = 1] menggunakan tdr [\P];
```

## Parameter

|  Parameter          | Protobuf                                      | TDR                             | Diperlukan       |
| --------- | ---------------------------------------- | -------------------------------------------- | ------------ |
| tabel     | Nama tabel                                                  | Nama tabel                             | Ya           |
| kunci       | Nama bidang kunci primer. Kueri indeks global didukung. Anda dapat memasukkan beberapa nilai kunci.      | Nama bidang kunci primer. Semua nilai kunci diperlukan.        | Ya     |
| nilai     | Nama bidang kunci non-primer                  | Nama bidang kunci non-primer                                 | Ya, setidaknya satu |
| \-index   | Tabel LIST: jika `\-index` ditentukan, catatan indeks di bawah kunci yang sama akan dikembalikan; jika `\-index` tidak ditentukan, semua catatan akan ditampilkan.<br>Tabel GENERIC: tidak didukung | Tabel LIST: jika `\-index` ditentukan, catatan indeks di bawah kunci yang sama akan dikembalikan; jika `\-index` tidak ditentukan, semua catatan akan ditampilkan.<br>Tabel GENERIC: tidak didukung | Tidak           |
| \\P       | Latensi Pencetakan                              | Latensi Pencetakan                           | Tidak           |
| \\G       | Pencetakan vertikal                                   | Pencetakan vertikal                                    | Tidak           |
| menggunakan tdr | Tidak didukung                 | Ketika data dikeluarkan dalam format XML, struktur file harus benar-benar mematuhi sintaksis XML. File TDR harus disediakan saat klien dimulai. | Tidak           |
| Ke dalam      | Mengeluarkan data ke file                           | Mengeluarkan data ke file                           | Tidak           |


## Kesalahan
Untuk informasi selengkapnya, lihat [Kode Kesalahan](https://intl.cloud.tencent.com/document/product/1016/38791).

## Sampel

```
tcaplus> pilih * dari test_table dengan gameid=1234 dan itemid=12323 dan name='testname';
+------+------+----------+------+----+-----+
|gameid|itemid|name      |typeid|Data|uname|
+------+------+----------+------+----+-----+
|1234  |12323 |"testname"|0     |9   |"ab" |
+------+------+----------+------+----+-----+
1 catatan dipilih, pilih waktu: 9802 us
 
tcaplus> pilih uname dari test_table dengan gameid=1234 dan itemid=12323 dan name='testname';
+------+------+----------+-----+
|gameid|itemid|name      |uname|
+------+------+----------+-----+
|1234  |12323 |"testname"|"ab" |
+------+------+----------+-----+
1 catatan dipilih, pilih waktu: 9457 us
 
tcaplus> pilih * ke dalam test.txt dari test_table dengan gameid=1234 dan itemid=12323 dan name='testname';
1 catatan disimpan ke test.csv, pilih waktu: 10198 us
 
tcaplus> pilih * dari test_table dengan gameid=1234 dan itemid=12323 dan name='testname' \P \G;
gameid: 1234
itemid: 12323
name: "testname"
typeid: 0:
Data: 9
uname: "ab"
 
API ----      -1us    --->ProxyFront----      10us    --->ProxyEnd---     364us    --->SvrMainStart
|                              |                             |                           |381us
|11380us                       |4138us                       |4104us                   SvrWorkerStart
|                              |                             |                           |61us
API <---   34197us    ----ProxyFront<---      24us    ----ProxyEnd<--    3298us    ----SvrWorkerEnd
1 catatan dipilih, pilih waktu: 11380 us
 
 
tcaplus> pilih * ke table_list.xml dari table_list dengan uin=99 dan name = "99" dan key1=99 menggunakan tdr;
11 catatan disimpan ke table_list.xml, pilih waktu: 135299 us
 
tcaplus> pilih c_string dari table_list dengan uin=99 dan name = "99" dan key1=99;
+---+----+----+--------+
|uin|name|key1|c_string|
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |""      |
+---+----+----+--------+
|99 |"99"|99  |""      |
+---+----+----+--------+
|99 |"99"|99  |""      |
+---+----+----+--------+
|99 |"99"|99  |""      |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
11 catatan dipilih, pilih waktu: 102572 us
 
tcaplus> pilih c_string dari table_list dengan uin=99 dan name = "99" dan key1=99 dan -index=9;
+---+----+----+--------+
|uin|name|key1|c_string|
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
1 catatan dipilih, pilih waktu: 9886 us
```

