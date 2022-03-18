## Mode Pemulihan Windows

**Windows Recovery** (Pemulihan Windows) adalah fitur pemulihan otomatis Windows. Saat Windows mendeteksi masalah sistem tertentu dan yakin bahwa berjalan terus menerus akan menyebabkan kerusakan sistem, fitur perbaikan otomatis ini akan mencegah Windows memulai dan memberikan **System Recovery Options** (Opsi Pemulihan Sistem) kepada pengguna untuk memperbaiki, mencadangkan atau memulihkan sistem. 
**System Recovery Options** (Opsi Pemulihan Sistem) mencakup **Startup Repair** (Perbaikan Startup), **System Restore** (Pemulihan Sistem), dan **Windows Memory Diagnostic** (Diagnostik Memori Windows), yang dapat membantu pengguna memperbaiki masalah, mencadangkan data, dan memulihkan sistem.
Jika Anda tidak dapat login ke CVM dari jarak jauh, dan melihat gambar berikut saat login ke CVM melalui konsol, berarti CVM Windows telah memasuki mode pemulihan.
![](//mc.qcloudimg.com/static/img/e278c336a415066dcb8fc58333395ac3/image.png)

## Alasan
Dalam situasi berikut, sistem dapat memasuki mode pemulihan.
- **The power was cut off while Windows was running or shutting down.** (Daya terputus saat Windows sedang berjalan atau dimatikan.) Sistem Windows dimatikan secara paksa melalui konsol. Kedua skenario dapat menyebabkan hilangnya data penting.
- **The power was cut off while Windows was updating.** (Daya terputus saat Windows sedang melakukan pembaruan.) Situasi ini dapat menyebabkan hilangnya data pembaruan penting.
- **The system was damaged by Trojans or viruses.** (Sistem dirusak oleh Trojan atau virus.)
- **There were bugs in Windows core services** (Ada bug di layanan inti Windows). Windows mendeteksi risiko.
- **The system lost critical data or was damaged** (Sistem kehilangan data penting atau rusak). File sistem rusak karena salah operasi.

## Tindakan pencegahan
Tindakan pencegahan yang direkomendasikan adalah sebagai berikut:
 - Login ke konsol untuk memantau proses pematian sistem Windows. Tencent Cloud mendukung soft shutdown yang dilengkapi dengan mekanisme waktu habis. Jika proses pematian belum selesai dalam jangka waktu yang ditentukan, akan muncul pesan kegagalan. Jika proses pematian lambat atau Windows Update dimulai, jangan paksa proses pematian; sebagai gantinya, tunggu saja hingga proses pematian selesai. Untuk informasi selengkapnya, harap lihat [Skenario Kegagalan Pematian](https://intl.cloud.tencent.com/document/product/213/2917#shutdown-failure-scenarios).
 - Periksa apakah ada program atau proses yang tidak normal dalam sistem, seperti Trojan atau virus.
 - Periksa apakah sistem pengelolaan dan perangkat lunak anti-virus berjalan dengan benar.
 - Instal pembaruan Windows tepat waktu, terutama pembaruan penting dan pembaruan keamanan.
 - Periksa rutin log peristiwa sistem untuk memperbaiki bug di layanan inti.

## Solusi
 Jika Windows memasuki mode pemulihan, lakukan langkah-langkah berikut untuk melanjutkan proses startup atau mengizinkan Windows memperbaiki masalah kecil secara otomatis.
1. Login ke CVM melalui [konsol CVM](https://console.cloud.tencent.com/cvm).
2. Di halaman mode pemulihan yang muncul, klik **Next** (Selanjutnya).
![](//mc.qcloudimg.com/static/img/94a1cf0f55d2c449a9d026bbbad5e4cd/image.png)
3. Di jendela **System Recovery Options** (Opsi Pemulihan Sistem), klik **Next** (Selanjutnya) untuk menggunakan solusi default, seperti yang ditunjukkan di bawah ini:
![](//mc.qcloudimg.com/static/img/d178865f822d2146eb3bb58f1b851294/image.png)
4. Klik **Restart** (Mulai Ulang), lalu tekan **F8** (F8) dengan cepat.
![](//mc.qcloudimg.com/static/img/ab2fdd697015fcb7e53b287052086b65/image.png)
5. Pilih **Start Windows Normally** (Mulai Windows Secara Normal).
 ![](https://main.qcloudimg.com/raw/c3c62a6d77a2fe41d0ad02899faa06ed.png)
Jika proses startup gagal, instal ulang sistem melalui konsol. Untuk informasi selengkapnya, lihat [Menginstal ulang sistem melalui konsol](https://intl.cloud.tencent.com/document/product/213/4933#useConsole).


