
## Langkah 1. Tambahkan server asal

1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap).
2. Klik **Origin Server Management** (Manajemen Server Asal) > **Create** (Buat), atur nama, masukkan IP server asal atau nama domain, dan tambahkan tag (opsional) untuk menambahkan informasi semua server yang akan mempercepat akses ke **Origin Server Management** (Manajemen Server Asal). Anda dapat memasukkan informasi beberapa server asal sekaligus.
3. Klik **OK** (Oke).
![](https://main.qcloudimg.com/raw/700758b2be655f701f88ddc2f72857fc.png)
4. (Opsional) Tambahkan alias ke server asal untuk penggunaan di masa mendatang: klik ikon **Edit** di samping nama server asal, masukkan nama, dan klik **OK** (Oke).
![](https://main.qcloudimg.com/raw/c72f5506cc15b41a93fb8ce64767108f.png)

## Langkah 2. Buat koneksi akselerasi

1. Klik **Access Management** (Manajemen Akses) > **Create** (Buat).
![](https://main.qcloudimg.com/raw/5f424ce7a93036ad42f1adb174bdffbc.png)
2. Pada jendela **Add a connection** (Tambahkan koneksi), masukkan informasi koneksi akselerasi.
![](https://main.qcloudimg.com/raw/e2c839706090fbce1d01d7ecae40310c.png)
	- Node Akses: entri koneksi akselerasi. Pilih node di wilayah klien atau wilayah terdekat.
	- Node Origin-Pull: koneksi akselerasi keluar. Pilih node di wilayah server tujuan atau wilayah terdekat.
	- Batas Bandwidth: batas atas bandwidth koneksi.
	- Koneksi Bersamaan Maksimum: jumlah maksimum koneksi bersamaan yang didukung oleh koneksi.
3. Klik **OK** (OKE). Setelah berhasil dibuat, Anda dapat melihat informasi koneksi, dengan **VIP** dan **Domain Name** (Nama Domain) adalah alamat akses koneksi akselerasi.
![](https://main.qcloudimg.com/raw/f398e22ba4e21ac9055b30141c049a7e.png)
4. Klik **ID/Connection Name** (ID/Nama Koneksi) koneksi untuk melanjutkan ke halaman selanjutnya.

## Langkah 3. Buat pendengar

1. Pilih tab **TCP/UDP Listener Management** (Manajemen Pendengar TCP/UDP), klik **Create** (Buat), dan tambahkan kebijakan penerusan di jendela pop-up.
2. Konfigurasi informasi pendengar (dengan TCP sebagai contoh) untuk mengatur pemetaan antara protokol akselerasi dan port pendengaran. Anda dapat memetakan beberapa port pendengaran sekaligus, tetapi port tersebut harus unik.
	- Port Pendengaran: port akses koneksi akselerasi VIP.
<img src="https://main.qcloudimg.com/raw/f611bf8653bce37ace29e99ebbb75f7b.png" width=70%>
3. Konfigurasi kebijakan pemrosesan server asal; yaitu, ketika pendengar terikat dengan beberapa server asal, Anda harus memilih kebijakan penjadwalan untuk server asal seperti yang ditunjukkan di bawah ini:
<img src="https://main.qcloudimg.com/raw/5454a77683dca1cfb491eccdae839aa4.png" height="207" width="408" />
4. Konfigurasi mekanisme pemeriksaan kesehatan server asal.
   Jika protokol TCP digunakan, mekanisme pemeriksaan kesehatan harus dikonfigurasi. Pilih **Enable Health Check** (Aktifkan Pemeriksaan Kesehatan) lalu konfigurasikan waktu respons dan interval pemantauan.
![img](https://main.qcloudimg.com/raw/c41a39a9a851fbe3778ca325edc2e3f8.png)
	- Waktu Respons Habis: periode batas waktu untuk suatu respons.
	**Health Check Interval** (Interval Pemeriksaan Kesehatan) mengacu pada interval antara dua pemeriksaan kesehatan berturut-turut. Jika pemeriksaan kesehatan menentukan bahwa server asal tidak normal, server asal akan berhenti meneruskan paket hingga pulih ke status normal pada pemeriksaan kesehatan lainnya.
	- Ambang Batas Tidak Sehat/Sehat: menunjukkan jumlah pemeriksaan gagal/berhasil berturut-turut sebelum server asal dianggap tidak sehat/sehat.





## Langkah 4. Ikat server asal

1. Pilih pendengar dan klik **Bind Origin Server** (Ikat Server Asal) di kolom **Operation** (Operasi).
2. Tambahkan semua server asal yang akan diikat dalam daftar di sebelah kiri ke kotak di sebelah kanan lalu masukkan nomor port server asal.
![](https://main.qcloudimg.com/raw/7fd67c2a72a2c57d2c626596ce74cf4d.png)

## Langkah 5. Gunakan koneksi akselerasi

Setelah menyelesaikan langkah-langkah di atas, Anda dapat menggunakan koneksi untuk akselerasi saat status pendengar menjadi **Normal** (Normal).
![](https://main.qcloudimg.com/raw/27c637a5321fde96212d7f48dc4a57de.png)

1. **Access methods** (Metode akses)
	- Metode 1: ketika klien mengakses port VIP +, akselerasi dari klien ke server tujuan dapat diterapkan.
	- Metode 2: ketika klien mengakses nama domain + port koneksi akselerasi, akselerasi dari klien ke server tujuan dapat diterapkan.
	- Metode 3: jika klien asalnya mengakses nama domain, nama domain dapat diselesaikan ke catatan CNAME dari koneksi akselerasi dengan mengonfigurasi CNAME, dan akselerasi dari klien ke server tujuan dapat diterapkan.
2. **Acceleration linkage description** (Deskripsi penautan akselerasi)
   Penautan akselerasi dibagi menjadi beberapa jenis berikut:
	- Klien ke VIP: jaringan publik.
	- VIP ke server penerusan wilayah asal: koneksi langsung (jaringan pribadi).
	- Server penerusan wilayah server asal ke server asal: jaringan publik.
    ![](https://main.qcloudimg.com/raw/263f007ed5775c3a81ad9ba03a2f2cb6.png)
3. **Forwarding server IP description** (Deskripsi IP server penerusan)
Jika aturan grup keamanan diatur untuk server asal, Anda harus mengeklik **ID/Connection Name** (ID/Nama Koneksi) koneksi terlebih dahulu, kueri **Forwarding Server IP** (IP Server Penerusan) pada tab **Connection Information** (Informasi Koneksi), dan izinkan akses ke server asal oleh IP ini untuk mengimplementasikan akselerasi seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/57f70164fc7b34b948a79740d035dfd4.png)
> ?Untuk informasi selengkapnya tentang cara mendapatkan IP klien yang nyata, lihat [Prinsip Dasar](https://intl.cloud.tencent.com/document/product/608/14429) (hanya untuk TCP).
> 
4. **Statistics** (Statistik)
Anda dapat melihat statistik terkini dan riwayat di halaman **Statistics** (Statistik). Untuk petunjuk, lihat [Statistik](https://intl.cloud.tencent.com/document/product/608/14425).
