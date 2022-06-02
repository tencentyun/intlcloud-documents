## Ikhtisar
Anda dapat mengonfigurasi pengiriman email di konsol SES. Dokumen ini menjelaskan cara mengirim email.

## Petunjuk
### Pengiriman Email
1. Login ke [konsol SES](https://console.cloud.tencent.com/ses/send) dan klik **Pengiriman Email** untuk membuka halaman **Pengiriman Email**.
![](https://main.qcloudimg.com/raw/3797c2f860e240f4e4864728aa09c80a.png)
2. Pilih templat email, masukkan subjek, pilih alamat pengirim, masukkan alamat penerima, dan klik **Send** (Kirim) untuk mengirim email.
>? Halaman ini hanya untuk menguji pengiriman email. Diizinkan hingga 20 alamat penerima untuk satu pengujian.

### Batch
1. Di konsol, Anda melihat daftar tugas pengiriman di halaman **Email Sending** (Pengiriman Email) > **Batch** (Batch). Daftar tugas pengiriman menampilkan informasi mendetail dari setiap tugas pengiriman, termasuk **Sending Progress** (Progres Pengiriman), **Task Type** (Jenis Tugas), **Task Status** (Status Tugas), dan **Requests** (Permintaan).
![](https://qcloudimg.tencent-cloud.cn/raw/03e8a8f74f5d0ab785bb016427712502.png)
2. Klik **Create Sending Task** (Buat Tugas Pengiriman), pilih **Batch** (Batch) untuk **Task Type** (Jenis Tugas), dan atur semua bidang wajib untuk tugas guna mengirim email dalam batch.
![](https://qcloudimg.tencent-cloud.cn/raw/bd85315b7f512173a687f6c0ea4f706c.png)

### Dijadwalkan
1. Di konsol, buka halaman **Email Sending** (Pengiriman Email) > **Batch** (Batch), klik **Create Sending Task** (Buat Tugas Pengiriman) dan pilih **Scheduled** (Dijadwalkan).
![](https://qcloudimg.tencent-cloud.cn/raw/7e4f2dcdca1e2f11ba55e7d03861489e.png)
2. Pilih **Start Time** (Waktu Mulai) untuk tugas dan email akan dikirim secara otomatis pada waktu yang ditentukan.
![](https://qcloudimg.tencent-cloud.cn/raw/55482b11771bbe336023ca840d346234.png)


### Berulang
1. Di konsol, buka halaman **Email Sending** (Pengiriman Email) > **Batch** (Batch), klik **Create Sending Task** (Buat Tugas Pengiriman) dan pilih **Recurring** (Berulang).
![](https://qcloudimg.tencent-cloud.cn/raw/972566ee846e6629d9518f67686cec99.png)
2. Tetapkan bidang tugas termasuk **Start Time** (Waktu Mulai) dan **Recurrence** (Pengulangan). Konsol akan secara otomatis mengirim email berdasarkan pengulangan yang ditentukan.
![](https://qcloudimg.tencent-cloud.cn/raw/e5ca62b26bbbfc467855d04d4e9c088e.png)

>?
>
>- Fitur **Batch** (Batch) di konsol cocok untuk pengiriman batch email pemasaran atau pemberitahuan. Untuk mengirim email berbasis pemicu (seperti autentikasi dan email transaksional), sebaiknya panggil API `SendEmail`.
>- Warm-up otomatis dibangun dalam fitur pengiriman batch untuk secara cerdas menentukan reputasi domain/IP pengirim dan jumlah maksimum email terkirim yang diizinkan per hari. Ketika batas harian ini tercapai, pengiriman email akan berhenti dan email tambahan akan masuk ke antrean cache dan dikirim dalam waktu 24 jam kemudian. Untuk batas email harian untuk domain/IP yang belum di-warm-up, lihat [Rencana Warm-up Standar](https://intl.cloud.tencent.com/document/product/1084/43285#default).
>- Anda dapat menggunakan satu domain untuk beberapa tugas pengiriman. Ketika total volume email melebihi jumlah maksimum yang diizinkan per hari, email tambahan akan masuk ke antrean cache dan dikirim pada hari berikutnya.
>- Saat tugas memasuki antrean cache, statusnya adalah **Paused** (Dijeda) dan bilah kemajuan pengiriman tetap statis. Setelah Anda memulai ulang tugas pada hari berikutnya, statusnya menjadi **Sending** (Mengirim) dan bilah kemajuan bertambah.
