## Menambahkan Koneksi
1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap), masuk ke halaman **Access Management** (Manajemen Akses), lalu klik **Add** (Tambahkan).
2. Di jendela pop-up, masukkan informasi koneksi.
![](https://main.qcloudimg.com/raw/d30c08d1cf9dedb12ed805bf731e073f.png)
	
	- **Project** (Proyek): proyek tempat koneksi berada, yang dapat diubah kemudian.
	- **Connection Name** (Nama Koneksi): terdiri dari maksimum 30 karakter.
	- **IP Version** (Versi IP): mendukung IPv4 atau IPv6. IPv6 hanya didukung untuk wilayah di Tiongkok Daratan.
	- **Acceleration Region** (Wilayah Akselerasi): wilayah tempat klien berada atau wilayah yang paling dekat dengan lokasi klien.
	<blockquote class="d-mod-notice">
							<div class="d-mod-title d-explain-title">
								<i class="d-icon-notice"></i>Catatan:
   						</div>
	            <p>Jaringan BGP khusus didukung di Hong Kong, Tiongkok. Jika Anda ingin menggunakannya, kirim tiket untuk menghubungi kami.</p>
						</blockquote>
	- **Origin Region** (Wilayah Asal): wilayah tempat server tujuan berada atau wilayah yang paling dekat dengan lokasi server tujuan.
	<blockquote class="d-mod-notice">
							<div class="d-mod-title d-explain-title">
								<i class="d-icon-notice"></i>Catatan:
   						</div>
	            <p>Server asal di Taiwan, Tiongkok tidak dapat mengakses wilayah akselerasi di Tiongkok Daratan, dan sebaliknya.</p>
						</blockquote>
	- **Bandwidth Cap** (Batas Bandwidth): bandwidth maksimum suatu koneksi, yaitu 10.000 Mbps (1.000 Mbps untuk beberapa koneksi).
	- **Maximum Concurrent Connections** (Koneksi Bersamaan Maksimum): jumlah maksimum koneksi bersamaan untuk sebuah koneksi, yaitu 1 juta (300.000 untuk beberapa koneksi).
	- **Tag**: mendukung klasifikasi koneksi. Item ini opsional.
	- **Fees** (Biaya): biaya untuk koneksi dan bandwidth dihitung berdasarkan bandwidth dan koneksi bersamaan yang Anda tentukan. Biaya koneksi dihitung per hari sampai koneksi dihapus, sedangkan bandwidth dikenai biaya berdasarkan batas bandwidth masuk dan keluar harian aktual.
3. Klik **OK** (Oke).
4. Di halaman **Access Management** (Manajemen Akses), lihat informasi daftar koneksi.
![](https://main.qcloudimg.com/raw/b326c683b47321704d0269a0eb047f2d.png)
	
	- **ID/Connection Name** (ID/Nama Koneksi): ID dan nama koneksi. Nama koneksi dapat diubah.
	- **VIP**: Alamat IP yang diakses oleh klien.
	- **Domain Name** (Nama Domain): nama domain yang diakses oleh klien, yang ditetapkan oleh sistem dan secara otomatis terikat ke VIP.
	- **Status**: koneksi akselerasi dapat bekerja secara normal hanya dalam status **Running** (Berjalan).

## Melihat Informasi Koneksi
1. Login ke [Konsol Global Application Acceleration Platform](https://console.cloud.tencent.com/gaap), masuk ke halaman **Access Management** (Manajemen Akses), lalu klik **ID/Connection Name** (ID/Nama Koneksi) koneksi tertentu.
 ![](https://main.qcloudimg.com/raw/3021dcb23fd2482cd7d43146b51aa96c.png)
2. Di tab **Connection Info** (Info Koneksi), Anda dapat melihat detail koneksi. **Forwarding Server IP** (IP Server Penerusan) adalah IP node penerusan di akhir koneksi akselerasi. Node penerusan ini meneruskan data koneksi akselerasi ke server asal melalui jaringan publik. Jika Anda ingin beberapa koneksi menggunakan nama domain yang sama, klik **Unified Domain Name** (Nama Domain Terpadu) untuk membuka [konfigurasi](https://console.cloud.tencent.com/gaap/domain).
![](https://main.qcloudimg.com/raw/0f3097be7c9bb138d4287683a97863d1.png) 
