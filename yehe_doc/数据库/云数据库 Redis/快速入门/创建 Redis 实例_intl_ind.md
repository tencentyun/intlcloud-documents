
Dokumen ini menjelaskan cara membuat instans di konsol TencentDB for MySQL.

## Prasyarat
Anda telah mendaftarkan akun Tencent Cloud dan menyelesaikan verifikasi identitas.
- Untuk mendaftarkan akun Tencent Cloud:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Klik di sini untuk mendaftar akun Tencent Cloud</a></div>

- Untuk memverifikasi identitas Anda:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Klik di sini untuk memverifikasi identitas Anda</a></div>

## Petunjuk
1. Login ke [halaman pembelian TencentDB for Redis](https://buy.intl.cloud.tencent.com/redis), konfigurasikan informasi instans berikut, konfirmasikan bahwa semuanya sudah benar, dan klik **Buy Now** (Beli Sekarang).
  - **Mode Penagihan**: Bayar sesuai pemakaian.
 - **Wilayah**: Pilih wilayah yang Anda inginkan untuk men-deploy instans TencentDB for Redis Anda. Sebaiknya gunakan wilayah yang sama dengan instans CVM yang akan dihubungkan. Produk Tencent Cloud di wilayah yang berbeda tidak dapat berkomunikasi satu sama lain melalui jaringan pribadi. Wilayah tidak dapat diubah setelah pembelian.
 - **Edisi Instans**: Edisi Memori didukung. Ini adalah edisi performa tinggi berdasarkan mesin Redis sumber terbuka, yang kompatibel dengan Redis v2.8, v4.0, dan v5.0.
 - **Versi yang Kompatibel**: TencentDB for Redis kompatibel dengan Redis v2.8, v4.0, dan v5.0. v2.8 tidak tersedia saat ini, dan disarankan v4.0 atau yang lebih baru. Untuk membeli v2.8, [kirim tiket](https://console.cloud.tencent.com/workorder/category).
 - **Arsitektur**: v4.0 atau lebih tinggi mendukung arsitektur standar dan arsitektur kluster, sedangkan v2.8 hanya mendukung arsitektur standar.
 - **Memori**: Memori opsional dari node tunggal dengan rentang 256 MB hingga 64 GB.
 -**Jumlah Replika**: TencentDB for Redis v2.8 (arsitektur standar) mendukung nol atau satu replika; v4.0 atau v5.0 (arsitektur standar atau kluster) mendukung satu hingga lima replika.
 - **Replika Baca Saja**: v4.0 atau lebih tinggi mendukung replika baca saja.
  - **Jaringan**: Pilih jaringan tempat instans TencentDB for Redis berada. Sebaiknya pilih [VPC](https://intl.cloud.tencent.com/document/product/215) yang sama di wilayah yang sama dengan instans CVM yang akan dihubungkan. Setelah instans TencentDB dibeli, Anda dapat mengalihkan jaringannya dari jaringan klasik ke VPC, tetapi Anda tidak dapat beralih dari VPC ke jaringan klasik.
 - **Zona Ketersediaan**: Pilih zona ketersediaan untuk node master dan node replika. Instans yang di-deploy multi-AZ memiliki ketersediaan yang lebih tinggi dan kemampuan pemulihan bencana yang lebih baik daripada instans yang di-deploy dengan AZ tunggal. Untuk informasi selengkapnya, lihat [Deployment Multi-AZ](https://intl.cloud.tencent.com/document/product/239/39812).
 - **Port**: Port kustom harus berada di antara 1024 hingga 65535.
 - **Templat Parameter**: Terapkan templat parameter untuk mengonfigurasi parameter dalam batch. Untuk informasi selengkapnya, lihat [Menggunakan Templat Parameter](https://intl.cloud.tencent.com/document/product/239/41810).
 - **Proyek** dan **Grup Keamanan**: Tentukan proyek dan [grup keamanan](https://intl.cloud.tencent.com/document/product/239/31945).
 - **Tag**: Anda dapat membuat tag untuk mengelola sumber daya instans.
 - **Grup Keamanan**: Saat membuat instans, Anda dapat memilih grup keamanan yang ada.
 - **Nama Instans** dan **Atur Kata Sandi**: Tetapkan nama dan kata sandi instans di sini atau atur dalam daftar instans setelah pembuatan.
2. Setelah selesai melakukan pembelian, Anda akan dialihkan ke daftar instans. Setelah status replika baca saja ditampilkan sebagai **Berjalan**, instans tersebut dapat digunakan secara normal.
3. (Opsional) Klik ikon **Edit** di kolom **ID/Nama Instans** di daftar instans untuk mengganti nama instans.
![](https://main.qcloudimg.com/raw/8a6917c05adb4e06731dbdd836c620da.png)

## Operasi Berikutnya
- Gunakan instans CVM untuk mengakses IP pribadi instans TencentDB secara langsung. Untuk informasi selengkapnya, lihat [Menghubungkan ke Instans TencentDB for Redis (melalui Jaringan Pribadi)](https://intl.cloud.tencent.com/document/product/239/9897).
- Gunakan instans CVM dengan IP publik untuk terhubung ke instans TencentDB melalui jaringan publik melalui penerusan port. Untuk informasi selengkapnya, lihat [Menghubungkan ke Instans TencentDB for Redis (melalui Jaringan Publik)](https://intl.cloud.tencent.com/document/product/239/35905).
