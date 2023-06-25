## Migrasi Offline

### Mengapa pengunggahan dan migrasi COS memerlukan waktu lama?

Waktu yang diperlukan untuk mengunggah citra ke COS berhubungan dengan ukuran file citra dan bandwidth. Sebaiknya Anda menggunakan format citra terkompresi (qcow2 atau vhd) untuk mempersingkat waktu transmisi dan migrasi.

### Mengapa tugas migrasi gagal?

 - Saat ini, migrasi layanan Tencent Cloud mendukung citra dalam format qcow2, vhd, vmdk, dan mentah. Pastikan citra Anda menggunakan salah satu format tersebut.
 - Konfirmasikan bahwa file citra Anda sudah diunggah ke COS dan pastikan file tersebut tidak cacat atau rusak.
 - Pastikan CVM atau disk cloud yang ingin dimigrasikan tidak kedaluwarsa; jika tidak, migrasi mungkin gagal.
 
### Bagaimana cara memecahkan masalah kesalahan yang terjadi dalam tugas migrasi?
 
 - Jika "image file verification failed" (verifikasi file citra gagal) ditampilkan, biasanya karena kapasitas disk sistem atau disk data yang ingin Anda migrasikan lebih kecil dari kapasitas disk sumber atau ukuran file citra. Sesuaikan kapasitas disk sistem atau disk data dan coba lagi.
 - Jika "failed to obtain the metadata of the image file" (gagal mendapatkan metadata file citra) ditampilkan, biasanya karena file citra rusak atau format file citra tidak didukung. Harap periksa dan konfirmasikan bahwa citra sudah disiapkan, diekspor, dan diunggah dengan benar. Anda juga dapat menggunakan file citra dalam format mentah, qcow2, vhd, dan vmdk lalu coba lagi.
 - Jika pesan seperti "task timeout" (waktu tugas habis), "system error" (kesalahan sistem), dan "other reasons" (alasan lain) ditampilkan, atau jika Anda mencoba lagi dan masih gagal, silakan [hubungi kami](https://intl.cloud.tencent.com/document/product/213/34837).
 

## Migrasi Online

### Jenis sistem operasi dan disk apa yang didukung?

- Sistem operasi Linux arus utama seperti CentOS dan Ubuntu didukung.
- Migrasi tidak relevan dengan jenis dan penggunaan disk.

### Apa perbedaan antara migrasi online dan impor citra?

Keduanya dapat memigrasikan sistem sumber ke Tencent Cloud. Namun, migrasi online memungkinkan Anda mentransfer sistem dan data dari server sumber ke Tencent Cloud tanpa menyiapkan, mengekspor, dan mengimpor citra secara manual.

### Apakah IP publik server sumber akan dimigrasikan?

Tidak. Migrasi online hanya menyinkronkan data dan sistem sumber, tetapi bukan IP publik.

### Di mana saya dapat mengunduh fitur migrasi online?

[Klik di sini](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) untuk mengunduh paket fitur migrasi terkompresi dan menggunakannya seperti yang diinstruksikan di [Fitur Migrasi Online](https://intl.cloud.tencent.com/document/product/213/35640).

### Bagaimana cara menggunakan fitur migrasi online?

Salin fitur migrasi online ke server sumber dan ubah file konfigurasi sesuai kebutuhan sebelum menggunakan fitur. Anda juga dapat menulis skrip untuk melakukan operasi batch.

### Apakah fitur migrasi online mendukung mulai ulang checkpoint?

Ya. Anda dapat menjalankan fitur lagi untuk melanjutkan transfer setelah gangguan.

### Apakah saya perlu menyimpan fitur ini setelah migrasi selesai?

Tidak. Begitu migrasi selesai, Anda dapat langsung menghapus fitur di server sumber.

### Bagaimana cara memecahkan masalah kesalahan atau kegagalan migrasi?

Alasan kegagalan yang umum meliputi:
1. Port 80 dan 443 tidak terbuka di grup keamanan CVM tujuan.
2. Bidang `DataDisks` dalam file user.json tidak dikonfigurasi untuk memigrasikan disk data server sumber. Kapasitas disk sistem CVM tujuan tidak cukup untuk menyimpan semua data.
3. Tahap migrasi 3 tidak dilakukan dalam [mode jaringan pribadi](https://intl.cloud.tencent.com/document/product/213/35640#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BF.81.E7.A7.BB.E6.A8.A1.E5.BC.8F), yang menyebabkan CVM tujuan keluar dari mode migrasi.

Jika masalah berlanjut atau alasannya tidak teridentifikasi, silakan [hubungi kami](https://intl.cloud.tencent.com/document/product/213/34837) dan berikan file log migrasi (dalam direktori `log` fitur migrasi secara default).

### Bagaimana dengan kecepatan dan biaya migrasi?

- Kecepatan: ini terutama tergantung bandwidth CVM tujuan. Kami menguji CVM berbasis pembayaran sesuai pemakaian (1 inti CPU dan memori 1 GB) dengan bandwidth 12Mbps, kecepatan migrasi aktual sekitar 9Mbps/detik.
- Biaya: fitur migrasi tidak dikenakan biaya. Anda akan dikenakan biaya untuk bandwidth dan sumber daya lain yang digunakan selama migrasi. Untuk detailnya, lihat harga yang tercantum di situs web Tencent Cloud.
  
### Bisakah saya memigrasikan beberapa CVM secara bersamaan?

Ya. Anda dapat memigrasikan beberapa CVM ke CVM tujuan yang berbeda secara bersamaan.
