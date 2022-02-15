## Ikhtisar
Perintah ini digunakan untuk mengekspor semua data dari tabel ke konsol atau ke file.

## Sintaksis
```
## Mengekspor Bidang Parsial
dump key1, key2, value1, value2 [into result.csv] dari tabel limit 10;
 
## Mengekspor sebagai File XML
dump * [ke dalam nama file] dari tabel limit 10 menggunakan tdr;
 
## Mengekspor sebagai File CSV
dump * [ke dalam nama file] dari tabel limit 10;
```

## Parameter

|  Parameter          | Protobuf                                      | TDR                             | Diperlukan       |
| ----- | --------------------------------------------------- | ------------------------------------------------------- | ------ |
| tabel | Nama tabel                                                   | Nama tabel                                                   | Ya     |
| kunci   | Nama bidang kunci primer. Semua nilai kunci diperlukan.                                | Nama bidang kunci primer. Semua nilai kunci diperlukan.         | Ya     |
| nilai | Nama bidang kunci non-primer                                                 | Nama bidang kunci non-primer                                                 | Tidak     |
| limit | Tabel LIST: jumlah kunci yang diekspor. Satu kunci untuk beberapa catatan.<br>Tabel GENERIC: jumlah catatan yang diekspor. Satu kunci untuk satu catatan. | Tabel LIST: jumlah kunci yang diekspor. Satu kunci untuk beberapa catatan.<br>Tabel GENERIC: jumlah catatan yang diekspor. Satu kunci untuk satu catatan. | Tidak     |
| menggunakan | Tidak didukung                                                       | Ketika data dikeluarkan dalam format XML, struktur file harus benar-benar mematuhi sintaksis XML. File TDR harus disediakan saat klien diluncurkan.  | Tidak     |
| ke dalam | Ekspor sebagai file.                                               | Ekspor sebagai file.                                               | Tidak     |


## Kesalahan
Untuk informasi selengkapnya, silakan lihat [Kode Kesalahan](https://intl.cloud.tencent.com/document/product/1016/38791).

## Sampel

```
tcaplus> dump * dari table_list limit 0;
uin,name,key1,level,count,array_count,items,c_int8,c_uint8,c_int16,c_uint16,c_int32,c_uint32,c_int64,c_uint64,c_float,c_double,c_string,c_string_128K,c_string_256K,c_binary,binary,selector,single_struct,simple_struct,single_union_selector,single_union,array,c_union,union_array,c_struct,struct_array
99,"99",99,1,0,1,0x,-1,2,-3,4,-5,6,-7,0,1.234568,9.876543,"","123456789","123456789",0x,0,0,0x,0x,0,0x,0x,0x,0x,0x,0x
99,"99",99,1,0,1,0x,-1,2,-3,4,-5,6,-7,0,1.234568,9.876543,"","123456789","123456789",0x,0,0,0x,0x,0,0x,0x,0x,0x,0x,0x
99,"99",99,1,0,1,0x,-1,2,-3,4,-5,6,-7,0,1.234568,9.876543,"","123456789","123456789",0x,0,0,0x,0x,0,0x,0x,0x,0x,0x,0x
99,"99",99,1,0,1,0x,-1,2,-3,4,-5,6,-7,0,1.234568,9.876543,"","123456789","123456789",0x,0,0,0x,0x,0,0x,0x,0x,0x,0x,0x
 
membuang 4 catatan berhasil
 
waktu pembuangan: 121671 us
 
tcaplus> dump * ke dalam table_list.txt dari table_list limit 0;
 
membuang 4 catatan berhasil
 
tcaplus> dump * ke dalam table_list.xml dari table_list limit 0 menggunakan tdr;
 
membuang 4 catatan berhasil
```
