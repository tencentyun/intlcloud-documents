## Ikhtisar
[Grup keamanan](https://intl.cloud.tencent.com/document/product/213/12452) adalah firewall virtual stateful yang mampu memfilter. Sebagai sarana penting untuk isolasi keamanan jaringan yang disediakan oleh Tencent Cloud, solusi ini dapat digunakan untuk mengatur kontrol akses jaringan untuk satu atau beberapa instans TencentDB. Instans dengan permintaan isolasi keamanan jaringan yang sama di satu wilayah dapat dimasukkan ke dalam grup keamanan yang sama, yang merupakan grup logis. TencentDB dan CVM berbagi daftar grup keamanan dan dicocokkan satu sama lain dalam grup keamanan berdasarkan aturan. Untuk aturan dan batasan khusus, silakan lihat [Ikhtisar Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/38750).

>?
>- Grup keamanan TencentDB for MySQL saat ini hanya mendukung kontrol akses jaringan untuk VPC dan jaringan publik tetapi tidak untuk jaringan klasik.
>- Grup keamanan yang terkait dengan instans TencentDB di wilayah Frankfurt, Silicon Valley, dan Singapura saat ini tidak mendukung kontrol akses jaringan publik.
>- Karena TencentDB tidak memiliki lalu lintas keluar yang aktif, aturan keluar tidak berlaku untuk TencentDB.
>- Grup keamanan didukung untuk instans TencentDB for MySQL sumber, baca saja, dan pemulihan bencana.
>- Grup keamanan tidak didukung untuk instans TencentDB for MySQL node tunggal dasar.


## Mengonfigurasi Grup Keamanan untuk TencentDB
### Langkah 1. Buat grup keamanan
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/securitygroup).
2. Pilih **Security Group** (Grup Keamanan) di bilah sisi kiri, pilih wilayah, dan klik **Create** (Buat).
3. Di jendela dialog pop-up, konfigurasikan item berikut, dan klik **OK** (OKE).
 - **Template** (Templat): pilih templat berdasarkan layanan yang akan di-deploy pada instans TencentDB di grup keamanan, yang menyederhanakan konfigurasi aturan grup keamanan, seperti yang ditunjukkan di bawah ini:
<table>
	<tr><th>Templat</th><th>Deskripsi</th><th>Keterangan</th></tr>
	<tr><td>Buka semua port</td><td>Semua port terbuka. Dapat menimbulkan masalah keamanan.</td><td>-</td></tr>
	<tr><td>Buka port 22, 80, 443, dan 3389 dan protokol ICMP</td><td>Port 22, 80, 443, dan 3389 dan protokol ICMP dibuka ke internet. Semua port dibuka ke jaringan pribadi.</td><td>Templat ini tidak berlaku untuk TencentDB.</td></tr>
	<tr><td>Kustom</td><td>Anda dapat membuat grup keamanan, lalu menambahkan aturan kustom. Untuk petunjuk rinci, silakan lihat "Langkah 2. Tambahkan aturan grup keamanan"</a> di bawah.</td><td>-</rd></tr>
</table>
 - **Name** (Nama): nama grup keamanan.
 - **Project** (Proyek): pilih proyek untuk pengelolaan yang lebih mudah. **DEFAULT PROJECT** (PROYEK DEFAULT) dipilih secara default.
 - **Note** (Catatan): deskripsi singkat tentang grup keamanan untuk pengelolaan yang lebih mudah.


### Langkah 2. Tambahkan aturan grup keamanan
1. Pada halaman [Grup Keamanan](https://console.cloud.tencent.com/cvm/securitygroup), klik **Modify Rule** (Modifikasi Aturan) di kolom **Operation** (Operasi) pada baris grup keamanan yang aturannya akan dikonfigurasi.
2. Di halaman aturan grup keamanan, klik **Inbound rule** (Aturan masuk) > **Add Rule** (Tambahkan Aturan).
3. Di kotak dialog pop-up, tetapkan aturan.
 - **Type** (Jenis): **Custom** (Kustom) dipilih secara default. Anda juga dapat memilih templat aturan sistem lain. MySQL(3306) direkomendasikan.
 - **Source** (Sumber) atau **Target** (Target): sumber lalu lintas (aturan masuk) atau target (aturan keluar). Anda perlu menentukan salah satu opsi berikut:
<table>
	<tr><th>Sumber atau Target</th><th>Deskripsi</th></tr>
	<tr><td>Satu alamat IPv4 atau rentang IPv4</td><td>Dalam notasi CIDR, seperti <code>203.0.113.0</code>, <code>203.0.113.0/24</code> atau <code>0.0.0.0/0</code>, dengan <code>0.0.0.0/0</code> menunjukkan semua alamat IPv4 akan cocok.</td></tr>
	<tr><td>Satu alamat IPv6 atau rentang IPv6</td><td>Dalam notasi CIDR, seperti <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code> atau <code>0::0/0</code>, dengan <code>::/0</code> atau <code>0::0/0</code> menunjukkan semua alamat IPv6 akan dicocokkan.</td></tr>
	<tr><td>ID grup keamanan yang dirujuk. Anda dapat merujuk ID:<ul  style="margin: 0;"><li>Grup keamanan saat ini</li><li>Grup keamanan lainnya</li></ul>
</td><td><ul  style="margin: 0;"><li>Untuk merujuk grup keamanan saat ini, masukkan ID grup keamanan yang terkait dengan CVM.</li><li>Anda juga dapat merujuk grup keamanan lain di wilayah yang sama dan proyek yang sama dengan memasukkan ID grup keamanan.</li></ul>
</td></tr>
	<tr><td>Rujuk objek alamat IP atau objek grup alamat IP dalam <a href="https://intl.cloud.tencent.com/document/product/215/31867">templat parameter</a>.</td><td>-</td></tr>
</table>
 - **Protocol Port** (Port Protokol): masukkan jenis protokol dan rentang port atau rujuk protokol/port atau grup protokol/port dalam [templat parameter](https://intl.cloud.tencent.com/document/product/215/31867).
>!Untuk terhubung ke instans TencentDB for MySQL, portnya harus dibuka. Anda dapat masuk ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans di daftar instans, dan lihat nomor portnya di halaman detail instans.
>![](https://main.qcloudimg.com/raw/9f471c644eb9a5aa86bd092fdebd0255.png)
>
>- TencentDB for MySQL menggunakan port jaringan pribadi 3306 secara default dan mendukung penyesuaian port. Jika port default diubah, port baru harus dibuka di grup keamanan.
>- TencentDB for MySQL menggunakan port jaringan publik 60719 secara default. Setelah akses jaringan publik TencentDB for MySQL diaktifkan, akses tersebut akan dikontrol oleh grup keamanan, sehingga port 60719 dan 3306 harus dibuka.
>- Aturan grup keamanan yang ditampilkan di halaman **Security Group** (Grup Keamanan) di konsol TencentDB for MySQL berlaku untuk alamat jaringan pribadi dan publik (jika diaktifkan) dari instans TencentDB for MySQL.
>
 - **Policy** (Kebijakan): **Allow** (Izinkan) atau **Reject** (Tolak). **Allow** (Izinkan) dipilih secara default.
    - **Allow** (Izinkan): lalu lintas ke port ini diizinkan.
    - **Reject** (Tolak): paket data akan dibuang tanpa respons apa pun.
 - **Note** (Catatan): deskripsi singkat tentang aturan untuk pengelolaan yang lebih mudah.
4. Klik **Complete** (Selesai).

#### Kasus penggunaan
**Scenario:** (Skenario:) Anda telah membuat instans TencentDB for MySQL dan ingin mengaksesnya dari instans CVM.
**Solution:** (Solusi:) saat menambahkan aturan grup keamanan, pilih MySQL(3306) di **Type** (Jenis) untuk membuka port 3306.
Anda juga dapat mengatur **Source** (Sumber) ke semua atau IP tertentu (rentang IP) sesuai kebutuhan agar dapat mengakses TencentDB for MySQL dari instans CVM.

| Masuk atau Keluar | Jenis | Sumber | Protokol dan Port | Kebijakan |
|---------|---------|---------|---------|---------|
| Masuk | MySQL(3306) | Semua IP: 0.0.0.0/0 <br>IP tertentu: tentukan IP atau rentang IP | TCP:3306 | Izinkan |


### Langkah 3. Konfigurasikan grup keamanan
Grup keamanan adalah firewall tingkat instans yang disediakan oleh Tencent Cloud untuk mengontrol lalu lintas masuk TencentDB. Anda dapat mengaitkan grup keamanan dengan instans saat membelinya atau nanti di konsol.

>!Saat ini, grup keamanan hanya dapat dikonfigurasi untuk **TencentDB for MySQL instances in VPC** (instans TencentDB for MySQL di VPC).

1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pada tab **Security Group** (Grup Keamanan), klik **Configure Security Group** (Konfigurasikan Grup Keamanan).
3. Di kotak dialog pop-up, pilih grup keamanan yang akan diikat dan klik **OK** (OKE). 

## Mengimpor Aturan Grup Keamanan
1. Pada halaman [Grup Keamanan](https://console.cloud.tencent.com/cvm/securitygroup), klik ID/nama grup keamanan yang diinginkan.
2. Di tab aturan masuk atau aturan keluar, klik **Import Rule** (Impor Aturan).
3. Di kotak dialog pop-up, pilih file templat aturan masuk/keluar yang telah diedit dan klik **Import** (Impor).
>? Karena aturan yang ada akan ditimpa setelah mengimpor, sebaiknya Anda mengekspor aturan yang ada sebelum mengimpor yang baru.

## Mengkloning Grup Keamanan
1. Pada halaman [Grup Keamanan](https://console.cloud.tencent.com/cvm/securitygroup), cari grup keamanan yang diinginkan dan klik **More** (Lainnya) > **Clone** (Kloning) di kolom **Operation** (Operasi).
2. Di kotak dialog pop-up, pilih wilayah target dan proyek target, masukkan nama grup keamanan baru, dan klik **OK** (OKE). Jika grup keamanan baru perlu dikaitkan dengan instans CVM, lakukan dengan mengelola instans CVM di grup keamanan.

## Menghapus Grup Keamanan
1. Pada halaman [Grup Keamanan](https://console.cloud.tencent.com/cvm/securitygroup), cari grup keamanan yang akan dihapus dan klik **More** (Lainnya) > **Delete** (Hapus) di kolom **Operation** (Operasi).
2. Klik **OK** (OKE) di kotak dialog pop-up. Jika grup keamanan saat ini dikaitkan dengan instans CVM, grup tersebut harus dipisahkan sebelum dapat dihapus.

