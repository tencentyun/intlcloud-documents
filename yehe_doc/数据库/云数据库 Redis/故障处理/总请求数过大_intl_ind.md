## Deskripsi Kesalahan
- Gejala 1: nilai QPS tinggi.
![](https://qcloudimg.tencent-cloud.cn/raw/a17ff6a9a1234786ebe2644ff62077bd.png)
- Gejala 2: latensi respons meningkat.
- Gejala 3: waktu koneksi habis.

## Penyebab Umum
- Bisnis perlu dioptimalkan.
- Konfigurasi instans perlu ditingkatkan.

## Solusi
- Periksa beban node: untuk arsitektur klaster, periksa beban node. Jika QPS hanya satu atau beberapa node melebihi ambang batas alarm, mungkin ada hot key; jika QPS sebagian besar node tinggi, beban keseluruhan instans TencentDB for Redis tinggi, sehingga dalam hal ini konfigurasi instans perlu ditingkatkan.
- Periksa kueri lambat: Anda dapat memeriksa apakah ada kueri lambat di konsol, dan jika memang ada dan kueri lambat cocok dengan waktu saat masalah terjadi, masalahnya mungkin disebabkan oleh big key.
- Periksa penggunaan CPU: Anda dapat memeriksa apakah penggunaan CPU terlalu tinggi, dan jika memang terlalu tinggi, sumber daya mesin mungkin tidak mencukupi, sehingga dalam hal ini konfigurasi instans perlu ditingkatkan.

Jika bisnis Anda memerlukan pengoptimalan, Anda dapat mengoptimalkannya dalam hal hot key dan big key. Jika konfigurasi instans memerlukan peningkatan, Anda dapat mengaktifkan pemisahan baca/tulis dan menambahkan lebih banyak shard untuk memenuhi kebutuhan bisnis Anda saat ini.


## Prosedur Pemecahan Masalah
### [Mengoptimalkan bisnis Anda](id:ywyh)
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans dalam daftar instans, dan masuk ke halaman manajemen instans.
2. Pada tab **System Monitoring** (Pemantauan Sistem), periksa apakah QPS tinggi atau ada hot keys yang tidak terduga.
3. Setelah memecahkan masalah akses tidak biasa, optimalkan logika bisnis Anda:
 - Hot key: Anda dapat membagi hot key dari struktur data yang kompleks menjadi beberapa kunci baru dan mendistribusikannya ke seluruh node Redis untuk mengurangi tekanan. Misalnya, jika hot key hash dua tingkat memiliki banyak elemen hash, Anda dapat membaginya.
 - Big key: jika nilainya terlalu besar, Anda dapat membagi objek menjadi beberapa nilai kunci sehingga beberapa node Redis akan berbagi tekanan. Jika ada terlalu banyak kunci, Anda dapat menyimpan beberapa kunci dalam struktur hash.


### [Meningkatkan instans](id:slsj)
#### Beban baca berat
[Tambahkan replika](#zjfb) dan aktifkan [pemisahan baca/tulis](https://intl.cloud.tencent.com/document/product/239/31935) untuk berbagi beban baca.
>!Pastikan bahwa bisnis Anda mengizinkan data yang tidak konsisten sebelum mengaktifkan pemisahan baca/tulis, karena setelah diaktifkan, data yang tidak konsisten dapat dibaca dari node replika dan node master (node replika tertinggal di belakang node master). Untuk informasi selengkapnya, lihat [Mengubah Spesifikasi Instans](https://intl.cloud.tencent.com/document/product/239/31934).

[](id:zjfb)
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), cari instans yang diinginkan dalam daftar instans, dan pilih **Configure** (Konfigurasikan) > **Add Replica** (Tambahkan Replika) di kolom **Operation** (Operasi).
![](https://qcloudimg.tencent-cloud.cn/raw/babd6ccfe0eb42326fda4e25101e50a4.png)
2. Di kotak dialog pop-up, sesuaikan konfigurasi dan klik **OK** (OKE).
3. Kembali ke daftar instans. Setelah status instans berubah menjadi **Running** (Berjalan), instans dapat digunakan secara normal.

#### Beban tulis berat
- **Arsitektur klaster** 
Login ke [konsol TencentDB for Redis]](https://console.cloud.tencent.com/redis), cari instans yang diinginkan dalam daftar instans, dan pilih **Configure** (Konfigurasikan) > **Add Shard** (Tambahkan Shard) di kolom **Operation** (Operasi).
>?
>- Setelah konfigurasi disesuaikan, instans akan dikenakan biaya konfigurasi baru.
>- Saat shard ditambahkan, sistem akan secara otomatis menyeimbangkan konfigurasi slot dan memigrasikan data, yang mungkin gagal. Disarankan untuk melakukan operasi tersebut selama jam normal untuk menghindari dampak migrasi pada akses bisnis.
>- Tambahkan shard sesuai kebutuhan: setiap shard mendukung 80.000 hingga 100.000 QPS.
>
![](https://qcloudimg.tencent-cloud.cn/raw/c9b06662d7f15daf5c7f1c89a4de54fd.png)

- **Arsitektur standar** 
Tingkatkan instans dari arsitektur standar ke arsitektur klaster untuk meningkatkan daya pemrosesan CPU. Sebelum peningkatan, Anda perlu memeriksa kompatibilitasnya. Untuk informasi selengkapnya, lihat [Memeriksa Migrasi dari Arsitektur Standar ke Arsitektur Klaster](https://intl.cloud.tencent.com/document/product/239/37594).
 1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans di daftar instans, dan masuk ke halaman detail instans.
 2. Di blok **Specs Info** (Info Spesifikasi), klik  **Upgrade Architecture** (Tingkatkan Arsitektur).
![](https://qcloudimg.tencent-cloud.cn/raw/52633dac2a97272cab593fc1eb306221.png)
 3. Setelah peningkatan selesai, buka daftar instans dan pilih **Configure**  (Konfigurasikan) > **Add Shard** (Tambahkan Shard) di kolom **Operation** (Operasi).

>?Jika masalah ini berlanjut, [kirim tiket](https://console.intl.cloud.tencent.com/workorder/category).
>
