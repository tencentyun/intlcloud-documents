Setelah instans TencentDB for MySQL dibuat, instans tersebut berada dalam status **Uninitialized** (Belum Diinisialisasi) dan perlu diinisialisasi sebelum dapat digunakan.

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), pilih wilayah target, pilih instans dalam status **Uninitialized** (Belum Diinisialisasi) dalam daftar instans, dan klik **Initialize** (Inisialisasi) di kolom **Operation** (Operasi).
2. Di jendela pop-up inisialisasi, konfigurasikan parameter inisialisasi dan klik **OK** (OKE).
 - **Character Set** (Kumpulan Karakter): Set karakter LATIN1, GBK, UTF8, dan UTF8MB4 didukung. Nilai defaultnya adalah UTF8. Setelah menginisialisasi instans, Anda dapat mengubah kumpulan karakter pada halaman detail instans di konsol. Untuk informasi selengkapnya, lihat [Batas Penggunaan > Catatan tentang kumpulan karakter](https://intl.cloud.tencent.com/document/product/236/7259).
 - **Table Name Case Sensitivity** (Sensitivitas Huruf Besar-Kecil Nama Tabel): apakah nama tabel peka huruf besar/kecil. Nilai defaultnya adalah ya.
 - **Custom Port** (Port Kustom): port akses database, yaitu 3306 secara default.
 - **Root Account Password** (Kata Sandi Akun Root): mengatur kata sandi akun root (nama pengguna default untuk database MySQL baru adalah "root").
 - **Confirm Password** (Konfirmasi Kata Sandi): masukkan kembali kata sandi.
3. Di jendela pop-up inisialisasi, klik **OK** (OKE).
![](https://qcloudimg.tencent-cloud.cn/raw/cd8d4f83c43cc23b23c50c2e85773473.png)
4. Kembali ke daftar instans. Setelah status instans berubah menjadi **Running** (Berjalan), instans dapat digunakan secara normal.

## Operasi Selanjutnya
Anda dapat mengakses instans TencentDB for MySQL melalui jaringan pribadi dan publik dari instans CVM Windows atau Linux. Untuk informasi selengkapnya, lihat [Menghubungkan ke Instans MySQL](https://intl.cloud.tencent.com/document/product/236/37788).
