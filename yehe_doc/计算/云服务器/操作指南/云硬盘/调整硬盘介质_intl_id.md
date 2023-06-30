
## Ikhtisar
Tencent Cloud CVM mendukung penyesuaian media perangkat keras penyimpanan, yang memungkinkan Anda merespons secara fleksibel kebutuhan penyimpanan yang beragam dari berbagai bisnis.
Tencent Cloud menyediakan dua jenis media penyimpanan: [Cloud Block Storage](https://intl.cloud.tencent.com/document/product/213/4953) dan [Local Storage atau Penyimpanan Lokal](https://intl.cloud.tencent.com/document/product/ 213/5798). Disk lokal dapat dikonversi ke disk cloud. Dokumen ini menjelaskan cara mengubah jenis media disk.
Kelemahan CVM dengan disk lokal adalah sebagai berikut:
- Konfigurasi tidak dapat disesuaikan karena keterbatasan sumber daya host.
- Fitur seperti snapshot dan akselerasi pembuatan tidak didukung.
- Keandalan data rendah.
- Kegagalan host akan berdampak lebih lama.

Untuk menghindari kerugian ini, Anda dapat mengonversi disk lokal yang terpasang ke CVM Anda ke disk cloud.

<span id="LocalDiskPrecondition"></span>
## Prasyarat
- **CVM Status** (Status CVM)
 Pastikan CVM terkait dinonaktifkan.
- **Unsupported CVM Types** (Jenis CVM yang Tidak Didukung)
 - Instans spot
 - Big data dan model I/O tinggi 
 - Instans bare metal
- **CVM Configuration** (Konfigurasi CVM)
 - Setidaknya salah satu disk sistem dan disk data CVM harus **HDD** (HDD) atau **SSD local disk** (disk lokal SSD).
 - Tersedia disk cloud yang ukurannya sesuai dengan disk lokal di zona ketersediaan tempat CVM berada.
 - Penyesuaian akan mengonversi **all** (semua) disk lokal ke disk cloud jika disk sistem dan disk data CVM adalah disk lokal. Anda juga dapat mengonfigurasi jenis disk cloud untuk setiap disk secara terpisah.
 Dengan kata lain, perubahan media disk dari CVM yang disk-nya adalah semua disk lokal berlaku untuk semua disk-nya, bukan hanya disk sistem atau disk data.
 - Mengubah media cloud disk tidak akan mengubah ukuran disk. Anda dapat [memperluas disk cloud](https://intl.cloud.tencent.com/document/product/362/5747) setelah mengubah jenis media.
 - Operasi ini tidak akan mengubah siklus pemakaian CVM, ID instans, IP pribadi/publik, nama disk, dan titik pemasangan.

<span id="LocalDiskNotice"></span>
## Catatan

- Konversi ini perlu menyalin semua data dari disk lokal ke disk cloud. Tergantung pada ukuran disk dan kecepatan transmisi, proses ini bisa memakan waktu.
- Anda hanya dapat mengonversi disk lokal ke disk cloud. Konversi TIDAK DAPAT dikembalikan.
- **After the adjustment, we recommend you to start up and log in to the CVM to check the data integrity** (Setelah penyesuaian, sebaiknya mulai dan login ke CVM untuk memeriksa integritas data).

## Petunjuk
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm) dan akses halaman **Instances* (Instans).
>? Jika CVM telah dinonaktifkan, lanjutkan ke [Langkah 3](#step3).
2. (Opsional) Cari CVM target, lalu klik **More** (Lainnya) > **Instance Status** (Status Instans) > **Shutdown** (Nonaktifkan) di bawah kolom **Operation** (Operasi) untuk menonaktifkannya.
<span id="step3"></span>
3. Di bawah kolom **Operation** (Operasi), klik **More** (Lainnya) > **Resource Adjustment** (Penyesuaian Sumber Daya) > **Change Disk Media Type** (Ubah Jenis Media Disk).
4. Di jendela pop-up, pilih jenis disk cloud target, centang **I have read and agreed to Rules for Changing Disk Media Type** (Saya telah membaca dan menyetujui Aturan untuk Mengubah Jenis Media Disk), lalu klik **Change Now** (Ubah Sekarang).
5. Periksa kembali informasinya, lakukan pembayaran jika berlaku, dan tunggu hingga prosesnya selesai.
 
