
Dokumen ini menjelaskan cara mengatur alamat akses proksi database di konsol TencentDB for MySQL.

Alamat akses proksi database tidak tergantung pada alamat akses database asli. Permintaan proksi di alamat proksi semuanya diteruskan melalui kluster proksi untuk mengakses sumber dan node replika database. Pemisahan Baca/Tulis diimplementasikan, sehingga permintaan baca diteruskan ke instans baca saja, yang menurunkan beban database sumber.

## Prasyarat
Anda telah [mengaktifkan proksi database](https://intl.cloud.tencent.com/document/product/236/42052).

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, pilih instans sumber untuk mengaktifkan proksi database dan klik ID-nya atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Database Proxy** (Proksi Database) dan klik ikon <img src="https://main.qcloudimg.com/raw/be716b5360d5256a9d5e816e29872ec1.png"  style="margin:0;"> di samping **Connection Address** (Alamat Koneksi).
![](https://main.qcloudimg.com/raw/63015c402bdd31e04e2597af84013a74.png)
<table>
<thead><tr><th width=15%>Jangka Waktu</th><th>Deskripsi</th></tr></thead>
<tbody><tr>
<td>Alamat proksi database</td>
<td>Ini tidak tergantung pada alamat akses database asli. Permintaan proksi semua disampaikan melalui kluster proksi untuk mengakses sumber dan node replika database. Permintaan ini dapat diedit.</td></tr>
<tr>
<td>Jenis jaringan</td>
<td>Anda dapat mengganti jenis jaringan instans antara jaringan klasik dan VPC sesuai dengan kebutuhan bisnis Anda. <ul><li>Di jaringan klasik, instans tidak dapat diisolasi melalui jaringan tetapi mengandalkan kebijakan daftar yang diizinkan untuk memblokir akses tidak sah. </li><li>VPC adalah lingkungan jaringan yang terisolasi dan memiliki tingkat keamanan yang lebih tinggi.</li></ul></td></tr>
<tr>
<td>Keterangan</td>
<td>Ini adalah deskripsi singkat tentang alamat proksi database untuk pengelolaan yang lebih mudah.</td></tr>
</tbody></table>
3. Di jendela pop-up, modifikasi alamat proksi dan klik **OK** (OKE).
>!Memodifikasi alamat proksi memengaruhi bisnis database yang sedang diakses. Sebaiknya modifikasi alamat selama jam tidak sibuk. Pastikan bisnis Anda memiliki mekanisme koneksi ulang.
>
![](https://main.qcloudimg.com/raw/982fd53d880ab1a6d4f8df0372a99613.png)
