## Skenario Operasi 
Dokumen ini menjelaskan cara memutar kembali catatan tertentu di Konsol TcaplusDB.

## Prasyarat
Anda telah membuat tabel. Untuk informasi selengkapnya, silakan lihat [Membuat Tabel](https://intl.cloud.tencent.com/document/product/1016/32715).

## Petunjuk
1. Masuk ke halaman [Daftar Tabel](https://console.cloud.tencent.com/tcaplusdb/table), pilih tabel target dan klik **More** (Lainnya) > **Roll back** (Putar kembali) di kolom "Operation" (Operasi), atau pilih beberapa tabel dan klik **Batch Rollback** (Putar Balik Massal) di atas.
2. Di kotak dialog pop-up, unggah file .txt yang berisi nilai bidang data target.
   File dalam format berikut:
   Misalkan tabel Anda didefinisikan sebagai berikut, tempat kunci utama adalah `openid`, `tconndid`, dan `timekey`:
```
syntax = "proto2";
package myTcaplusTable;
import "tcaplusservice.optionv1.proto";
message tb_online {
    option(tcaplusservice.tcaplus_primary_key) = "openid,tconndid,timekey";
    required int32 openid = 1; //QQ Uin
    required int32 tconndid = 2;
    required string timekey = 3;
    required string gamesvrid = 4;
	optional int32 logintime = 5 [default = 1];
    repeated int64 lockid = 6 [packed = true]; 
	optional pay_info pay = 7;
	message pay_info {
		optional uint64 total_money = 1;
		optional uint64 pay_times = 2;
	}
}
```
Untuk memutar kembali catatan dengan kunci `openid` = 100, `tconndid`= 1, dan `timekey` = '123456', Anda perlu menyiapkan file yang berisi kunci sebagai berikut. Baris pertama berisi nama-nama kunci utama yang dipisahkan oleh spasi, dan baris kedua dan berikutnya berisi nilai kunci utama dari catatan yang akan diputar kembali.
```
openid tconndid timekey 
100 1 123456
```
4. Setelah file key.txt diunggah, pilih waktu pemutaran kembali dan klik **Submit** (Kirim).
![](https://main.qcloudimg.com/raw/60f9532439c46ae11803a267bed79f98.png)

