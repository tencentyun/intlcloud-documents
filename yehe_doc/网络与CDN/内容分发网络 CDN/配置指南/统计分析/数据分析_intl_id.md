Anda dapat memeriksa distribusi pengguna akhir dan penggunaan sumber daya di halaman **Data Analysis** (Analisis Data). Namun, ECDN tidak mendukung menampilkan jumlah permintaan akses IP unik dan distribusi wilayah akses pengguna akhir saat ini.


Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn) dan pilih **Statistics** (Statistik) > **Data Analysis** (Analisis Data) di bilah samping kiri untuk masuk ke halaman **Data Analysis** (Analisis Data).

- Anda dapat mengueri data yang dihasilkan dalam periode waktu maksimum 31 hari. Data riwayat disimpan selama 90 hari.
- Anda dapat mengueri data riwayat yang dihasilkan dalam tiga bulan terakhir.

>! ECDN tidak mendukung menampilkan jumlah permintaan akses IP unik dan distribusi wilayah akses pengguna akhir saat ini.


## Permintaan Akses IP Unik
Jumlah permintaan akses IP unik dalam periode waktu yang ditentukan dihitung dengan menghapus duplikat IP klien akses di log:
<li>Jika rentang waktu kurang dari atau sama dengan satu hari, kurva IP yang duplikatnya dihapus dengan perincian 5 menit akan diberikan.</li>
<li>Statistik nama domain dihitung dengan menghapus duplikat jumlah yang aktif dalam sehari penuh. Jika ada beberapa nama domain, proyek, atau akun, statistik dihitung dengan mengakumulasi jumlah aktif harian tiap domain dengan perincian 5 menit.</li>
<img src="https://main.qcloudimg.com/raw/bed86e21420fe337d6b0587090fe4b64.png" alt>


## Distribusi Distrik Akses Pengguna
Distrik pemohon akses dapat diidentifikasi melalui IP klien sumber, yang dapat ditampilkan dalam peta atau daftar, memungkinkan Anda untuk melihat distribusi distrik pengguna Anda.
![](https://main.qcloudimg.com/raw/d89e4321c94499833d04841c7e5e3597.png)

## Distribusi ISP Pengguna
ISP pemohon akses dapat diidentifikasi melalui IP klien sumber, yang dapat ditampilkan dalam diagram lingkaran atau daftar, memungkinkan Anda untuk melihat distribusi ISP pengguna Anda.
![](https://main.qcloudimg.com/raw/b6fa25e2fb72dbcd02e11fae43e888ed.png)
