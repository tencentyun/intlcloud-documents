## Ikhtisar
[Grup keamanan](https://intl.cloud.tencent.com/document/product/213/12452) adalah firewall virtual stateful yang mampu memfilter. Sebagai sarana penting untuk isolasi keamanan jaringan yang disediakan oleh Tencent Cloud, solusi ini dapat digunakan untuk mengatur kontrol akses jaringan untuk satu atau beberapa instans TencentDB. Instans dengan permintaan isolasi keamanan jaringan yang sama di satu wilayah dapat dimasukkan ke dalam grup keamanan yang sama, yang merupakan grup logis. TencentDB dan CVM berbagi daftar grup keamanan dan dicocokkan satu sama lain dalam grup keamanan berdasarkan aturan. Untuk aturan khusus dan batas penggunaan, lihat [Ikhtisar Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/38750).

>?
>- Grup keamanan TencentDB for SQL Server saat ini hanya mendukung kontrol akses jaringan untuk VPC dan jaringan publik tetapi tidak untuk jaringan klasik.
>- Grup keamanan yang saat ini mendukung akses jaringan publik hanya tersedia di Guangzhou, Shanghai, Beijing, dan Chengdu.
>- Karena TencentDB tidak memiliki lalu lintas keluar yang aktif, aturan keluar tidak berlaku untuk TencentDB.
>- Grup keamanan TencentDB for SQL Server mendukung instans utama dan replika baca saja.


## Konfigurasi Grup Keamanan untuk TencentDB
### Langkah 1. Buat grup keamanan
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/securitygroup).
2. Pilih **Security Group** (Grup Keamanan) di bilah sisi kiri, pilih wilayah, dan klik **+New** (+Baru).
3. Di kotak dialog pop-up, konfigurasikan item berikut dan klik **OK** (OKE).
 - **Template** (Template): pilih templat berdasarkan layanan yang akan di-deploy pada instans TencentDB di grup keamanan, yang menyederhanakan konfigurasi aturan grup keamanan, seperti yang ditunjukkan di bawah ini:
<table>
	<tr><th>Templat</th><th>Deskripsi</th><th>Keterangan</th></tr>
	<tr><td>Buka semua port</td><td>Semua port terbuka. Dapat menimbulkan masalah keamanan.</td><td>-</td></tr>
	<tr><td>Buka port 22, 80, 443, dan 3389 dan protokol ICMP</td><td>Port 22, 80, 443, dan 3389 dan protokol ICMP dibuka ke internet. Semua port dibuka ke jaringan pribadi.</td><td>Templat ini tidak berlaku untuk TencentDB.</td></tr>
	<tr><td>Kustom</td><td>Anda dapat membuat grup keamanan, lalu menambahkan aturan kustom. Untuk petunjuk rinci, silakan lihat "Langkah 2. Tambahkan aturan grup keamanan"</a> di bawah.</td><td>-</rd></tr>
</table>
 - **Nama**: nama grup keamanan.
 - **Proyek**: secara default, **DEFAULT PROJECT** (PROYEK DEFAULT) dipilih. Pilih proyek untuk manajemen yang lebih mudah.
 - **Catatan**: deskripsi singkat tentang grup keamanan untuk pengelolaan yang lebih mudah.



### Langkah 2. Tambahkan aturan grup keamanan
1. Pada halaman [Grup Keamanan](https://console.cloud.tencent.com/cvm/securitygroup), klik **Modify Rules** (Modifikasi Aturan) di kolom **Operation** (Operasi) pada baris grup keamanan yang aturannya akan dikonfigurasi.
2. Pilih **Security Group Rule** (Aturan Grup Keamanan) > **Inbound rule** (Aturan masuk), klik **Add a Rule** (Tambahkan Aturan).
3. Di kotak dialog pop-up, tetapkan aturan.
 - **Jenis**: **Kustom** dipilih secara default. Anda juga dapat memilih templat aturan sistem lain. SQL Server (1433) direkomendasikan.
 - **Sumber** atau **Target**: sumber lalu lintas (aturan masuk) atau target (aturan keluar). Anda perlu menentukan salah satu opsi berikut:
<table>
	<tr><th>Sumber atau Tujuan</th><th>Deskripsi</th></tr>
	<tr><td>Satu alamat IPv4 atau rentang IPv4</td><td>Dalam notasi CIDR, seperti <code>203.0.113.0</code>, <code>203.0.113.0/24</code> atau <code>0.0.0.0/0</code>, dengan <code>0.0.0.0/0</code> menunjukkan semua alamat IPv4 akan cocok.</td></tr>
	<tr><td>Satu alamat IPv6 atau rentang IPv6</td><td>Dalam notasi CIDR, seperti <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code> atau <code>0::0/0</code>, dengan <code>::/0</code> atau <code>0::0/0</code> menunjukkan semua alamat IPv6 akan dicocokkan.</td></tr>
	<tr><td>ID grup keamanan yang dirujuk. Anda dapat merujuk ID:<ul  style="margin: 0;"><li>Grup keamanan saat ini</li><li>Grup keamanan lainnya</li></ul>
</td><td><ul  style="margin: 0;"><li>Grup keamanan saat ini: CVM yang terkait dengan grup keamanan saat ini.</li><li>Grup keamanan lainnya: ID grup keamanan lain di wilayah yang sama yang berada dalam proyek yang sama.</li></ul>
</td></tr>
	<tr><td>Rujuk objek alamat IP atau objek grup alamat IP dalam <a href="https://intl.cloud.tencent.com/document/product/215/31867">templat parameter</a>.</td><td>-</td></tr>
</table>
 - **Port protokol**: masukkan jenis protokol dan rentang port atau rujuk protokol/port atau grup protokol/port dalam [templat parameter](https://intl.cloud.tencent.com/document/product/215/31867).
  >?Agar terhubung ke TencentDB for SQL Server, port 1433 harus dibuka.
 - **Kebijakan**: **Izinkan** atau **Tolak**. **Izinkan** dipilih secara default.
    - **Izinkan**: lalu lintas ke port ini diizinkan.
    - **Tolak**: paket data akan dibuang tanpa respon apa pun.
 - **Catatan**: deskripsi singkat tentang aturan untuk pengelolaan yang lebih mudah.
4. Klik **Complete** (Selesai).

#### Kasus penggunaan
**Skenario**: Anda telah membuat instans TencentDB for SQL Server dan ingin mengaksesnya dari instans CVM.
**Solusi**: saat menambahkan aturan grup keamanan, pilih **SQL Server(1433)** (SQL Server(1433)) di **Jenis** untuk membuka port 1433.
Anda juga dapat mengizinkan semua IP atau IP yang ditentukan (rentang IP) berdasarkan kebutuhan aktual Anda untuk mengonfigurasi sumber IP yang dapat mengakses TencentDB for SQL Server melalui CVM.

| Petunjuk | Jenis | Sumber | Protokol dan Port | Kebijakan |
|---------|---------|---------|---------|---------|
| Masuk | SQL Server(1433) | Semua IP: 0.0.0.0/0 <br>IP yang Ditentukan: masukkan rentang IP atau IP yang ditentukan | TCP:1433 | Izinkan |


### Langkah 3. Konfigurasikan grup keamanan
Grup keamanan adalah firewall tingkat instans yang disediakan oleh Tencent Cloud untuk mengontrol lalu lintas masuk ke TencentDB. Anda dapat menghubungkan grup keamanan dengan instans saat membelinya atau nanti di konsol.

>!Saat ini, hanya **TencentDB for SQL Server di VPC** yang dapat dihubungkan dengan grup keamanan.

1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, temukan instans untuk mengonfigurasi grup keamanan dan klik **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman manajemen instans.
2. Pada halaman **Security Group** (Grup Keamanan), klik **Configure Security Group** (Konfigurasi Grup Keamanan).
3. Di kotak dialog pop-up, pilih grup keamanan yang akan dihubungkan dan klik **OK** (OKE). 

## Impor Aturan Grup Keamanan
1. Pada halaman [Grup Keamanan](https://console.cloud.tencent.com/cvm/securitygroup), klik ID/nama grup keamanan target.
2. Pada tab **Inbound rule** (Aturan masuk) atau **Outbound rule** (Aturan keluar), klik **Import rule** (Impor aturan).
3. Di kotak dialog pop-up, pilih file templat aturan masuk/keluar yang telah diedit dan klik **Import** (Impor).
>? Jika ada aturan yang ada di grup keamanan, ekspor aturan sebelum mengimpor aturan baru. Aturan yang ada akan ditimpa setelah mengimpor.


## Kloning Grup Keamanan
1. Pada halaman [Grup Keamanan](https://console.cloud.tencent.com/cvm/securitygroup), cari grup keamanan yang diinginkan dan klik **More** (Lainnya) > **Clone** (Kloning) di kolom **Operation** (Operasi).
2. Di kotak dialog pop-up, pilih wilayah dan proyek, masukkan nama baru untuk grup keamanan, dan klik **OK** (OKE). Jika grup keamanan baru perlu dihubungkan dengan instans CVM, klik **Manage Instances** (Kelola Instans) di kolom **Operation** (Operasi) untuk menambahkan instans CVM di tab **Associate with Instance** (Hubungkan dengan Instans) > **Cloud Virtual Machine** (Mesin Virtual Cloud).

## Penghapusan Grup Keamanan
1. Pada halaman [Grup Keamanan](https://console.cloud.tencent.com/cvm/securitygroup), cari grup keamanan yang akan dihapus dan klik **More** (Lainnya) > **Delete** (Hapus) di kolom **Operation** (Operasi).
2. Klik **OK** (OKE) di kotak dialog pop-up. Jika grup keamanan saat ini dihubungkan dengan instans CVM, grup tersebut harus dipisahkan sebelum dapat dihapus.

