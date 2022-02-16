TencentDB for TcaplusDB mendukung dua bahasa definisi tabel:  Protocol Buffer (Protobuf) dan Tencent Data Representation (TDR). Protobuf adalah metode serialisasi data terstruktur yang dikembangkan oleh Google yang menekankan kemudahan dan kinerja. TDR adalah bahasa deskripsi data netral platform yang dikembangkan oleh Tencent yang menggabungkan keunggulan XML, bahasa biner, dan pemetaan relasional objek (ORM) dan banyak digunakan dalam skenario serialisasi data game Tencent. Kedua bahasa tersebut sama-sama sangat berguna. Gunakan salah satunya berdasarkan kebiasaan penggunaan Anda. Dokumen ini menjelaskan cara mendefinisikan tabel di Protobuf.

## Definisi Tabel di Protobuf
Untuk membuat tabel di TcaplusDB, Anda harus terlebih dahulu menggunakan bahasa deskripsi tabel untuk menentukan format tabel dan menulis konten definisi tabel ke dalam file deskripsi IDL tabel.
File deskripsi tabel IDL mendefinisikan tabel berdasarkan aturan Protocol Buffers.
Informasi definisi utamanya dibagi menjadi tiga jenis:
- Informasi definisi file
- Informasi definisi tabel
- Informasi jenis nested

## Definisi File
Area informasi definisi file utamanya mendefinisikan informasi umum dari file deskripsi tabel saat ini yang berisi tiga jenis konten berikut:

| Nama Opsi | Deskripsi | Nilai Sampel | Diperlukan |
| --- | --- | --- | --- |
| sintaksis | Ini menentukan versi spesifikasi sintaksis untuk menulis file saat ini. | proto2, proto3 | Ya |
| paket | Ini menentukan nama paket khusus dari file saat ini yang membantu menghindari konflik nama dengan pesan. | Informasi nama paket | Ya |
| importIt | Ini menunjukkan beberapa informasi umum yang diimpor ke tabel TcaplusDB yang harus diimpor dalam definisi tabel. | tcaplusservice.optionv1.proto | Ya |


## Definisi Tabel

Dalam informasi definisi tabel, format tabel (termasuk informasi tambahan dan informasi bidang) ditentukan dalam pesan.
#### Definisi informasi yang diperluas
Informasi definisi tabel dapat diperluas dengan `option` berdasarkan sintaksis Protobuf yang dapat mengimplementasikan fitur semantik yang lebih kaya. Konten yang dapat ditentukan adalah sebagai berikut:
Format definisi terperinci adalah `option(tcaplusservice.option) = "value";`.

| Nama Opsi | Deskripsi | Contoh Konfigurasi | Diperlukan |
| --- | --- | --- | --- |
| tcaplus_primary_key | Menetapkan bidang kunci utama tabel TcaplusDB. | option(tcaplusservice.tcaplus_primary_key) = "uin,name,region"; | Ya |
| tcaplus_index | Mengatur bidang kunci indeks tabel TcaplusDB. | option(tcaplusservice.tcaplus_index) = "index_1(uin,region)"; | No |
| tcaplus_sharding_key | Anda dapat menyesuaikan shardkey tabel. | option(tcaplusservice.tcaplus_sharding_key) = "uin"; | No |
| tcaplus_field_cipher_suite | Diperlukan jika fitur enkripsi bidang digunakan. Untuk menentukan algoritme enkripsi khusus Anda, lihat contoh di dokumentasi API. | option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; | No |
| tcaplus_cipher_md5 | MD5 (digunakan untuk mengenkripsi string kata sandi yang disimpan di pihak pengguna) harus diatur jika fitur enkripsi bidang digunakan. | option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; | No |

#### Definisi informasi bidang

Format definisi bidang TcaplusDB adalah `field modifier field type field name = identifier[special definition];`.
##### Modifier bidang
proto2 mendukung tiga modifier pembatas, sementara proto3 tidak lagi mendukung modifier `REQUIRED` dan menggunakan `OPTIONAL` sebagai modifier default.
- REQUIRED (DIPERLUKAN): ini menunjukkan bahwa bidang ini wajib diisi. Di proto2, bidang kunci utama harus dinyatakan dengan `REQUIRED`.
- OPTIONAL (OPSIONAL): ini menunjukkan bahwa bidang ini opsional. Anda dapat menetapkan nilai default untuk bidang opsional.
- REPEATED (BERLULANG): ini menunjukkan bahwa bidang ini dapat berisi elemen 0–N. Fiturnya sama dengan fitur `OPTIONAL`, tetapi dapat berisi beberapa nilai sekaligus yang dapat dianggap sebagai array. Definisi khusus `[packed = true]` harus ditentukan.

##### Jenis bidang
TcaplusDB mendukung bidang umum dan bidang nested. Untuk informasi selengkapnya, lihat [Jenis Data](https://intl.cloud.tencent.com/document/product/1016/38659).
##### Nama bidang
Anda dapat memberi nama bidang berdasarkan atributnya saat ini. Nama dapat berisi huruf, angka, dan garis bawah dan tidak boleh dimulai dengan angka. Anda sebaiknya menggunakan camelCase untuk namanya.
##### Pengidentifikasi
Rentang nilai pengidentifikasi: [1, 2^29 - 1]
Pengidentifikasi dalam [19000, 19999] tidak dapat digunakan karena dicadangkan di Protocol Buffer. Jika Anda menggunakan salah satu dari mereka, kesalahan akan dilaporkan.
Setiap bidang akan menempati memori saat dikodekan, dan ukuran memori yang ditempati sesuai dengan pengidentifikasi:
- Bidang dengan pengidentifikasi dalam [1, 15] menempati 1 byte selama pengkodean.
- Bidang dengan pengidentifikasi dalam [16, 2047] menempati 2 byte selama pengkodean.
##### Definisi khusus
- Anda dapat menggunakan `packed=true` untuk menentukan bidang yang dinyatakan dengan modifier `REPEATED`. Sintaksis kebijakannya sebagai berikut:
```
repeated int64 lockid = 6 [packed = true]; 
```
- Anda dapat menggunakan `default = 1` untuk menentukan nilai default untuk bidang yang dinyatakan dengan modifier `OPTIONAL`. Sintaksis kebijakannya sebagai berikut:
```
optional int32 logintime = 5 [default = 1];
```
- Anda dapat menentukan bidang dalam jenis string dan byte sebagai bidang terenkripsi. Sintaksis kebijakannya sebagai berikut:
```
required string name = 2[(tcaplusservice.tcaplus_crypto) = true];
```

#### Informasi jenis nested
TcaplusDB mendukung jenis nested. Jenis nested dapat berisi yang lain sebagai bidangnya. Anda juga dapat menentukan jenis nested baru di yang lain.
Mirip dengan definisi tabel, definisi jenis nested juga dinyatakan dengan pesan, tetapi struktur jenis nested tidak dapat berisi definisi informasi tambahan seperti "kunci utama" dan "indeks".
TcaplusDB mendukung hingga 128 tingkat nesting berturut-turut; namun, Anda tidak disarankan untuk menggunakan jumlah tingkat nested yang tinggi karena akan membahayakan kinerja akses data.

## Contoh Kode untuk Tabel Deskripsi File di proto2

Di bawah ini adalah file deskripsi tabel sesuai dengan spesifikasi sintaksis proto2:

```
syntax = "proto2";                      // Menunjukkan kesesuaian dengan spesifikasi sintaksis proto2.
package myTcaplusTable;                      // Nama paket khusus

import "tcaplusservice.optionv1.proto"; // Menentukan beberapa informasi umum dari tabel TcaplusDB yang harus diimpor dalam definisi tabel Anda.

message player { // Menggunakan pesan untuk mendefinisikan tabel, dan nama pesan adalah nama tabel.

    // Hanya pesan yang menentukan opsi kunci utama (tcaplusservice.tcaplus_primary_key) yang dapat dikenali sebagai tabel data bisnis TcaplusDB. Jika tidak, pesan tersebut hanyalah sebuah struktur.
    // Opsi kunci utama menentukan daftar nama bidang kunci utama yang dipisahkan dengan koma. Hingga empat bidang dapat ditentukan sebagai kunci utama.
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // Gunakan opsi "tcaplusservice.tcaplus_index" untuk menentukan indeks TcaplusDB.
    // Kode indeks yang disertakan dalam setiap indeks harus berupa kunci utama, dan titik temu semua kumpulan bidang indeks tidak boleh kosong.
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    // "option(tcaplusservice.tcaplus_sharding_key) = "uin";". Anda dapat secara eksplisit mengatur bidang sharding indeks. Jika tidak mengaturnya secara eksplisit, sistem akan menggunakan bidang kunci utama sebagai bidang sharding secara default.

    option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; // Gunakan fungsi enkripsi default "DefaultAesCipherSuite". Parameter ini bersifat opsional.
    option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; // Tetapkan nilai MD5 dari string kata sandi enkripsi. Parameter ini bersifat opsional.

    // Berikut ini menunjukkan definisi bidang tabel.
    // Tabel TcaplusDB mendukung jenis data berikut:
    // Jenis tidak nested: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, byte
    // Jenis nested: message
    // TcaplusDB mendukung tiga modifier bidang: REQUIRED (DIPERLUKAN), OPTIONAL (OPSIONAL), dan REPEATED (BERULANG).

    // (Hingga empat) bidang kunci utama
    required int64 uin = 1; // Bidang kunci utama harus dinyatakan dengan modifier REQUIRED. Tipe data nested tidak didukung.
    required string name = 2[(tcaplusservice.tcaplus_crypto) = true]; // Bidang jenis string dan jenis byte dalam pesan dapat ditentukan sebagai kolom terenkripsi. Parameter ini bersifat opsional.
    required int32 region = 3;
    // Sebuah tabel dapat berisi hingga empat bidang kunci utama.

    // Bidang nilai umum.
    required int32 gamesvrid = 4; // Bidang umum dapat dinyatakan dengan modifier REQUIRED, OPTIONAL, dan REPEATED.
    optional int32 logintime = 5 [default = 1];
    repeated int64 lockid = 6 [packed = true]; // Opsi "packed=true" harus ditentukan untuk bidang yang dinyatakan dengan modifier REPEATED.
    optional bool is_available = 7 [default = false]; // Anda dapat menentukan nilai default untuk bidang OPTIONAL.
    optional pay_info pay = 8; // Bidang nilai bisa dalam jenis struktur khusus.
}

message pay_info { // Gunakan pesan untuk mendefinisikan struktur.

    required int64 pay_id = 1;
    optional uint64 total_money = 2;
    optional uint64 pay_times = 3;
    optional pay_auth_info auth = 4;

    message pay_auth_info { // Jenis struktur mendukung definisi nested.
        required string pay_keys = 1;
        optional int64 update_time = 2;
    }
}
```


## Contoh Kode untuk File Deskripsi Tabel di proto3
Di bawah ini adalah file deskripsi tabel sesuai dengan spesifikasi sintaksis proto3:
```
syntax = "proto3";                      // Menunjukkan kesesuaian dengan spesifikasi sintaksis proto3.
package myTcaplusTable;                 // Nama paket khusus

import "tcaplusservice.optionv1.proto"; // Menentukan beberapa informasi umum dari tabel TcaplusDB yang harus diimpor dalam definisi tabel Anda.

message player { // Menggunakan pesan untuk mendefinisikan tabel, dan nama pesan adalah nama tabel.

    // Hanya pesan yang menentukan opsi kunci utama (tcaplusservice.tcaplus_primary_key) yang dapat dikenali sebagai tabel data bisnis TcaplusDB. Jika tidak, pesan tersebut hanyalah sebuah struktur.
    // Opsi kunci utama menentukan daftar nama bidang kunci utama yang dipisahkan dengan koma. Hingga empat bidang dapat ditentukan sebagai kunci utama.
    option(tcaplusservice.tcaplus_primary_key) = "uin,name,region";

    // Gunakan opsi "tcaplusservice.tcaplus_index" untuk menentukan indeks TcaplusDB.
    // Kode indeks yang disertakan dalam setiap indeks harus berupa kunci utama, dan titik temu semua kumpulan bidang indeks tidak boleh kosong.
    option(tcaplusservice.tcaplus_index) = "index_1(uin,region)";
    option(tcaplusservice.tcaplus_index) = "index_2(uin,name)";

    // "option(tcaplusservice.tcaplus_sharding_key) = "uin";". Anda dapat secara eksplisit mengatur bidang sharding. Jika tidak mengaturnya secara eksplisit, sistem akan menggunakan bidang kunci utama sebagai bidang sharding secara default.

    option(tcaplusservice.tcaplus_field_cipher_suite) = "DefaultAesCipherSuite"; // Gunakan fungsi enkripsi default "DefaultAesCipherSuite". Parameter ini bersifat opsional.
    option(tcaplusservice.tcaplus_cipher_md5)= "62fee3b53619b7f303c939964c6f2c4b"; // Tetapkan nilai MD5 dari string kata sandi enkripsi. Parameter ini bersifat opsional.

    // Berikut ini menunjukkan definisi bidang tabel.
    // Tabel TcaplusDB mendukung jenis data berikut:
    // Jenis tidak nested: int32, int64, uint32, uint64, sint32, sint64, bool, fixed64, sfixed64, double, fixed32, sfixed32, float, string, byte
    // Jenis nested: message

    // (Hingga empat) bidang kunci utama
    int64 uin = 1; // Bidang kunci utama harus dalam jenis non-nested.
    string name = 2[(tcaplusservice.tcaplus_crypto) = true]; // Bidang jenis string dan jenis byte dalam pesan dapat ditentukan sebagai bidang terenkripsi. Parameter ini bersifat opsional.
    int32 region = 3;
    // Sebuah tabel dapat berisi hingga empat bidang kunci utama.

    // Bidang nilai umum.
    int32 gamesvrid = 4;
    int32 logintime = 5;
    int64 lockid = 6;
    bool is_available = 7;
    pay_info pay = 8; // Bidang nilai bisa dalam jenis struktur khusus.
}

message pay_info { // Gunakan pesan untuk mendefinisikan struktur.

    int64 pay_id = 1;
    uint64 total_money = 2;
    uint64 pay_times = 3;
    pay_auth_info auth = 4;

    message pay_auth_info { // Jenis struktur mendukung definisi nested.
        string pay_keys = 1;
        int64 update_time = 2;
    }
}
```