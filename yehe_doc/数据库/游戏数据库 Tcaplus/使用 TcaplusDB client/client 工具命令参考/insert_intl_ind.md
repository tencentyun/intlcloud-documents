## Ikhtisar
Perintah ini digunakan untuk menyisipkan entri data ke dalam tabel dengan mendeklarasikan parameter secara eksplisit atau mengimpor file.

## Sintaksis
```
## Secara Eksplisit Mendeklarasikan Parameter untuk Memasukkan Data
masukkan ke dalam tabel (key1, key2, value1, vlaue2) nilai (1, "abc", 2, "def") [after -1] [shift none/head/tail];

## Mengimpor File CSV untuk Menyisipkan Data
masukkan ke dalam tabel infile result.csv [after -1] [shift none/head/tail];

## Mengimpor File XML untuk Memasukkan Data Asalkan File TDR Disediakan di Startup Klien
masukkan ke dalam tabel infile result.xml [after -1] [shift none/head/tail] menggunakan tdr;
```

## Parameter

|  Parameter          | Protobuf sebuah TDR                                    | Diperlukan       |
| --------- | ------------------------------------------------------------ | ------------ |
| tabel     | Nama tabel                                                  | Ya           |
| kunci       | Nama bidang kunci primer                                                   | Ya           |
| nilai | Nama bidang kunci non-primer                                                 | Ya, setidaknya satu |
| setelah     | Tabel LIST: <br> n>0 menunjukkan bahwa data akan dimasukkan setelah data n pertama<br>n=-2 menunjukkan bahwa data akan dimasukkan di bagian awal antrean<br>n=-1 menunjukkan bahwa data akan dimasukkan di bagian belakang antrean<br>n<-2: tidak didukung <br>tabel GENERIC: bidang ini tidak didukung. | Tidak          |
| pengalihan     | Jika ukuran tabel melebihi nilai maksimum, Anda dapat menentukan cara menghapus data secara otomatis. Nilai yang valid: <br>`none`: tidak ada data yang akan dihapus<br>`head`: data di bagian awal antrean akan dihapus<br>bagian akhir: data di bagian akhir antrean akan dihapus. | Tidak |
| menggunakan tdr | Tabel Protobuf tidak mendukung parameter ini. Untuk memasukkan data ke dalam tabel TDR, impor file XML yang strukturnya harus benar-benar mematuhi sintaksis XML. Selain itu, file TDR harus disediakan saat klien dimulai. | Tidak           |
| infile    | Baca data dari file                                             | Tidak           |


## Kesalahan
Untuk informasi selengkapnya, lihat [Kode Kesalahan](https://intl.cloud.tencent.com/document/product/1016/38791).

## Sampel
Unduh file sampel [result.xml](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/result.xml) dan [result.csv](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/result.csv).

```
tcaplus>masukkan ke dalam game_players (player_id,player_name,player_email,game_server_id) nilai (2,name,email,2);
masukkan berhasil
 
masukkan waktu: 45322 us
 
tcaplus> Masukkan ke dalam table_list (uin, name, key1) nilai (99,99,99) setelah -1 shift tail;
 
masukkan berhasil
 
masukkan waktu: 22464 us
 
tcaplus> Masukkan ke dalam table_list infile result.xml menggunakan tdr;
 
 
masukkan berhasil
 
masukkan waktu: 9493 us
 
tcaplus> Masukkan ke dalam table_list infile result.csv;
 
 
masukkan berhasil
 
masukkan waktu: 22368 us
```

