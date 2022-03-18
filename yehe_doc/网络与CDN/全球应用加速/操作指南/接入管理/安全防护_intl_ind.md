Global Application Acceleration Platform (GAAP) menyediakan paket perlindungan keamanan dasar secara default (bandwidth sebesar 2 Gbps untuk pengguna umum dan 10 Gbps untuk pengguna VIP). Untuk tingkat perlindungan yang lebih tinggi, buka **Assets on Cloud** (Aset di Cloud) untuk meningkatkan versi di konsol Anti-DDoS Pro.

Di konsol GAAP, Anda juga dapat mengonfigurasi daftar blokir/daftar izin. Konfigurasi dapat dilakukan dengan langkah-langkah berikut:
1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap), masuk ke halaman **Access Management** (Manajemen Akses), lalu klik **ID/Connection Name** (ID/Nama Koneksi) dari koneksi yang dipilih.
2. Pilih **Attack Defense** > **Add Rule** (Pertahanan Serangan > Tambahkan Aturan), kemudian lakukan langkah-langkah konfigurasi berikut:
	1. Tambahkan aturan akses dan pilih untuk mengizinkan atau menolak semua lalu lintas yang mengakses koneksi tersebut secara default.
	 ![](https://main.qcloudimg.com/raw/db45ecb4382cfc75b632f086caba4d2a.png)
	2. Tambahkan IP sumber, pilih protokol, dan tambahkan port protokol. Kemudian pilih **Allow** (Izinkan) atau **Reject** (Tolak) untuk memproses akses dari IP.
<img src="https://main.qcloudimg.com/raw/435c2ede3aa58b20060e828cad9db856.png" width="50%">
>? i. Maksimum 100 aturan akses dapat ditambahkan.
>
3. Klik **Confirm** (Konfirmasi).
