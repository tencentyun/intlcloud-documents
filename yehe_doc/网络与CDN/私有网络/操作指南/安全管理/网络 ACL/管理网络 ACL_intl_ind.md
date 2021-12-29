## Membuat ACL Jaringan
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Security** (Keamanan) -> **Network ACL** (ACL Jaringan) di direktori sebelah kiri untuk membuka halaman manajemen.
3. Pilih wilayah dan VPC di bagian atas daftar dan klik **+New** (+Baru).
4. Masukkan namanya di jendela pop-up, pilih VPC miliknya, dan klik **OK** (Oke).
![](https://main.qcloudimg.com/raw/3e5444cc57b2da457c2cd9db221dd1d3.png)
5. Pada halaman daftar, klik ID ACL yang sesuai untuk membuka halaman detailnya, tempat Anda dapat menambahkan aturan ACL dan menghubungkan aturan ACL dengan subnet.

## Menambahkan Aturan ACL Jaringan
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Klik **Security** (Keamanan) -> **Network ACL** (ACL Jaringan) di direktori sebelah kiri untuk membuka halaman manajemen.
3. Lihat di daftar untuk jaringan ACL yang akan dimodifikasi, dan klik ID-nya untuk membuka halaman detail.
4. Untuk menambahkan aturan keluar/masuk, klik **Outbound Rules** (Aturan Keluar) atau **Inbound Rules** (Aturan Masuk) -> **Edit** -> **New Line** (Baris Baru), pilih jenis protokol, masukkan port dan alamat IP sumber, dan pilih kebijakan.
 - Jenis protokol: menunjukkan jenis protokol yang diizinkan atau ditolak oleh aturan ACL, misalnya, TCP dan UDP.
 - Port: menunjukkan port sumber lalu lintas yang dapat berupa port tunggal atau segmen port, misalnya port 80 atau port 90 hingga 100.
 - Alamat IP sumber: menunjukkan alamat IP sumber atau rentang IP lalu lintas yang mendukung rentang IP atau blok CIDR, misalnya, `10.20.3.0` atau `10.0.0.2/24`.
 - Kebijakan: mengizinkan atau menolak permintaan akses.
![](https://main.qcloudimg.com/raw/d6d87cc117b15f5125d7f7fbb327f845.png)
5. Klik **Save** (Simpan).

## Menghapus Aturan ACL Jaringan
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Klik **Security** (Keamanan) -> **Network ACL** (ACL Jaringan) di direktori sebelah kiri untuk membuka halaman manajemen.
3. Lihat daftar ACL jaringan yang akan dihapus, dan klik ID-nya untuk membuka halaman **Basic Information** (Informasi Dasar).
4. Klik tab **Inbound Rules** (Aturan Masuk) atau tab **Outbound Rules** (Aturan Keluar) untuk membuka halaman **Rules List** (Daftar Aturan).
5. Klik **Edit** (Edit). Proses untuk menghapus aturan masuk sama dengan menghapus aturan keluar. Penghapusan aturan masuk digunakan sebagai contoh di sini.
![](https://main.qcloudimg.com/raw/2d3a16b59a2566a2bfd6226086b3528b.png)
6. Dalam daftar, pilih baris aturan yang akan dihapus dan klik **Delete** (Hapus) di kolom operasi.
>? Aturan ACL ini kini berwarna abu-abu. Jika Anda tidak sengaja menghapusnya, Anda dapat mengeklik **Recover the deleted rule** (Pulihkan aturan yang dihapus) di kolom operasi untuk memulihkan aturan.
>
![](https://main.qcloudimg.com/raw/57389cf8420513b893c5f55747826247.png)
7. Klik **Save** (Simpan) untuk menyimpan operasi sebelumnya.
>! Penghapusan atau pemulihan aturan ACL hanya berlaku setelah Anda menyimpan operasi.

## Menghubungkan ACL Jaringan ke Subnet
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Klik **Security** (Keamanan) -> **Network ACL** (ACL Jaringan) di direktori sebelah kiri untuk membuka halaman manajemen.
3. Lihat daftar untuk jaringan ACL yang akan dihubungkan, dan klik ID-nya untuk membuka halaman detail.
4. Pada halaman **Basic Information** (Informasi Dasar), klik **Add Association** (Tambahkan Hubungan) di modul **Associated Subnets** (Subnet Terhubung).
![](https://main.qcloudimg.com/raw/60374f034ac84bc088b42f1b2811af93.png)
5. Pilih subnet yang akan dihubungkan dari jendela pop-up dan klik **OK** (Oke).
![2](https://main.qcloudimg.com/raw/dd1c974c4938aa5bfd13ebbba2fa3274.png)

## Memutus Hubungan ACL Jaringan dari Subnet
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Klik **Security** (Keamanan) -> **Network ACL** (ACL Jaringan) di direktori sebelah kiri untuk membuka halaman manajemen.
3. Lihat daftar untuk jaringan ACL yang akan diputus hubungannya, dan klik ID-nya untuk membuka halaman detail.
4. Ada beberapa metode berbeda untuk memutus hubungan ACL dari subnet:
 - Metode 1: cari subnet yang akan diputus hubungannya di modul **Associated Subnets** (Subnet Terhubung) pada halaman **Basic Information** (Informasi Dasar) dan klik **Disassociate** (Putus Hubungan).
![1](https://main.qcloudimg.com/raw/f5049453bb9838e03e093461232e5c82.png)
 - Metode 2: beri tanda centang di sebelah subnet yang akan diputus hubungannya dalam modul **Associated Subnets** (Subnet Terhubung) pada halaman **Basic Information** (Informasi Dasar), dan klik **Batch Disassociate** (Putus Hubungan Batch).
![2](https://main.qcloudimg.com/raw/e2953af15a89f4476e033e08e67009e5.png)
5. Klik **OK** (Oke) di jendela pop-up.
![3](https://main.qcloudimg.com/raw/e44731b65300f164200946b10b2d8be6.png)

## Menghapus ACL Jaringan
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Klik **Security** (Keamanan) -> **Network ACL** (ACL Jaringan) di direktori sebelah kiri untuk membuka halaman manajemen.
3. Pilih wilayah dan VPC.
4. Dalam daftar, cari ACL jaringan yang akan dihapus, klik **Delete** (Hapus), lalu konfirmasi penghapusan. ACL jaringan dan semua aturannya akan dihapus.
>? Jika opsi **Delete** (Hapus) berwarna abu-abu, seperti untuk jaringan ACL `testEg` pada gambar berikut, ini menunjukkan bahwa ACL jaringan saat ini terhubung ke subnet. Anda harus memutus hubungannya dari subnet terlebih dahulu sebelum dapat menghapusnya.

![](https://main.qcloudimg.com/raw/3d6113a44321ce73e35f99efc246bfb4.png)

