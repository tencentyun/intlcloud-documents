## Ikhtisar
Perintah ini digunakan untuk menghapus catatan dari tabel dengan kunci yang ditentukan. Jika parameter `-index` tidak ditentukan, semua catatan yang memenuhi kondisi akan dihapus dari tabel.

## Sintaksis
```
hapus dari tabel dengan key1 = 1 dan key2 = "abc" [dan -index = 1] [oleh partkey];
```

## Parameter

|  Parameter          | Protobuf                                      | TDR                             | Diperlukan       |
| ---------- | ------------------------------------- | -------------------------------- | ------------ |
| tabel      | Nama tabel                                        | Nama tabel                                  | Ya           |
| kunci       | Nama bidang kunci primer. Semua nilai kunci diperlukan.             | Nama bidang kunci primer. Semua nilai kunci diperlukan.               | Ya       |
| nilai     | Nama bidang kunci non-primer                  | Nama bidang kunci non-primer                                 | Ya, setidaknya satu nama bidang diperlukan. |
| \-index   | tabel LIST: Anda harus menentukan `\-index`. Hanya catatan tertentu yang akan diganti.<br>Tabel GENERIC: tidak didukung | Tabel LIST: jika `\-index` ditentukan, catatan index-th dengan kunci yang sama akan dikembalikan; jika `\-index` tidak ditentukan, semua catatan akan dikembalikan.<br>Tabel GENERIC: tidak didukung | Tidak           |
| oleh partkey | Tidak didukung         | Tabel LIST: tidak didukung <br> tabel GENERIC: hapus catatan dengan kunci parsial      | Tidak           |


## Kesalahan
Untuk informasi selengkapnya, silakan lihat [Kode Kesalahan](https://intl.cloud.tencent.com/document/product/1016/38791).

## Sampel
```
tcaplus> hapus dari table_list dengan uin=99 dan name = "99" dan key1=99 dan -index=0;
 
penghapusan berhasil
 
hapus waktu: 10263 us
 
tcaplus> hapus dari table_generic_xiahuaxian dengan _uin=99 dan nama = "danmi_test_1" dan _key3=4 oleh partkey;
 
penghapusan berhasil
 
hapus waktu: 14405 us
```
