## Ikhtisar
Perintah ini digunakan untuk memperbarui catatan dalam tabel dengan secara eksplisit menyatakan parameter atau mengimpor file.

## Sintaksis
```
## Secara Eksplisit Mendeklarasikan Bidang untuk Memperbarui Catatan
perbarui peraturan tabel value1 = 1, value2 = "abc", value3 = 0x123456 dengan key1 = 1 dan key2 = "abc" dan [-index = 1];
 
## Mengimpor File CSV untuk Mengganti Catatan
perbarui nama file infile tabel [dengan -index = 0];
 
## Mengimpor File XML untuk Mengganti Catatan
perbarui nama file tabel infile [dengan -index = 0] menggunakan tdr;
```

## Parameter

|  Parameter          | ProtoBuf                                      | TDR                             | Diperlukan       |
| --------- | ------------------------------------- | ------------------------------------------- | ------------ |
| tabel     | Nama tabel                                   | Nama tabel                                  | Ya           |
| kunci       | Nama bidang kunci primer. Semua nilai kunci diperlukan.             | Nama bidang kunci utama. Semua nilai kunci diperlukan.               | Ya       |
| nilai     | Nama bidang kunci non-primer                  | Nama bidang kunci non-primer                                 | Setidaknya satu atau \* |
| \-index   | tabel LIST: Anda harus menentukan `\-index`. Hanya catatan tertentu yang akan diganti.<br>Tabel GENERIC: tidak didukung | Tabel LIST: jika `\-index` ditentukan, catatan index-th dengan kunci yang sama akan dikembalikan; jika `\-index` tidak ditentukan, semua catatan akan dikembalikan.<br>Tabel GENERIC: tidak didukung | Tidak           |
| menggunakan tdr | Tidak didukung                 | Ketika data dikeluarkan dalam format XML, struktur file harus benar-benar mematuhi sintaksis XML. File TDR harus disediakan saat klien diluncurkan. | Tidak           |
| infile | Membaca data dari file.                          | Membaca data dari file.                          | Tidak           |


## Kesalahan
Silakan lihat [Kode Kesalahan](https://intl.cloud.tencent.com/document/product/1016/38791).

## Sampel
```
tcaplus> perbarui table_list set level=99 dan count= 88 dengan uin=99 dan name = "99" dan key1=99 dan -index=0;
 
pembaruan berhasil
 
waktu pembaruan: 117086 us
```
