Setelah Anda menambahkan nama domain di konsol CSS, sistem akan secara otomatis menetapkan nama domain CNAME (berakhiran `.tlivecdn.com`) untuk nama domain tersebut, yang dapat dilihat di **[Domain Management (Manajemen Domain)](https://console.cloud.tencent.com/live/domainmanage)**. Nama domain tersebut tidak dapat diakses jika Anda belum menyelesaikan konfigurasi CNAME di penyedia layanan DNS Anda. Setelah konfigurasi diterapkan, Anda dapat menggunakan layanan CSS.

## Catatan
- Resolusi CNAME diperlukan untuk nama domain pemutaran ulang dan nama domain push.
- Silakan konfigurasikan rekaman CNAME di penyedia layanan DNS Anda. Untuk mendapatkan petunjuk mendetail, silakan hubungi penyedia layanan Anda.
>- Konfigurasi CNAME akan diterapkan dalam waktu sekitar 15 menit. Jika Anda mengatur beberapa lapisan CNAME, CSS tidak dapat memantau hasil resolusi secara efektif. Konfigurasi CNAME berhasil jika nama domain CNAME dapat diakses.
- Jika konfigurasi CNAME gagal diterapkan setelah waktu yang lama, lihat [Domain Configuration (Konfigurasi Domain)](https://intl.cloud.tencent.com/document/product/267/32478).

## Prasyarat
- Anda telah mengajukan permohonan nama domain di [Tencent Cloud Domains (Domain Tencent Cloud)](https://dnspod.cloud.tencent.com/?from=qcloudProductDns).
- Anda berhasil [menambahkan nama domain](https://intl.cloud.tencent.com/document/product/267/35970) di halaman **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) di konsol CSS, dan status alamat CNAME nama domain tersebut adalah ![](https://main.qcloudimg.com/raw/ed1ac2f8541f629814a3f2420b1eb79c.png) (CNAME not configured (CNAME tidak dikonfigurasi)).



## Petunjuk
Dokumen ini menjelaskan cara melakukan konfigurasi rekaman CNAME di Tencent Cloud, Alibaba Cloud, Baidu AI Cloud, DNSPod, Wanwang, dan Xinnet. Petunjuk di bawah ini hanya untuk referensi Anda. Harap ikuti petunjuk yang diberikan penyedia layanan DNS Anda. Setelah mengonfigurasi nama domain CNAME, Anda dapat memverifikasi penerapan konfigurasi CNAME seperti yang diinstruksikan di [Verifying Whether CNAME Takes Effect (Memverifikasi Penerapan CNAME)](#check).


[](id:tencent)
### Tencent Cloud
Jika penyedia layanan DNS Anda adalah Tencent Cloud, gunakan langkah-langkah berikut untuk menambahkan rekaman CNAME:

1. Login ke [konsol Layanan Nama Domain Tencent Cloud](https://console.cloud.tencent.com/domain).
2. Temukan nama domain target, lalu klik **Resolve** (Selesaikan).
3. Di halaman DNS yang ditampilkan untuk nama domain, klik **Add Record** (Tambahkan Rekaman).
4. Atur parameter berikut untuk rekaman CNAME:
<table>
    <tr><th width="12%" >Parameter</th><th width="38%">Deskripsi</th><th width="50%">Konfigurasi</th></tr>
    <tr>
    <td>Host Record (Rekaman Host)</td>
        <td>Awalan nama subdomain</td>
        <td>
            <ul style="margin-bottom:0;">
                <li>Jika nama domain adalah <code>play.myqcloud.com</code>, silakan pilih: <code>play (putar)</code></li>
                <li>Untuk menyelesaikan nama domain utama <code>myqloud.com</code>, silakan pilih: <code>@</code></li>
                <li>Untuk menyelesaikan nama domain wildcard, silakan pilih: <code>\*</code></li>
            </ul>
        </td>
    </tr>
    <tr>
    <td>Record Type (Jenis Rekaman)</td>
        <td>Record type (Jenis rekaman)</td>
        <td>Untuk mengarahkan nama domain ke nama domain lain, silakan pilih: <b>CNAME</b></td>
    </tr>
    <tr>
        <td>Line Type (Jenis Saluran)</td>
        <td>Digunakan oleh server DNS untuk menyelesaikan nama domain ke alamat IP server yang sesuai berdasarkan sumber pengunjung </td>
        <td>Silakan pilih: <b>Default</b></td>
    </tr>
    <tr>
        <td>Record Value (Nilai Rekaman)</td>
        <td>Nama domain yang akan dituju. Masukkan nilai CNAME yang sesuai untuk nama domain yang diperoleh di halaman **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>** (Manajemen Domain) di konsol Tencent Cloud.</td>
        <td>Buka halaman **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>** (Manajemen Domain), temukan nama domain tanpa konfigurasi CNAME, salin dan masukkan di **Record Value** (Nilai Rekaman) dalam format: <ul style="margin:0">
            <li/><code><b style="color:red;">xxxx</b>.tlivecdn.com</code>
            <li/><code><b style="color:red;">xxxx</b>.tlivepush.com</code>
            </ul></td>
    </tr>
    <tr>
        <td>TTL (Waktu untuk Aktif)</td>
        <td>Waktu untuk aktif cache, yaitu <b>600s (600 detik)</b> secara default</td>
        <td>Anda sebaiknya mengaturnya ke <b>600s (600 detik)</b>.</td>
    </tr>
</table>
5. Klik **Save** (Simpan) untuk menyelesaikan konfigurasi CNAME.

>!  Rekaman dengan jenis berbeda memiliki prioritas berbeda. Untuk host yang sama, beberapa jenis rekaman tidak dapat digunakan bersamaan. Jenis CNAME tidak sesuai dengan jenis rekaman lainnya. Anda harus menghapus rekaman jenis lain agar rekaman CNAME dapat ditambahkan.

[](id:ali)
### Alibaba Cloud
Jika penyedia layanan DNS Anda adalah Alibaba Cloud, gunakan langkah-langkah berikut untuk menambahkan rekaman CNAME:

1. Login ke konsol Alibaba Cloud, lalu buka **Alibaba Cloud DNS** > **[Manage DNS](https://dns.console.aliyun.com/#/dns/domainList)** (Kelola DNS).
2. Klik nama domain tempat Anda akan menambahkan rekaman CNAME untuk membuka halaman **DNS Settings** (Pengaturan DNS).
3. Klik **Add Record** (Tambahkan Rekaman) dan atur sebagai berikut:
  - Type (Jenis): pilih `CNAME`.
  - Host: masukkan awalan nama subdomain; misalnya, jika nama domain pemutaran ulang adalah `play.myqcloud.com`, masukkan `play`; jika Anda ingin langsung menyelesaikan nama domain utama `myqloud.com`, masukkan `@`; dan jika Anda ingin menyelesaikan nama domain wildcard, masukkan `\*`.
  - ISP Line (Saluran ISP): Anda disarankan untuk memilih `Default`.
  - Value (Nilai): masukkan CNAME nama domain di halaman manajemen nama domain di konsol Tencent Cloud, dalam format `domain.tlivecdn.com`.
  - TTL (Waktu untuk Aktif): Anda disarankan untuk memilih 10 menit.
4. Klik **OK** (OKE).


[](id:baidu)
### Baidu AI Cloud
Jika penyedia layanan DNS Anda adalah Baidu AI Cloud, gunakan langkah-langkah berikut untuk menambahkan rekaman CNAME:
1. Login ke konsol Baidu AI Cloud dan buka [Domain Name System (Sistem Nama Domain)](https://console.bce.baidu.com/bcd/?_=1550137564099#/bcd/manage/list).
2. Pilih nama domain yang ditambahkan ke CSS dan klik **Resolve** (Selesaikan) di kolom **Operation** (Operasi) untuk masuk ke halaman DNS seperti ditunjukkan di bawah ini:
3. Tambahkan rekaman DNS dan atur sebagai berikut:
 - CVM server record (Rekaman server CVM): masukkan nama domain tingkat kedua, yaitu awalan nama domain; misalnya, jika nama domain pemutaran ulang adalah `play.myqcloud.com`, masukkan `play`; jika Anda ingin langsung menyelesaikan nama domain utama `myqloud.com`, masukkan `@`; dan jika Anda ingin menyelesaikan nama domain wildcard, masukkan `\*`.
 - Record type (Jenis rekaman): pilih `CNAME record` (rekaman CNAME).
 - Resolution line (Saluran resolusi): Anda sebaiknya memilih `Default`.
 - Record value (Nilai rekaman): masukkan nilai CNAME yang diperoleh di halaman manajemen nama domain di konsol CSS, dalam format `domain.tlivecdn.com`.
 - TTL (Waktu untuk Aktif): Anda disarankan untuk memilih 10 menit.
4. Klik **OK** (OKE) untuk mengirim.


[](id:dnspod)
### DNSPod
Jika penyedia layanan DNS Anda adalah DNSPod, gunakan langkah-langkah berikut untuk menambahkan rekaman CNAME:
1. Login ke [konsol DNSPod](https://console.dnspod.cn/dns/list).
2. Klik nama domain target di daftar untuk masuk ke halaman "Add Record" (Tambahkan Rekaman).
3. Tambahkan rekaman CNAME melalui langkah berikut:
  1. Masukkan nama subdomain untuk rekaman host. Misalnya, jika Anda ingin menyelesaikan `www.123.com`, Anda hanya perlu memasukkan `www` sebagai rekaman host; jika Anda ingin menyelesaikan `123.com`, Anda dapat mengosongkan rekaman host dan sistem akan secara otomatis memasukkan `@`. Rekaman CNAME dengan `@` akan memengaruhi resolusi rekaman MX.
  2. Pilih **CNAME** sebagai jenis rekaman.
  3. Atur jenis bagi zona (secara default harus diisi; jika dibiarkan kosong, permintaan beberapa pengguna mungkin tidak dapat diselesaikan. Dalam gambar di bawah, nilai default berarti bahwa semua pengguna, kecuali pengguna China Unicom, akan diarahkan ke `1.com `).
  4. Atur nilai rekaman ke nama domain yang ditunjukkan oleh resolusi CNAME. Hanya nama domain yang dapat dimasukkan. Setelah rekaman dibuat, biasanya tanda "." akan secara otomatis ditambahkan setelah nama domain.
  5. Prioritas MX tidak diperlukan.
  6. TTL (Waktu untuk Aktif) adalah periode cache untuk rekaman. Makin kecil nilainya, makin cepat rekaman yang dimodifikasi diterapkan secara global. Jika Anda mengosongkannya, nilai akan diatur ke 600 detik secara default.



[](id:wwwnet)
### Wanwang
Jika penyedia layanan DNS Anda adalah Wanwang, gunakan langkah-langkah berikut untuk menambahkan rekaman CNAME:

1. Login ke Wanwang Member Center.
2. Di bilah sisi kiri, klik **Product Management** > **My Cloud Resolution** (Manajemen Produk > Resolusi Cloud Saya) untuk masuk ke halaman daftar resolusi cloud.
3. Klik nama domain yang akan diselesaikan untuk masuk ke halaman rekaman resolusi.
4. Di halaman rekaman resolusi, klik **Add Resolution** (Tambahkan Resolusi) untuk mengatur rekaman resolusi.
5. Untuk mengatur rekaman CNAME, pilih CNAME sebagai jenis rekaman. Masukkan rekaman host (misalnya `www`) sesuai kebutuhan, yang merupakan awalan nama domain. Masukkan nama domain yang ditunjukkan oleh nama domain saat ini sebagai nilai rekaman. Jangan ubah pengaturan default untuk saluran resolusi dan TTL.
6. Setelah menyelesaikan pengaturan, klik **Save** (Simpan).


[](id:xinnet)
### Xinnet
Jika penyedia layanan DNS Anda adalah Xinnet, tambahkan rekaman CNAME dengan **mengatur alias (rekaman CNAME)**.
Rekaman alias memungkinkan Anda untuk memetakan beberapa nama ke komputer yang sama dan umumnya digunakan untuk komputer yang menyediakan layanan www dan email. Misalnya, komputer bernama `host.mydomain.com` (sebuah rekaman) menyediakan layanan www dan email. Untuk memudahkan akses pengguna, Anda dapat mengatur dua alias (rekaman CNAME) yang dimulai dengan `www` dan `mail` untuk komputer ini.


[](id:check)
## Memverifikasi Efek Rekaman CNAME
Waktu yang dibutuhkan agar rekaman CNAME diterapkan berbeda-beda, bergantung pada penyedia layanan DNS. Umumnya, rekaman CNAME aktif dalam waktu setengah jam. Anda juga dapat memeriksa telah diterapkan atau belumnya rekaman CNAME menggunakan cara berikut:
- **Metode 1:** buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) di konsol CSS, dan periksa status CNAME yang diakhiri dengan `.myqcloud.com` sudah berubah menjadi ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png) atau belum. Konfigurasi CNAME berhasil jika status sudah berubah.
![](https://main.qcloudimg.com/raw/7930331f6eb7f4271014083cab27fb26.png)
- **Metode 2**: di Linux/macOS, jalankan perintah `dig` dalam format `dig your own domain name` (telusuri nama domain Anda). Jika baris pertama menampilkan bahwa nama domain tujuan yang disediakan oleh CSS telah diselesaikan, konfigurasi CNAME berhasil. 
![](https://main.qcloudimg.com/raw/2cbe7fdc1c9d7dbed7851aa86dd64ff1.png)
- **Metode 3**: di Windows, klik **Start** > **Run** (Mulai > Jalankan), masukkan `cmd`, tekan Enter (Masuk), lalu masukkan `nslookup your own domain name` (jalankan nslookup pada nama domain Anda) di baris perintah. Jika nama domain tujuan yang disediakan oleh CSS diselesaikan, konfigurasi CNAME berhasil.
![](https://main.qcloudimg.com/raw/765ac099e7c79a70496563f00cdab9a7.png)


>!Jika konfigurasi CNAME gagal diterapkan setelah waktu yang lama, lihat [Domain Configuration (Konfigurasi Domain)](https://intl.cloud.tencent.com/document/product/267/32478).
