TencentDB for Redis mendukung replikasi global untuk sinkronisasi data yang konsisten di seluruh wilayah. 

## Mengapa Replikasi Global
Ketika kode asli Redis melakukan replikasi lintas wilayah, jika instans lokal ditulis secara berlebihan atau terputus dari replikasi untuk waktu yang lama, `backlog` dari node master mungkin tidak dapat melanjutkan replikasi, sehingga mengakibatkan replikasi penuh yang harus dilakukan oleh instans jarak jauh. Ini akan memblokir akses ke dan memengaruhi bisnis normal instans jarak jauh secara serius. Untuk informasi selengkapnya, lihat [Replikasi](https://redis.io/topics/replication).

Selain itu, skema replikasi asli Redis tidak menandai node tertulis di `backlog`, yang cenderung menyebabkan pengulangan replikasi dan inkonsistensi data ketika replikasi dua arah diperlukan antara instans lokal dan jarak jauh.

## Mekanisme Implementasi
Replikasi global adalah fitur baru yang ditambahkan ke kernel versi sumber terbuka oleh Tencent Cloud. Fitur ini sepenuhnya kompatibel dengan perintah Redis 4.0 dan Redis 5.0. Berdasarkan skema replikasi pemimpin-pengikut asli, file log baru ditambahkan untuk replikasi jarak jauh guna memastikan konsistensi data pada akhirnya untuk instans di wilayah mana pun dalam grup replikasi.
- Sebelum file log direplikasi oleh node jarak jauh, node lokal akan menyimpannya untuk memastikan kelangsungan replikasi jarak jauh.
- File log berisi `ServerID` untuk mengidentifikasi ID node tempat file log ditulis dan mendukung replikasi dua arah untuk menghindari pengulangan replikasi
- File log berisi stempel waktu eksekusi perintah dan nomor versi operasi `KEY` untuk menyelesaikan konflik perintah.

![](https://qcloudimg.tencent-cloud.cn/raw/03cc44b805ae54db35c0627091cbb42f.png)


> !Replikasi global mencatat nomor versi untuk setiap `KEY`. Setiap `KEY` akan menempati 4 byte overhead memori, sehingga menghabiskan lebih banyak memori.

## Kasus Penggunaan
### Instans baca saja dan pemulihan bencana
Dalam skema replikasi global TencentDB for Redis, instans master dikonfigurasikan dalam grup replikasi, sementara instans baca saja di-deploy di beberapa wilayah dan mereplikasi data dari instans master. Versi data didasarkan pada instans master, dan tingkat konsistensi data adalah konsistensi pada akhirnya. Ini memungkinkan Anda mengakses data secara lokal dengan respons yang lebih cepat, pengalaman yang lebih baik, ketersediaan data yang lebih tinggi, dan keamanan data yang lebih baik.
![](https://qcloudimg.tencent-cloud.cn/raw/32586e18f567cfbab7adf9efbd58cc1d.png)

### Arsitektur multi-master
Jika Anda perlu menjelajah dan menggabungkan data di seluruh wilayah, Anda perlu mendistribusikan salinan data yang sama di beberapa wilayah, membaca dan memperbarui data di wilayah mana pun, atau menggabungkan data dari beberapa wilayah Dalam hal ini, database harus memiliki kemampuan untuk menulis data di beberapa wilayah. Dalam grup replikasi global, Anda dapat mengonfigurasi arsitektur multi-master, sehingga data yang ditulis ke satu instans master akan disinkronkan ke instans master lain di wilayah lain
![](https://qcloudimg.tencent-cloud.cn/raw/1702367157d53cf5e3b177eca2577f16.png)
> !Instans master TencentDB for Redis tidak melakukan deteksi versi dan pemeriksaan waktu penulisan untuk data yang ditulis oleh aplikasi dan instans master lainnya dalam grup replikasi; sebagai gantinya, mereka menjalankan perintah secara kronologis sesuai dengan urutan perintah yang terima. Jika data yang sama diperbarui dalam instans master yang berbeda pada saat yang sama, data yang direplikasi secara global mungkin tidak selaras dan tidak konsisten.
> Oleh karena itu, dalam skenario multi-master, hindari memperbarui data yang sama di instans master yang berbeda secara bersamaan. Karena arsitektur multi-instans dapat menyebabkan inkonsistensi data, evaluasi dengan cermat apakah arsitektur tersebut cocok untuk bisnis Anda.

