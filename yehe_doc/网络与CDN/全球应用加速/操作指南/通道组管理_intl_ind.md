## Menambahkan Grup Koneksi
Untuk akselerasi di beberapa wilayah dengan konfigurasi server asal dan pendengar yang sama, Anda dapat menambahkan grup koneksi untuk mengelola koneksi dalam batch agar beban kerja Anda berkurang.

1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap), masuk ke halaman **Connection Group Management** (Manajemen Grup Koneksi), lalu klik **Add** (Tambahkan).
2. Di jendela pop-up, masukkan informasi grup koneksi.
![](https://main.qcloudimg.com/raw/8422f414d9053317e531e7df56eb524b.png)
	- **Project** (Proyek): proyek tempat grup koneksi berada, yang dapat diubah.
	- **Connection Group Name** (Nama Grup Koneksi): terdiri dari maksimum 30 karakter.
	- **IP Version** (Versi IP): mendukung IPv4 atau IPv6. IPv6 hanya didukung untuk wilayah di Tiongkok Daratan.
	- **Acceleration Region** (Wilayah Akselerasi): wilayah tempat klien berada atau wilayah yang paling dekat dengan lokasi klien. Anda dapat memilih lebih dari satu wilayah akselerasi.
	<blockquote class="d-mod-notice">
                   <div class="d-mod-title d-explain-title">
                       <i class="d-icon-notice"></i>Catatan:
                   </div>
      <p>Jaringan BGP khusus hanya didukung di Hong Kong, Tiongkok. Jika Anda membutuhkannya, kirim tiket untuk menghubungi kami.</p>
               </blockquote>
	- **Origin Region** (Wilayah Asal): wilayah tempat server tujuan berada atau wilayah yang paling dekat dengan lokasi server tujuan.
	<blockquote class="d-mod-notice">
                   <div class="d-mod-title d-explain-title">
                       <i class="d-icon-notice"></i>Catatan:
                   </div>
      <p>Server asal di Taiwan, Tiongkok tidak dapat mengakses wilayah akselerasi di Tiongkok Daratan, dan sebaliknya.</p>
               </blockquote>
	- **Connection Specification** (Spesifikasi Koneksi): mendukung pengaturan batas bandwidth koneksi dan jumlah maksimum koneksi bersamaan.
	- **Bandwidth Cap** (Batas Bandwidth): bandwidth maksimum suatu koneksi, yaitu 10.000 Mbps (1.000 Mbps untuk beberapa koneksi).
	- **Maximum Concurrent Connections** (Koneksi Bersamaan Maksimum): jumlah maksimum koneksi bersamaan untuk sebuah koneksi, yaitu 1 juta (300.000 untuk beberapa koneksi).
	
   	<blockquote class="d-mod-notice">
   	            <div class="d-mod-title d-explain-title">
   	                <i class="d-icon-notice"></i>Catatan:
   	            </div>
      <p>Satu grup koneksi dapat berisi hingga 20 koneksi.</p>
	            </blockquote>
	- **Tag**: mendukung klasifikasi koneksi. Item ini opsional.
	- **Fees** (Biaya): biaya untuk koneksi dan bandwidth dihitung berdasarkan bandwidth dan koneksi bersamaan yang Anda tentukan. Biaya koneksi dihitung per hari sampai koneksi dihapus, sedangkan bandwidth dikenai biaya berdasarkan batas bandwidth masuk dan keluar harian aktual.
3. Klik **OK** (Oke).
4. Di halaman [Manajemen Grup Koneksi](https://console.cloud.tencent.com/gaap/group), Anda dapat melihat detail grup koneksi, mengelola koneksi dalam grup koneksi yang sama, dan memantau statusnya secara real time.
![](https://main.qcloudimg.com/raw/ffe0e9059a8852996af10d34a6fb5e90.png)
	- **ID/Connection Group Name** (ID/Nama Grup Koneksi): ID dan nama grup koneksi. Nama grup koneksi dapat diubah.
	- **VIP**: Alamat IP yang diakses oleh klien.
	- **Domain Name** (Nama Domain): nama domain yang diakses oleh klien, yang ditetapkan oleh sistem dan secara otomatis terikat ke VIP.
	- **Status**: koneksi akselerasi dapat bekerja secara normal hanya dalam status **Running** (Berjalan).

## Melihat Informasi Grup Koneksi
1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap), masuk ke halaman **Connection Group Management** (Manajemen Grup Koneksi), lalu klik **ID/Connection Group Name** (ID/Nama Grup Koneksi) salah satu grup koneksi.
 ![](https://main.qcloudimg.com/raw/f30309e39fd75c32a55ce084342f828d.png)
2. Di tab **Connection group info** (Info grup koneksi), Anda dapat melihat detail koneksi. **Forwarding Server IP** (IP Server Penerusan) adalah IP node penerusan di akhir koneksi akselerasi. Node penerusan ini meneruskan data koneksi akselerasi ke server asal melalui jaringan publik. Jika Anda ingin beberapa koneksi menggunakan nama domain yang sama, klik **Unified Domain Name** (Nama Domain Terpadu) untuk membuka [konfigurasi](https://console.cloud.tencent.com/gaap/domain). Anda juga dapat mengatur konfigurasi nama domain terpadu secara terpisah untuk koneksi yang ada di grup koneksi yang sama.
 ![](https://main.qcloudimg.com/raw/708e37323d8d0a4892c11aea052c6bce.png)


## Mengelola Pendengar TCP/UDP
## Menambahkan pendengar TCP/UDP
Untuk informasi selengkapnya, lihat [Manajemen Akses](https://cloud.tencent.com/document/product/608/13764#.E6.96.B0.E5.A2.9Etcp.2Fudp-.E7.9B.91.E5.90.AC.E5.99.A8).

### Mengonfigurasi pendengar TCP/UDP
Untuk informasi selengkapnya, lihat [Manajemen Akses](https://cloud.tencent.com/document/product/608/13764#.E8.AE.BE.E7.BD.AEtcp.2Fudp-.E7.9B.91.E5.90.AC.E5.99.A8).

## Mengelola Pendengar HTTP/HTTPS

### Menambahkan pendengar HTTP/HTTPS
Untuk informasi selengkapnya, lihat [Manajemen Akses](https://cloud.tencent.com/document/product/608/17539#.E6.96.B0.E5.A2.9Ehttp.2Fhttps-.E7.9B.91.E5.90.AC.E5.99.A8).

### Mengonfigurasi pendengar HTTP/HTTPS
Untuk informasi selengkapnya, lihat [Manajemen Akses](https://cloud.tencent.com/document/product/608/17539#.E8.AE.BE.E7.BD.AEhttp.2Fhttps-.E7.9B.91.E5.90.AC.E5.99.A8).

## Perlindungan Keamanan
Untuk informasi selengkapnya, lihat [Manajemen Akses](https://intl.cloud.tencent.com/document/product/608/42338).
