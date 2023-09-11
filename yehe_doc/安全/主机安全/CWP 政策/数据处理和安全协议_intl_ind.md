## 1\. LATAR BELAKANG

Modul ini berlaku jika Anda menggunakan Cloud Workload Protection Platform (CWPP) (“**Fitur**”). Modul ini tergabung dalam Perjanjian Pemrosesan dan Keamanan Data yang terdapat di (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)”). Istilah-istilah yang digunakan tetapi tidak didefinisikan dalam Modul ini memiliki arti yang sama dengan yang ditetapkan dalam DPSA. Jika terdapat perbedaan antara DPSA dengan Modul ini, Modul inilah yang akan berlaku apabila terjadi ketidaksesuaian.

## 2\. PEMROSESAN

Kami akan memproses data berikut sehubungan dengan Fitur:

| **Informasi Pribadi**                                     | **Penggunaan**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Sumber Daya yang Dilindungi Klien Informasi: <br><li>**Untuk perlindungan Server Tencent Cloud**: APPID, UIN, informasi server Anda (nama, alamat IP, jenis, OS, versi agen, tanggal angsuran agen, waktu login terakhir, status online, komponen terpasang, dan tingkat keamanan) <br><li>**Untuk perlindungan server non-Tencent Cloud**: Pemantauan sumber daya, akun, port, aplikasi perangkat lunak, proses, basis data, aplikasi web, layanan web, kerangka kerja web, situs web, paket jar, layanan startup, tugas terjadwal, variabel lingkungan, modul kernel | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda. <br/> Harap dicatat bahwa kecuali Anda mengizinkan, kami tidak memiliki akses ke data pribadi, jika ada, yang disimpan dalam basis data atau kontrol atas data.<br/> Harap diperhatikan bahwa data ini disimpan dan dicadangkan dalam fitur TencentDB for MySQL (MySQL) kami. |
| Insiden Keamanan Informasi: **Untuk langganan gratis Fitur:** <br><li>Informasi deteksi penyusupan: peristiwa seperti login abnormal server klien, peretasan kata sandi; informasi mengenai peristiwa yang relevan (server UUID, detail peristiwa, tingkat ancaman, dan status pemrosesan). **Untuk langganan berbayar Fitur, berikut ini juga diproses:** <br><li> Informasi deteksi tentang titik lemah keamanan server: UUID server yang terpengaruh, nama dan deskripsi dari titik lemah keamanan yang terdeteksi, status saat ini, tanggal dan waktu deteksi terbaru; <br><li>Informasi garis besar keamanan: UUID server, nama baseline keamanan, jenis deteksi, tingkat ancaman keamanan, status saat ini, tanggal dan waktu deteksi terbaru; <br><li>Laporan keamanan server: Jumlah total login abnormal klien yang dicatat, hasil pemindaian kerentanan, peretasan kata sandi, dan pemindaian file berbahaya; jumlah dan jenis langganan Fitur yang dibeli oleh Anda. | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda. Kami juga dapat menganonimkan dan menghapus identifikasi informasi insiden keamanan tertentu untuk meningkatkan Fitur. <br/>Harap diperhatikan bahwa data ini disimpan dan dicadangkan dalam fitur MySQL kami. |
| Data Konfigurasi Klien: <br><li>Konfigurasi deteksi kerentanan/baseline/file: pengaturan deteksi reguler, kerentanan/baseline yang diabaikan, file tepercaya, file yang dikarantina; <br><li>Konfigurasi daftar putih untuk fungsi pencegahan intrusi: ketentuan daftar putih, server tertutup; <br><li>Konfigurasi lain: pengaturan peningkatan perlindungan otomatis, pengaturan perpanjangan otomatis, dan pengaturan alarm. | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda sesuai konfigurasi spesifik Anda. <br/>Harap diperhatikan bahwa data ini disimpan dan dicadangkan dalam fitur MySQL kami. |

## 3\. WILAYAH LAYANAN

Sebagaimana ditentukan dalam DPSA.

## 4\. SUB-PROSESOR

Sebagaimana ditentukan dalam DPSA.

## 5\. RETENSI DATA

Kami akan menyimpan data pribadi yang diproses sehubungan dengan Fitur sebagai berikut:

| **Informasi Pribadi**                                     | **Kebijakan Retensi**                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Informasi Sumber Daya yang Dilindungi Klien Informasi Insiden Keamanan Data Konfigurasi Klien | Kami menyimpan data tersebut hingga Anda menghapusnya secara manual. Jika tidak, saat Anda menghentikan langganan Fitur atau menghapus akun Anda, kami akan menghapus data tersebut dalam waktu 7 hari. |

Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.

## 6\. PERSYARATAN KHUSUS

Anda harus memastikan bahwa Fitur ini hanya digunakan oleh pengguna akhir yang setidaknya berusia minimum yang memungkinkan individu untuk menyetujui pemrosesan data pribadi. Persyaratan ini mungkin berbeda-beda, bergantung pada wilayah hukum tempat pengguna akhir berada.