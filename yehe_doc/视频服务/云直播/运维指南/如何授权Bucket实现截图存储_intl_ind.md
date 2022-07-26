Dokumen ini menjelaskan cara menyimpan data tangkapan layar atau deteksi pornografi di bucket COS. Anda perlu membuat bucket COS, mengizinkan CSS untuk menyimpan data di dalamnya, lalu mengonfigurasikan pengaturan pengambilan tangkapan layar dan deteksi pornografi langsung di konsol CSS. Setelah itu, data tangkapan layar dan deteksi pornografi dapat disimpan di bucket. (Fitur ini tersedia di konsol versi baru.)
### Membuat bucket COS
1. Login ke Konsol COS, lalu pilih [Bucket List (Daftar Bucket)](https://console.cloud.tencent.com/cos5/bucket).
2. Klik **Create Bucket** (Buat Bucket), masukkan informasi yang sesuai di halaman pop-up, lalu klik **OK** (Oke).
 ![](https://main.qcloudimg.com/raw/423beefad19658e0cec8cdd28d6d25e1.png)
>!
> - Bucket akan diberi nama "examplebucket" (tidak termasuk nomor di sebelah kanan).
> - Informasi di atas dapat dikonfigurasikan sesuai dengan kebutuhan aktual bisnis Anda.
3. Anda dapat mengaktifkan akselerasi CDN untuk bucket COS sesuai dengan kebutuhan. Klik nama bucket atau **Configuration Management** (Manajemen Konfigurasi) untuk masuk ke halaman detail. Pilih **Domain and transmission management** -> **Default CDN Acceleration Domain** (Manajemen domain dan transmisi -> Domain Akselerasi CDN Default) di sebelah kiri, lalu klik **Edit** untuk mengaktifkan **Status** dan menyelesaikan konfigurasi lainnya. Klik **Save** (Simpan) untuk mengaktifkan akselerasi CDN. Informasi selengkapnya tentang konfigurasi dapat dilihat di [Enabling Default CDN Acceleration Domain Names (Mengaktifkan Nama Domain Akselerasi CDN Default)](https://intl.cloud.tencent.com/zh/document/product/436/31505).
![](https://main.qcloudimg.com/raw/097144cf7c6d1df5923d406b0301f93e.png)

### Mengizinkan CSS Menyimpan Tangkapan Layar
1. Berikan izin ke akun root (ID: 3508645126) untuk menyimpan tangkapan layar.

	i. Tambahkan pengguna untuk bucket di **[Bucket List](https://console.cloud.tencent.com/cos5/bucket)** > **Permission Management** > **Bucket Access Permission** (Daftar Bucket > Manajemen Izin > Izin Akses Bucket), pilih akun root sebagai jenis pengguna, **lalu masukkan ID akun root `3508645126`**
	> **Anda perlu memasukkan ID akun root `3508645126` di bidang ID akun untuk otorisasi. (Akun root ini merupakan layanan CSS sehingga memasukkan `3508645126` langsung sudah cukup).**
	![](https://main.qcloudimg.com/raw/37362cc7a0b945e79899e24f84f33dab.png)
	
	ii. Informasi selengkapnya tentang API pengaturan izin akses bucket dapat dilihat di [PUT Bucket acl (acl Bucket PUT)](https://intl.cloud.tencent.com/document/product/436/7737).
2. Dapatkan informasi bucket COS yang telah mendapatkan izin.
	(1) Anda dapat melihat semua informasi COS di bagian **Basic Configuration** (Konfigurasi Dasar) di bucket. Nama domain akses (yaitu nama domain server asal) berisi nama bucket, appid cos, dan wilayah bucket.
	![](https://main.qcloudimg.com/raw/b84d288cf37b40ed548ca4a25863742a.png)
	 - nama bucket: examplebucket
	 - appid cos: 125****900
	 - wilayah bucket: ap-chengdu
	(2) Setelah 3 bidang di atas dikirim, sistem akan menyimpan tangkapan layar CSS di bucket COS yang telah mendapatkan izin.
