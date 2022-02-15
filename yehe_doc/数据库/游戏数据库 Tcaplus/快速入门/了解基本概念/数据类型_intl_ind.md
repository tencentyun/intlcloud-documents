TencentDB for TcaplusDB mendukung jenis data Protocol Buffers.

## Pemetaan antara proto3 dan Jenis Data dalam Bahasa Pemrograman Lain

| .proto | C++ | Java | Python | Go | Ruby | C\# | PHP| Dart | Notes |    
| ------------ | ---------- | ---------- | ----------- | -------- | ---------------- | ---------- | -------------- | --------- | ----------- |
| double       | double     | double     | float       | float64  | float    | double     | float          | double    |     -     |
| float        | float      | float      | float       | float32  | float               | float      | float          | double    |  -  |
| int32        | int32      | int        | int         | int32    | fixnum/<br>bignum<br>(sebagaimana diperlukan) | int        | integer        | int       | Menggunakan pengkodean panjang variabel.<br>Tidak efisien untuk pengkodean angka negatif. Jika bidang cenderung memiliki nilai negatif, gunakan sint32 sebagai gantinya. |
| int64        | int64      | long       | int/long    | int64    | bignum                        | long       | integer/<br>string | Int64     | Menggunakan pengkodean panjang variabel.<br>Tidak efisien untuk pengkodean angka negatif. Jika bidang cenderung memiliki nilai negatif, gunakan sint64 sebagai gantinya. |
| uint32       | uint32     | int        | int/long    | uint32   | fixnum/<br>bignum<br>(sebagaimana diperlukan) | uint       | integer        | int       | Menggunakan pengkodean panjang variabel.                                           |
| uint64       | uint64     | long       | int/long    | uint64   | bignum                        | ulong      | integer/<br>string | Int64     | Menggunakan pengkodean panjang variabel.                                           |
| sint32       | int32      | int        | int         | int32    | fixnum/<br>bignum<br>(sebagaimana diperlukan)| int        | integer        | int       | Menggunakan pengkodean panjang variabel.                                           |
| sint64       | int64      | long       | int/long    | int64    | bignum                        | long       | integer/<br>string | Int64     | Menggunakan pengkodean panjang variabel.<br>Nilai int yang ditandatangani. Ini menyandikan angka negatif secara lebih efisien dibanding int32 biasa. |
| fixed32      | uint32     | int        | int/long    | uint32   | fixnum/<br>bignum<br>(sebagaimana diperlukan)| uint       | integer        | int       | Selalu empat byte.<br>Lebih efisien dari uint32 jika nilai umumnya lebih besar dari 2^28.     |
| fixed64      | uint64     | long       | int/long    | uint64   | bignum                        | ulong      | integer/<br>string | Int64     | Selalu delapan byte.<br>Lebih efisien dari uint64 jika nilai umumnya lebih besar dari 2^56.      |
| sfixed32     | int32      | int        | int         | int32    | fixnum/<br>bignum<br>(sebagaimana diperlukan)| int        | integer        | int       | Selalu empat byte.                                             |
 sfixed64     | int64      | long       | int/long    | int64    | bignum                        | long       | integer/<br>string | Int64     | Selalu delapan byte.                                             |
| bool         | bool       | boolean    | bool        | bool     | trueClass/<br>falseClass          | bool       | boolean        | bool      |           -             |
| string       | string     | String     | str/unicode | string   | string<br>(UTF -8)            | string     | string      | string    | String harus selalu berisi teks ASCII yang dikodekan UTF-8 atau 7-bit, dan tidak boleh lebih panjang dari 2^32. |
| bytes        | string     | ByteString | str         | byte | string<br>(ASCII-8BIT)        | bytestring | string      |  -         |  Dapat berisi urutan byte apa pun yang tidak lebih panjang dari 2^32.                          |


## Pemetaan antara proto2 dan Jenis Data dalam Bahasa Pemrograman Lain

| .proto | C++ | Java  | Python               | Go   | Notes                       |
| ------------ | ---------- | ---------- | ---------------- | --------- | ---------------------------------- |
| double       | double     | double     | float                                    | \*float64 |   -            |
| float        | float      | float      | float                                    | \*float32 |                -    |
| int32        | int32      | int        | int                                      | \*int32   | Menggunakan pengkodean panjang variabel. Tidak efisien untuk pengkodean angka negatif. Jika bidang cenderung memiliki nilai negatif, gunakan sint32 sebagai gantinya. |
| int64        | int64      | long       | int/long                                 | \*int64   |  Menggunakan pengkodean panjang variabel. Tidak efisien untuk pengkodean angka negatif. Jika bidang cenderung memiliki nilai negatif, gunakan sint64 sebagai gantinya. |
| uint32       | uint32     | int        | int/long                                 | \*uint32  |  Menggunakan pengkodean panjang variabel.                                           |
| uint64       | uint64     | long       | int/long                                 | \*uint64  | Menggunakan pengkodean panjang variabel.                                           |
| sint32       | int32      | int        | int                                      | \*int32   | Menggunakan pengkodean panjang variabel. Nilai int bertanda. Ini menyandikan angka negatif secara lebih efisien dibanding int32 biasa. |
| sint64       | int64      | long       | int/long                                 | \*int64   |  Menggunakan pengkodean panjang variabel. Nilai int bertanda. Ini lebih efisien mengkodekan angka negatif dibanding int64 biasa. |
| fixed32      | uint32     | int        | int/long                                 | \*uint32  | Selalu empat byte. Lebih efisien dari uint32 jika nilai umumnya lebih besar dari 2^28.      |
| fixed64      | uint64     | long       | int/long                                 | \*uint64  | Selalu delapan byte. Lebih efisien dari uint64 jika nilai umumnya lebih besar dari 2^56.      |
| sfixed32     | int32      | int        | int                                      | \*int32   | Selalu empat byte.                                             |
| sfixed64     | int64      | long       | int/long                                 | \*int64   | Selalu delapan byte.                                             |
| bool         | bool       | boolean    | bool                                     | \*bool    |   -                        |
| string       | string     | String     | unicode(Python 2)<br>or<br>str(Python 3) | \*string  | String harus selalu berisi teks ASCII yang dikodekan UTF-8 atau 7-bit.                 |
| byte        | string     | ByteString | byte                                    | byte  | Dapat berisi urutan byte yang berubah-ubah.                                       |

