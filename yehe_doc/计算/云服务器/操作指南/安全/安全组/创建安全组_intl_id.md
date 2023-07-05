## Skenario
Grup Keamanan bertindak sebagai firewall virtual untuk CVM. Setiap instans CVM harus dikaitkan dengan setidaknya satu grup keamanan. Secara default, setiap instans CVM memiliki dua templat (**Open all ports** (Buka semua port) dan **Open port 22, 80, 443, 3389 and ICMP protocol** (Buka port 22, 80, 443, 3389, dan protokol ICMP)) untuk membuat grup keamanan default. Untuk detailnya, lihat Ikhtisar Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/12452).

Jika grup keamanan default tidak memenuhi kebutuhan Anda, Anda dapat membuat grup keamanan Anda sendiri seperti yang diinstruksikan di bawah ini.


## Petunjuk

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Di bilah sisi kiri, pilih **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)** ([Grup Keamanan]). Halaman Grup Keamanan kemudian akan muncul.
3. Pilih wilayah untuk grup keamanan. Klik **+New** (+Baru). 
4. Di halaman **Create a security group** (Buat grup keamanan), selesaikan konfigurasi berikut:
![](https://main.qcloudimg.com/raw/575b2a589a58aef436bc5208facf4614.png)
 - **Template** (Templat): pilih templat yang sesuai dengan kebutuhan Anda, seperti yang ditampilkan di bawah ini:
<table>
	<tr><th>Templat</th><th>Deskripsi</th><th>Catatan</th></tr>
	<tr><td>Buka semua port</td><td>Semua port terbuka. Dapat menimbulkan masalah keamanan.</td><td>-</td></tr>
	<tr><td>Buka port TCP 22，80，443，3389, dan ICMP</td><td>Port TCP 22, 80, 443, dan 3389, dan ICMP terbuka. Semua port terbuka secara internal.</td><td>Cocok untuk instans dengan layanan web.</td></tr>
	<tr><td>Kustom</td><td>Membuat grup keamanan kosong yang aturannya ditambahkan setelahnya. Untuk detail tentang cara menambahkan aturan, lihat <a href="https://intl.cloud.tencent.com/document/product/213/34272">artikel ini</a>.</td><td>-</rd></tr>
</table>
 - **Name** (Nama): nama grup keamanan.
 - **Project** (Proyek): secara default, **Deafult project** (Proyek default) dipilih. Pilih proyek untuk manajemen yang lebih baik.
 - **Notes** (Catatan): deskripsi singkat untuk grup keamanan.
5. Klik **OK** (OKE) untuk membuat grup keamanan.
Jika Anda memilih **Custom** (Kustom) sebagai templat untuk grup keamanan Anda, klik **Add rules now** (Tambahkan aturan sekarang) untuk [menambahkan aturan grup keamanan](https://intl.cloud.tencent.com/document/product/213/34272).
