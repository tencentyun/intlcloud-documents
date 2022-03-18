## Membuat Pendengar TCP/UDP
1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap). Masuk ke halaman **Access Management** (Manajemen Akses). Klik **ID/Connection Name** (ID/Nama Koneksi) koneksi tertentu.
2. Di halaman yang muncul, pilih **TCP/UDP Listener Management** > **Create** (Manajemen Pendengar TCP/UDP > Buat). Detail terkait konfigurasi dapat dilihat di bagian berikut:
	1. Konfigurasi informasi pendengar untuk mengatur pemetaan antara protokol dan port.
	![](https://main.qcloudimg.com/raw/ccb559a46fe23d7cbaf67e0a80cd21b2.png) 
		
		- **Origin Server Type** (Jenis Server Asal): mendukung alamat IP atau nama domain. Satu server hanya mendukung satu jenis. (Catatan: jenis nama domain saat ini tidak didukung untuk koneksi IPv6).
		- **Get Client IP** (Dapatkan IP Klien): Pilih TOA atau Proxy Protocol (Protokol Proksi) untuk mendapatkan IP sesungguhnya pengguna. Untuk informasi selengkapnya, lihat [Prinsip Dasar](https://intl.cloud.tencent.com/document/product/608/14429).
		- **Source Port** (Port Sumber): Port akses koneksi akselerasi VIP. Rentang yang valid: 1–64999 (port 21 saat ini tidak tersedia). Port tunggal atau rentang port yang berurutan didukung. Port harus unik. Jumlah maksimum port berurutan yang dapat ditambahkan sekaligus adalah 20 port, misalnya 8000–8019.
	2. Konfigurasi kebijakan pemrosesan server asal; yaitu, jika pendengar terikat ke beberapa server asal, Anda harus memilih kebijakan penjadwalan untuk server asal.
	 ![](https://main.qcloudimg.com/raw/eada50bba6b187bbf1063c85a9bb82d8.png)
		
		- **RR**: Beberapa server asal melakukan origin-pull sesuai dengan kebijakan RR.
		- **Weighted RR** (RR Tertimbang): - Beberapa server asal melakukan origin-pull sesuai dengan rasio bobot (Anda dapat mengatur bobot setiap server asal saat mengikat pendengar).
		- **Least Connections** (Koneksi Terkecil): Menjadwalkan server asal dengan jumlah koneksi paling sedikit terlebih dahulu.
		- **Least Latency** (Latensi Terkecil): Menjadwalkan server asal dengan latensi terkecil terlebih dahulu.
		- **Secondary Origin Server** (Server Asal Sekunder): Mengaktifkan perpindahan server asal primer/sekunder (untuk mengaktifkan fitur ini, Anda harus mengaktifkan pemeriksaan kesehatan server asal).
		<blockquote class="d-mod-notice">
							<div class="d-mod-title d-explain-title">
    							<i class="d-icon-notice"></i>Catatan:
	    					</div>
		       <p>Pendengar dengan server asal tipe nama domain hanya mendukung **RR** dan **Least Connections** (Koneksi Terkecil) sebagai kebijakan penjadwalan dan tidak mendukung server asal sekunder.</p>
						</blockquote>
	3. Jika pendengar TCP digunakan, Anda dapat memilih untuk mengonfigurasi mekanisme pemeriksaan kesehatan untuk secara otomatis mendeteksi dan menghapus server asal pengecualian. Jika server asal sekunder diaktifkan, Anda tidak akan dapat menonaktifkan pemeriksaan kesehatan.
	 ![](https://main.qcloudimg.com/raw/ebd2d05dd1fbab5531d4897fd0b8c046.png)
		
		- **Response Timeout** (Waktu Respons Habis): periode batas waktu untuk suatu respons.
		- **Health Check Interval** (Interval Pemeriksaan Kesehatan): interval antara dua pemeriksaan kesehatan berturut-turut.
		- **Unhealthy Threshold** (Ambang Batas Tidak Sehat): jumlah pemeriksaan pendengar yang gagal berturut-turut dan ditampilkan sebelum server asal dianggap tidak sehat. Jika server asal dianggap tidak sehat, penerusan paket tidak akan dilanjutkan hingga server asal kembali normal. 
		- **Healthy Threshold** (Ambang Batas Sehat): jumlah pemeriksaan pendengar yang berhasil berturut-turut sebelum server asal dianggap sehat. Jika server asal dianggap sehat, penerusan paket akan dilanjutkan.
	4. Pilih persistensi sesi akan diaktifkan atau tidak.
	 ![](https://main.qcloudimg.com/raw/2e7471ba4795c532966dbc67f391c81d.png)
		- **Session Persistence** (Persistensi Sesi): permintaan pengguna dari IP yang sama akan mengakses server asal yang sama.
		- **Hold Time** (Waktu Tunggu): durasi persistensi sesi. Jika pendengar tidak memiliki permintaan untuk jangka waktu yang lebih lama dari waktu tunggu, persistensi sesi akan terputus secara otomatis.
3. Klik **Complete** (Selesai).

## Mengonfigurasi Pendengar TCP/UDP
Buka tab **TCP/UDP listener management** (Manajemen pendengar TCP/UDP), klik **Set** (Atur) di kolom operasi pendengar tertentu untuk memodifikasi namanya serta menjadwalkan kebijakan dan parameter pemeriksaan kesehatannya.
## Mengikat Server Asal
1. Pilih tab **TCP/UDP Listener Management** (Manajemen Pendengar TCP/UDP), lalu klik **Bind Origin Server** (Ikat Server Asal) di sebelah kanan "Pendengar TCP/UDP" yang dibuat untuk mengikat atau melepas ikatan satu atau beberapa server asal. Jika tidak ditemukan informasi server asal seperti yang ditampilkan di konsol, mungkin jenis server asal tidak valid atau server asal tidak ditambahkan ke [Manajemen Server Asal](https://console.cloud.tencent.com/gaap/listrs).
 ![](https://main.qcloudimg.com/raw/7777f065d6f2c6e0b04aeca4f8deeb9a.png)
2. Pilih server asal dan konfigurasikan port origin-pull.
	- Jika RR primer/sekunder diaktifkan untuk pendengar, Anda perlu mengatur **Primary Origin Server** (Server Asal Utama) dan **Secondary Origin Server** (Server Asal Sekunder) di halaman **Bind Origin Server** (Ikat Server Asal).
	- Jika ingin mengatur port beberapa server asal, Anda dapat menggunakan fitur **Cover Port/Complement Port** di sudut kanan atas. Meskipun Anda telah mengatur port server asal sebelumnya, fitur **Cover Port** tetap akan mengatur server asal tujuan yang Anda pilih ke nomor port yang Anda masukkan. Jika tidak ada port yang diatur untuk server asal tujuan yang dipilih, Anda dapat menggunakan fitur **Complement Port** untuk pengaturan terpadu guna mengurangi beban kerja berulang.
	- Jika kebijakan pendengar adalah **Weighted RR** (RR Tertimbang), Anda dapat mengatur bobot (1–100) suatu server asal saat mengikatnya. Server asal dijadwalkan berdasarkan rasio bobotnya terhadap bobot total. Misalnya, jika bobot server asal 1 adalah 60 dan bobot server asal 2 adalah 80, rasio penjadwalannya adalah 60/(60 + 80) = 42,8% untuk server asal 1 atau 57,2% untuk server asal 2.
	 ![](https://main.qcloudimg.com/raw/ddb99c5d31ee860aa75687cc722bcc60.png)
	- Jika diaktifkan, pemeriksaan kesehatan akan dimulai saat server asal terikat. Anda dapat mengetahui normal atau tidaknya server asal dengan memeriksa status pendengar. Koneksi akselerasi hanya akan meneruskan paket ke server asal dalam status normal. Paket tidak akan diteruskan ke server asal yang tidak normal, dan akan diteruskan setelah server asal kembali ke status normal selama pemeriksaan kesehatan.
	- Jika pemeriksaan kesehatan tidak diaktifkan, atau jika Anda menggunakan pendengar UDP, koneksi akselerasi akan selalu meneruskan paket ke server asal dalam status normal maupun tidak normal.
	 ![](https://main.qcloudimg.com/raw/cc79b67e828e33377bd83ff5ba7d356e.png)
3. Konfirmasi konfigurasi.
Setelah Anda menyelesaikan konfigurasi server asal, klik **Next** (Selanjutnya) untuk masuk ke halaman konfirmasi konfigurasi. Di halaman ini, Anda dapat melihat informasi koneksi dan detail pendengar yang saat ini dikonfigurasikan.
 ![](https://main.qcloudimg.com/raw/11a39a5defaea8d2540e037334ba93ab.png)
4. Klik **Complete** (Selesai).

## Menghapus Pendengar TCP/UDP
Buka tab **TCP/UDP Listener Management** (Manajemen Pendengar TCP/UDP), klik **Delete** (Hapus) di pendengar yang akan dihapus. Jika pendengar terikat ke server asal, Anda perlu mencentang **Allow force deletion of listeners bound with origin servers** (Izinkan penghapusan paksa pendengar yang terikat ke server asal) terlebih dahulu. Setelah pendengar dihapus, layanan akselerasi untuk port pendengar akan berhenti.
 ![](https://main.qcloudimg.com/raw/987d8c8ca0937b698d60941959713c00.png)