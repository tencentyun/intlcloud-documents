## Ikhtisar
Selain menggunakan citra publik Tencent Cloud, Anda dapat membuat citra kustom untuk membuat dengan cepat instans Tencent Cloud CVM dengan konfigurasi yang sama.
>?
>- Citra menggunakan layanan snapshot CBS untuk penyimpanan data. Saat Anda membuat citra kustom, snapshot akan dibuat secara otomatis dan dikaitkan dengan citra tersebut. Anda akan dikenakan biaya untuk snapshot ini. Untuk informasi selengkapnya, lihat [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/362/32415).
>- Untuk CVM yang dibuat berdasarkan citra publik setelah Juli 2018 dan menggunakan disk cloud sebagai disk sistem, Anda dapat membuat citra tanpa menonaktifkan instans. Untuk CVM lain, Anda harus mematikan instans sebelum membuat citra kustom untuk memastikan bahwa citra memiliki lingkungan deployment yang sama dengan instans saat ini.


## Catatan

- Setiap wilayah mendukung maksimal 10 citra kustom.
- Direktori dan file berikut akan dihapus.
 - `/var/log/`  
 - `/root/.bash_history` dan `/home/ubuntu/.bash_history` (untuk sistem operasi Ubuntu)
- Saat membuat citra kustom pada instans Linux, pastikan `/etc/fstab` tidak berisi konfigurasi disk data. Jika tidak, instans yang dibuat dengan citra ini tidak dapat dimulai secara normal. Jika instans Linux yang digunakan untuk membuat citra kustom memiliki disk data yang terpasang, beri komentar atau hapus konfigurasi disk data yang relevan di `/etc/fstab`.
- Proses pembuatan memakan waktu sepuluh menit atau lebih, tergantung pada ukuran data instans. Harap persiapkan terlebih dahulu untuk menghindari dampak bisnis.

## Petunjuk

### Membuat citra kustom dari instans melalui konsol

1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm).
2. Pada halaman manajemen instans, pilih instans untuk citra yang akan dibuat, lalu klik **More** (Lainnya) > **Instance Status** (Status Instans) > **Shut down** (Nonaktifkan), seperti yang ditunjukkan di bawah ini:
![Nonaktifkan](https://main.qcloudimg.com/raw/cc0bb1c82b96cca94cb7c1c011b664a7.png)
3. Setelah instans dinonaktifkan, klik **More** (Lainnya)> **Create Image** (Buat Citra), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/8e3fc28e1a0b1e9e337ff72e34a9fd01.png)
4. Di jendela pop-up, masukkan **Image Name** (Nama Citra) dan **Description** (Deskripsi), lalu klik **Create Image** (Buat Citra).
>? Anda dapat mengklik <img src="https://main.qcloudimg.com/raw/31b31c7b27848f0378932f17273feff3.png" style="margin: 0;"></img> di sudut kanan atas untuk melihat kemajuan pembuatan citra.
>
5. Setelah citra dibuat, klik **[Images](https://console.cloud.tencent.com/cvm/image)** [Citra] di bilah sisi kiri untuk masuk ke halaman manajemen citra.
6. Dalam daftar citra, pilih citra yang telah Anda buat, lalu klik **Create an Instance** (Buat Instans) untuk membeli server dengan konfigurasi yang sama seperti citra.
![Citra Kustom](https://main.qcloudimg.com/raw/2d64df77d16b3c26d275770e03a1caf1.png)

### Membuat citra kustom melalui API

Anda dapat menggunakan `CreateImage` API untuk membuat citra kustom. Untuk informasi selengkapnya, lihat [CreateImage](https://intl.cloud.tencent.com/document/product/213/33276).

## Praktik Terbaik

### Memigrasikan data pada disk data

Jika Anda perlu menyimpan data pada disk data instans asli saat meluncurkan instans baru, Anda dapat mengambil [snapshot](https://intl.cloud.tencent.com/document/product/362/31638) disk data terlebih dahulu, lalu menggunakan snapshot ini untuk membuat data cloud baru disk.
Untuk informasi selengkapnya, lihat [Membuat Disk Cloud Menggunakan Snapshot](https://intl.cloud.tencent.com/document/product/362/5757).