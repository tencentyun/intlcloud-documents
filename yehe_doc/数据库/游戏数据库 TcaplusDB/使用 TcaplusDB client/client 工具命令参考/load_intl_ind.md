## Ikhtisar
Perintah ini digunakan untuk mengimpor data dalam format CSV atau XML untuk memperbarui atau menambahkan catatan.

## Sintaksis
```
## Mengimpor File XML
memuat nama file infile tabel menggunakan tdr;
 
## Mengimpor File CSV
memuat nama file infile tabel;
```

## Parameter

|  Parameter          | Protobuf                                      | TDR                             | Diperlukan       |
| --------- | -------------- | ------------------------------------------------------------ | ------ |
| tabel     | Nama tabel         | Nama tabel                                                      | Ya     |
| menggunakan tdr | Tidak didukung                 | Saat data dalam format XML diimpor, struktur file harus benar-benar mematuhi sintaksis XML. File TDR harus disediakan saat klien dimulai. | Tidak           |
| infile | Membaca data dari file.                          | Membaca data dari file.                          | Ya           |

## Kesalahan
Untuk informasi selengkapnya, lihat [Kode Kesalahan](https://intl.cloud.tencent.com/document/product/1016/38791).

## Sampel
```
tcaplus> memuat table_list infile table_list_dump.xml menggunakan tdr;
memuat 49 catatan berhasil
 
tcaplus> memuat table_list infile table_list-dump.txt;
memuat 98 catatan berhasil
```
