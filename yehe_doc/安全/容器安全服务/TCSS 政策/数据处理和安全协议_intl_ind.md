## 1\. LATAR BELAKANG

Modul ini berlaku jika Anda menggunakan Tencent Container Security Service (“**Fitur**”). Modul ini dimasukkan dalam Perjanjian Keamanan dan Pemrosesan Data yang terdapat di (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)”). Istilah-istilah yang digunakan tetapi tidak didefinisikan dalam Modul ini memiliki arti yang sama dengan yang ditetapkan dalam DPSA. Jika terdapat perbedaan antara DPSA dengan Modul ini, Modul inilah yang akan berlaku apabila terjadi ketidaksesuaian.

## 2\. PEMROSESAN

Kami akan memproses data berikut sehubungan dengan Fitur:

| **Informasi Pribadi**                                     | **Penggunaan**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Data Dasar Aset:** Informasi dasar server, kontainer, gambar, dan klaster Anda (informasi sidik jari aset (pemantauan sumber daya, akun, port, aplikasi perangkat lunak, proses, database, aplikasi web, layanan web, kerangka kerja web, situs web, layanan startup paket Jar, tugas terjadwal, variabel lingkungan, modul kernel), informasi dasar repositori gambar (alamat repositori gambar, jenis repositori, nama gambar, ID gambar, versi gambar, ukuran gambar, risiko keamanan (termasuk kerentanan keamanan, virus Trojan, informasi sensitif), riwayat konstruksi) | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/>Harap dicatat bahwa data ini disimpan dan dicadangkan di fitur TencentDB for MongoDB (MongoDB) dan TencentDB for MySQL (MySQL) kami, disimpan sementara dan dicadangkan di fitur Cloud Object Storage (COS) kami,  dan terintegrasi dengan Layanan Hosting yang relevan (sebagaimana didefinisikan dalam modul Kebijakan Privasi untuk Fitur ini) langganan Anda. Jika Anda telah membeli klaster Tencent Kubernetes Engine (TKE) kami, informasi dasar repositori gambar juga dibagikan kepada kami atas otorisasi Anda, untuk tujuan menyediakan Fitur kepada Anda (termasuk untuk melakukan pemeriksaan keamanan). |
| **Data Konfigurasi Konsol:**<br/><li>Konfigurasi gambar, klaster, kerentanan, baseline, file,  deteksi log: deteksi rutin, abaikan kerentanan / baseline, konfirmasi Anda untuk memercayai file atau mengisolasi file, menahan proses, menahan gambar, menahan akses jaringan kontainer)<li>Konfigurasi daftar putih untuk pelarian kontainer, shell terbalik, pemeriksaan file, proses abnormal, gangguan file, panggilan drop sistem berisiko tinggi, dan fitur pencegahan intrusi lainnya: kondisi daftar putih, rentang cermin efektif Informasi konfigurasi lainnya: pengaturan perlindungan peningkatan server otomatis, pengaturan pembaruan otomatis, pengaturan alarm | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda sesuai konfigurasi spesifik Anda.<br/>Harap dicatat bahwa data ini disimpan dan dicadangkan di fitur TencentDB for MongoDB (MongoDB) dan TencentDB for MySQL (MySQL) kami, dan terintegrasi dengan Layanan Hosting yang relevan (sebagaimana didefinisikan dalam modul Kebijakan Privasi untuk Fitur ini) langganan Anda. |

## 3\. WILAYAH LAYANAN

Sebagaimana ditentukan dalam DPSA.

## 4\. SUB-PEMROSES

Sebagaimana ditentukan dalam DPSA.

## 5\. PENYIMPANAN DATA

Kami akan menyimpan data pribadi yang diproses sehubungan dengan Fitur sebagai berikut:

| **Informasi Pribadi**   | **Kebijakan Penyimpanan**                                         |
| -------------------------- | ------------------------------------------------------------ |
| Data Dasar Aset           | Kami menyimpan data ini selama minimal 180 hari. Kami menyimpan data tersebut sampai Anda menghentikan penggunaan Anda atas Layanan Hosting yang relevan, dalam hal ini kami akan menyimpan sementara data ini di fitur COS kami dan menghapus (i) 30 hari setelahnya yang sama atau (ii) setelah jumlah hari minimum yang diperlukan untuk memenuhi ambang batas retensi data minimum 180 hari (sebagaimana berlaku). |
| Data Konfigurasi Konsol | Disimpan sampai Anda meminta penghapusan, di mana data tersebut akan dihapus dalam waktu 30 hari. Jika Anda tidak meminta penghapusan, data tersebut akan dihapus setelah 1 bulan penghentian penggunaan Fitur ini oleh Anda, kecuali diwajibkan lain oleh undang-undang perlindungan data yang berlaku. |

Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.

## 6\. PERSYARATAN KHUSUS

Anda harus memastikan bahwa Fitur ini hanya digunakan oleh pengguna akhir yang setidaknya berusia minimum yang memungkinkan individu untuk menyetujui pemrosesan data pribadi. Persyaratan ini mungkin berbeda-beda, bergantung pada wilayah hukum tempat pengguna akhir berada.

Fitur ini tidak dimaksudkan untuk pemrosesan data sensitif. Anda harus memastikan bahwa Fitur ini tidak digunakan untuk mentransfer atau memproses data sensitif apa pun oleh Anda atau pengguna akhir Anda.