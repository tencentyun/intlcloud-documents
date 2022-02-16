Dokumen ini menjelaskan cara menggunakan alat klien `tcaplus_client` untuk mengakses data TcaplusDB.
Semua pernyataan operasi data harus membawa ketentuan `WHERE` yang harus berisi setidaknya bidang kunci utama. Jika ada beberapa kunci utama, pisahkan dengan `and`.

## Alat Klien
`tcaplus_client` adalah alat klien yang digunakan untuk mengakses tabel TcaplusDB dan dapat diperoleh di alamat unduhan pada tabel di bawah.

Paket rilis TcaplusServiceAPI untuk Linux x86_64 berisi alat `tcaplus_client` untuk Linux 64-bit.

| Versi | OS | Nama Paket Unduhan |
| ------------- | -------- | ------------------------------------------------------------ |
| 3.36.0.192960 | Linux    | [TcaplusPbApi3.36.0.192960.x86_64](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/TcaplusPbApi3.36.0.192960.x86_64_release_20200115.tar.gz) |

>?Operasi yang relevan harus dilakukan pada instans CVM di VPC dan subnet yang sama di bawah akun Tencent Cloud Anda sebagai instans TcaplusDB Anda.

### Menginstal klien
Setelah mengunduh paket penginstalan TcaplusServiceAPI, Anda dapat [menggunakan alat unggah](https://intl.cloud.tencent.com/document/product/213/34821) untuk mengunggahnya ke instans CVM di VPC dan subnet yang sama dengan kluster TcaplusDB.

1. Selepas mengunggah, Jalankan perintah berikut untuk mendekompresi paket penginstalan:
```
tar -xf TcaplusServiceApi3.32.0.191008.x86_64_release_20190409.tar.gz -C tcaplus
```
2. Setelah dekompresi, masukkan direktori `bin` di `tcaplus` dan berikan izin yang dapat dieksekusi alat ini:
```
cd tcaplus/release/x86_64/bin
chmod +x tcaplus_client
```
3. Jalankan perintah `./tcaplus_client`, dan sistem akan meminta Anda memasukkan informasi parameter yang diperlukan untuk koneksi database. Anda dapat memasukkannya berdasarkan informasi kluster Anda.
>!Dalam contoh di bawah, `app_id` menunjukkan ID akses kluster, `App` menunjukkan kluster, dan `zone` menunjukkan grup tabel.


```
# ./tcaplus_client
--------------------------------------------------------------------------------
 parameter tidak valid, harap mulai klien sebagai berikut:
    ./tcaplus_client -a app_id -z zone_id -s signature -d dir_server_url [-t table_name] [-l log_file.xml] [-T tdr_file.tdr] [-e execute_command]
    parameter di [] opsional, dan urutannya tidak penting.
    -a(--ap_id) ID Aplikasi
    -z(--zone_id)    ID ZONA
	-s(--signature)    KATA SANDI
    -d(--dir)    dir server addr
    -t(--table)    tabel untuk ditambahkan
    -l(--log)   nama file log yang harus berupa client_log.xml, dan nama kelas log menjadi klien
    -T(--tdr)    nama file tdr 
    -e(--execute) konten berikut harus dengan qoute.
    e.g. ./tcaplus_client -a 2 -z 3 -s "test@Password1" -d 172.xx.xx.181:9999 -T table_test.tdr 
--------------------------------------------------------------------------------
```

### Menghubungkan ke TcaplusDB
Jalankan perintah yang sesuai untuk terhubung ke TcaplusDB. Informasi titik akses dalam contoh di bawah ini adalah sebagai berikut, dan tabel `tb_online` telah dibuat di grup tabel yang ID-nya 1:
- ID akses kluster: 2
- Kata sandi koneksi: test@Password1
- Alamat pribadi: port pribadi: 10.125.32.21:9999
- ID grup tabel: 1

```
./tcaplus_client -a 2 -z 1 -s "test@Password1" -d 10.125.32.21:9999
+------------------------------------------------------------------------------+
|    tcaplus_client x86_64  dibangun pada Rabu 18 Jan 22:08:38 CST 2017              |
|                                                                              |
|    Selamat datang!                                                                  |
+------------------------------------------------------------------------------+

tcaplus>
```

Masukkan `help` setelah prompt, dan informasi bantuan akan ditampilkan. Anda dapat menjalankan `> help specific command` untuk melihat detail penggunaan perintah tertentu.
```
tcaplus>help
--------------------------------------------------------------------------------
    show                 mendapatkan informasi terkait status server. menjalankan help menampilkan detail.
    dir                  menambah dir server url. jika tidak ada dir_server_url yang ditambahkan ,
                         perintah akan gagal saat dijalankan.
    desc                menampilkan deskripsi struction tabel saat ini
    count                menampilkan jumlah baris tabel
    select               data kueri
    update               memperbarui catatan. jika catatan tidak ada, tambahkan atau perbarui jika ada.
    insert               memasukkan catatan baru (tidak diterapkan)
    delete               menghapus catatan
    bson                 menjalankan kueri bson
    dump                 catatan dump dari tcaplus ke file dengan format csv
    load                memuat catatan beban dari file csv dan mengimpor catatan ke tcplus
    clean                menghapus tabel
    quit                 keluar dari klien
    help                 mengikuti perintah untuk mendapatkan detail.
                         misalnya help show, help dir dll.
    catatan: mode tdr berarti memulai klien dengan -T, dan tidak ada mode tdr yang memulai klien tanpa -T
--------------------------------------------------------------------------------
```


## Metode Eksekusi Pernyataan
<br>Metode eksekusi dan fitur dari pernyataan di atas adalah sebagai berikut.

#### Melakukan operasi desc
Perintah ini digunakan untuk melihat informasi definisi tabel. Untuk bidang nested, Anda hanya dapat melihat bahwa atributnya adalah jenis nested, tetapi Anda tidak dapat melihat definisi struktur nested.
Sintaksis: `desc table name;`
```
tcaplus>desc game_players;
TableName:game_players
TableType:PROTOBUF
-------------------------------------------------------------------------
| Bidang                         Jenis                          Kunci       |
-------------------------------------------------------------------------
| player_id                     int64                         key       |
| player_email                  string                        key       |
| player_name                   string                                  |
| game_server_id                int32                                   |
| login_timestamp               string                                  |
| logout_timestamp              string                                  |
| is_online                     int8                                    |
| pay                           message                                 |
-------------------------------------------------------------------------
```

#### Melakukan operasi hitung
Perintah ini digunakan untuk melihat jumlah total catatan tabel.
Sintaksis: `count table name;`
```
tcaplus>count t1;
-------------------------------------------
| TableName                     COUNT(*)  |
-------------------------------------------
| t1                            15        |
-------------------------------------------
```

#### Mengekspor data
Anda dapat menjalankan perintah `dump` untuk mengekspor semua catatan dari tabel tertentu ke dalam file .json.
Sintaksis: `dump * dari nama tabel menjadi filename;`
```
tcaplus>dump * dari player menjadi player.txt;
--------------------------------------------------------------------------------
      dump dari table("player") success. catatan total adalah 4
--------------------------------------------------------------------------------
```

#### Mengimpor data
Anda dapat menjalankan perintah `load` untuk mengimpor catatan tabel tertentu dari file .csv. File yang diekspor dengan perintah `dump` tidak dapat diimpor secara langsung.
Sintaksis: `load table name from file;`
```
tcaplus>load hehe from test1;
--------------------------------------------------------------------------------
      1 catatan berhasil dimuat.
--------------------------------------------------------------------------------
```

#### Menghapus data tabel
Demi keamanan, alat klien saat ini tidak memungkinkan Anda untuk menghapus data tabel secara langsung. Jika ingin menghapus data seluruh tabel, silakan gunakan fitur [table clearing](https://console.cloud.tencent.com/tcaplusdb/table) di konsol.


### Memasukkan data
Saat ini, pernyataan `INSERT` tidak dapat digunakan; sebagai gantinya, Anda dapat menjalankan pernyataan `UPDATE` untuk menyisipkan catatan.

### Memodifikasi data
Anda dapat menjalankan pernyataan `UPDATE` untuk menulis catatan. Jika tidak ada catatan yang cocok dengan nilai bidang kunci utama dalam ketentuan `WHERE`, catatan akan ditambahkan sebagai yang baru.
Sintaksis: `update table set field=value[,field 2=value 2…] where primary key field=value [and primary key field 2=value 2…];`
```
tcaplus>update tb_online set gamesvrid=4099, logintime=101 where uin=1024 and name="tcaplus_user" and region=10;
--------------------------------------------------------------------------------
        success. 
--------------------------------------------------------------------------------
waktu pembaruan: 5593 us
```

### Membaca data
Anda dapat menjalankan pernyataan `SELECT` untuk membaca data bidang yang ditentukan.
Sintaksis: `select field[,field 2…] from table where primary key field=value [and primary key field 2=value];`
Kolom `recDataVersion` dalam data input menunjukkan nomor versi dari catatan saat ini.
```
tcaplus>select gamesvrid, logintime from tb_online where uin=1024 and name="tcaplus_user" and region=10;
+------+--------------+--------+------------------+--------------+-----------+
| uin  | nama         | wilayah | recDataVersion   | gamesvrid    | waktu login |
+------+--------------+--------+------------------+--------------+-----------+
| 1024 | tcaplus_user | 10     | 2                | 4099         | 101       |
+------+--------------+--------+------------------+--------------+-----------+
total 1 catatan merespons.
waktu kueri 8686 us
```

Sintaksis`select * from table where primary key field=value` didukung. Di bawah ini adalah contoh:
```
tcaplus>select * dari pengujian di mana id=1 dan nama=1;
+----+------+------------------+----+
| id | nama | recDataVersion   | em |
+----+------+------------------+----+
| 1  | 1    | 1                | 1  |
+----+------+------------------+----+
total 1 catatan merespons.
waktu kueri 7537 us
```

Mode output berformat `\G` dan `\P` didukung. `\G` menunjukkan output horizontal menurut bidang, sedangkan `\P` menunjukkan bahwa data akan dikeluarkan sebagai tabel. Bidang yang tidak dikonfigurasi dengan output yang diformat akan dikeluarkan dalam mode `\P` secara default.
```
tcaplus>select * dari hehe di mana id=1 dan nama=1 \G;
----------------------------------------1.row----------------------------------------
id: 1
name: 1
recDataVersion: 1
em: 1
total respons catatan: 1
waktu kueri 3285 us
```

Anda dapat menjalankan pernyataan `SELECT` untuk mengekspor data ke dalam file.
Sintaksis: `select * into [outfile] filename from table name where primary key=value [and primary key 2=value];`

```
tcaplus>select * ke outfile test2.xml dari hehe di mana id=1 dan name=1;
+----+------+------------------+----+
| id | nama | recDataVersion   | em |
+----+------+------------------+----+
| 1  | 1    | 1                | 1  |
+----+------+------------------+----+
total 1 catatan merespons.
waktu kueri 5399 us
```

### Menghapus data
Anda dapat menjalankan pernyataan `DELETE` untuk menghapus catatan tertulis.
Sintaksis: `delete from table name where primary key=value [and primary key 2=value];`
```
tcaplus>delete dari hehe di mana id=4 dan nama=4;
--------------------------------------------------------------------------------
        success
--------------------------------------------------------------------------------
waktu hapus 4280 us
```
