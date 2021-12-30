## Skenario Operasi
Grup keamanan adalah firewall virtual untuk instans CVM. Setiap instans CVM harus dimasukkan dengan setidaknya satu grup keamanan. Tencent Cloud menyediakan dua templat: **Open all ports to the Internet** (Buka semua port ke internet) dan **Open ports 22, 80, 443, and 3389 and ICMP protocol to the Internet** (Buka port 22, 80, 443, dan 3389 serta protokol ICMP ke internet). Dengan templat ini, Anda dapat membuat grup keamanan default saat membuat instans CVM jika belum membuat grup keamanan. 

Jika tidak ingin instans CVM bergabung dengan grup keamanan default, Anda dapat membuat grup keamanan lain di konsol CVM sebagai berikut:


## Langkah
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm).
2. Di bilah sisi kiri, klik **[Security Group] (https://console.cloud.tencent.com/cvm/securitygroup)** (Grup Keamanan) untuk masuk ke halaman manajemen grup keamanan.
3. Pada halaman manajemen grup keamanan, pilih **Region** (Wilayah) dan klik **+Create** (+Buat).
4. Pada jendela **Create a security group** (Buat grup keamanan) yang muncul, selesaikan konfigurasi seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/dc265c99d23e7a05bb9cc8b72f2cebee.png)
 - Templat: berdasarkan layanan yang akan di-deploy untuk instans CVM di grup keamanan, pilih templat yang sesuai untuk menyederhanakan konfigurasi aturan grup keamanan seperti yang dijelaskan dalam tabel berikut:
<table>
	<tr><th>Templat</th><th>Deskripsi</th><th>Skenario</th></tr>
	<tr><td>Buka semua port ke internet</td><td>Secara default, semua port akan dibuka ke internet dan jaringan pribadi yang kemudian dapat menimbulkan risiko keamanan.</td><td>-</td></tr>
	<tr><td>Buka port 22, 80, 443, dan 3389 dan protokol ICMP ke internet</td><td>Secara default, port 22, 80, 443, dan 3389 dan protokol ICMP akan dibuka ke internet. Selain itu, semua port akan dibuka ke jaringan pribadi.</td><td>Layanan web perlu di-deploy untuk instans dalam grup keamanan.</td></tr>
	<tr><td>Kustom</td><td>Setelah membuat grup keamanan, Anda dapat menambahkan aturan grup keamanan sesuai kebutuhan. Untuk detail tentang operasi, lihat <a href="https://intl.cloud.tencent.com/document/product/215/35513">Menambahkan Aturan Grup Keamanan</a>.</td><td>-</rd></tr>
</table>
 - Nama: menyesuaikan nama grup keamanan.
 - Proyek: secara default, **Default project** (Proyek default) dipilih. Anda juga dapat menentukan proyek lain untuk memfasilitasi manajemen di masa mendatang.
 - Keterangan: jelaskan grup keamanan secara singkat untuk memfasilitasi manajemen di masa mendatang.
5. Klik **OK** (Oke) untuk menyelesaikan pembuatan grup keamanan.
Jika Anda memilih templat **Custom** (Kustom) saat membuat grup keamanan, klik **Set rules now** (Tetapkan aturan sekarang) setelah pembuatan ke [tambahkan aturan grup keamanan](https://intl.cloud.tencent.com/document/product/215/35513).
