
Anda dapat membuat, melihat, dan menghentikan instans baca saja di konsol TencentDB for SQL Server.

>?Instans Baca Saja tidak dapat dibeli dan digunakan secara terpisah; sebagai gantinya, mereka harus terikat ke instans utama (Edisi Ketersediaan Tinggi Server Ganda atau Edisi Kluster).

## Batasan Fitur
- Maksimal 3 instans baca saja dapat dibuat untuk instans utama.
- Saat ini, instans baca saja tidak didukung untuk Edisi Standar.
- Saat ini, instans baca saja tidak dapat ditambahkan ke instans di zona keuangan.
- Instans Baca Saja tidak mendukung pencadangan dan pengembalian.
- Data tidak dapat dimigrasikan ke instans baca saja.
- Instans Baca Saja tidak mendukung pembuatan/penghapusan database. Jika diperlukan, silakan operasikan pada instans utama.
- Instans Baca Saja tidak mendukung pembuatan/penghapusan/otorisasi akun dan perubahan nama/kata sandi akun. Jika diperlukan, silakan operasikan pada instans utama.


## Membuat Instans Baca Saja
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail.
2. Klik **Add Read-Only Instance** (Tambahkan Instans Baca Saja) di **Instance Architecture Diagram** (Diagram Arsitektur Instans) pada halaman detail instans atau klik **Create** (Buat) pada halaman **Read-Only Instance** (Instans Baca Saja) untuk masuk ke halaman pembelian.
![](https://qcloudimg.tencent-cloud.cn/raw/9f46d9d3fe5a77819b68d9fe1081813f.png)
3. Di halaman pembelian yang ditampilkan, tentukan konfigurasi instans baca saja berikut, konfirmasikan bahwa semuanya sudah benar, dan klik **Buy Now** (Beli Sekarang).
>?Jika Anda perlu menyatukan waktu kedaluwarsa dari instans utama dan baca saja, Anda dapat mengatur tanggal kedaluwarsa kolektif di [konsol Manajemen Perpanjangan]](https://console.cloud.tencent.com/account/renewal).
>
![](https://qcloudimg.tencent-cloud.cn/raw/407fa77c69d571162dc711299f8d91c8.png)


## Melihat Instans Baca Saja
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, instans dengan bendera **R** (R) adalah instans baca saja. Klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail instans baca saja.
2. Pada **Instance Architecture Diagram** (Diagram Arsitektur Instans) di halaman detail instans, Anda dapat melihat informasi instans utama yang terikat. Anda dapat mengeklik ID instans untuk masuk ke halaman detail instans utama. Anda juga dapat masuk ke halaman detail instans baca saja dari **Instance Architecture Diagram** (Diagram Arsitektur Instans) dari instans utama.
>?Beberapa fitur di halaman detail instans baca saja tidak dapat diubah dan disinkronkan dari instans utama. Jika Anda perlu mengubahnya, lakukan di halaman detail instans utama.
>
![](https://qcloudimg.tencent-cloud.cn/raw/b5f90a8f7c0ad4e1de69af51cbdfd107.png)


## Menghentikan Instans Baca Saja
Instans baca saja dapat dihentikan dengan cara yang sama seperti instans utama seperti yang diinstruksikan di [Menghentikan Instans](https://intl.cloud.tencent.com/document/product/238/35787).
