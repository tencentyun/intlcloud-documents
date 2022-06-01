Pesan SMS lengkap terdiri dari **tanda tangan SMS** dan **isi SMS**. Anda dapat memilih jenis template isi sesuai kebutuhan bisnis Anda, lalu menggabungkan tanda tangan dan isi ke dalam konten SMS akhir: `[Tanda tangan SMS] Isi SMS`.
Tanda tangan SMS atau template yang telah dikirim biasanya akan ditinjau dalam waktu dua jam. Jam peninjauan: Senin–Minggu, 9:00–23:00 (jadwal dapat berubah jika terdapat hari libur nasional). Anda dapat mencantumkan nomor ponsel dan alamat email untuk menerima pemberitahuan hasil tinjauan.

<span id="Template"></span>
## Membuat Template Isi
1. Login ke [SMS Console (Konsol SMS)](https://console.cloud.tencent.com/smsv2).
2. Pilih **Chinese Mainland SMS** > **Body Templates** (SMS Tiongkok Daratan > Template Isi) di bilah sisi kiri dan klik **Create Body Template** (Buat Template Isi).
4. Atur parameter berikut sesuai kebutuhan dan sesuai dengan [standar tinjauan template isi]:
 - Template Name (Nama Template): nama template untuk memudahkan identifikasi.
 - SMS Type (Jenis SMS): jenis SMS yang akan dikirim dengan template isi ini. Pengguna perusahaan dapat memilih **Regular SMS** (SMS Biasa) atau **Marketing SMS** (SMS Pemasaran), sementara pengguna individu hanya dapat memilih **Regular SMS** (SMS Biasa).
 - SMS Content (Konten SMS): konten isi SMS dengan kurang dari 500 karakter. Konten kustom dapat dikonfigurasi, tetapi tidak boleh hanya berisi variabel. Variabel memiliki format `{number}` dan angkanya harus berurutan. SMS Pemasaran harus berisi opsi untuk berhenti berlangganan, seperti `Balas dengan T untuk berhenti berlangganan`.
 - Remarks (Catatan): Anda dapat memasukkan skenario pengiriman dan penerima di sini, yang bersifat opsional.
5. Klik **OK**.
 Menunggu tinjauan template isi. Template isi hanya akan tersedia setelah statusnya berubah menjadi **approved** (disetujui).


## Memodifikasi Template Isi
>Modifikasi hanya dapat dilakukan jika status template isi adalah **pending review** (menunggu tinjauan) atau **rejected** (ditolak). Template isi dengan status **Approved** (Disetujui) tidak dapat dimodifikasi.

1. Pada halaman [Template Isi](https://console.cloud.tencent.com/smsv2/csms-template), Anda dapat melihat informasi template isi.
 - ID: ID template isi yang secara otomatis dihasilkan oleh sistem. ID template isi yang disetujui dapat ditetapkan sebagai nilai parameter `tpl_id` saat mengirim SMS melalui API atau SDK.
 - Content (Konten): konten sebenarnya dari isi SMS.
 - Status/Reason (Status/Alasan): status template isi, yang meliputi **pending review** (menunggu tinjauan), **rejected** (ditolak), dan **approved** (disetujui). Jika status template isi adalah **rejected** (ditolak), Anda dapat mengeklik **View Failure Reason and Modify** (Lihat Alasan Kegagalan dan Modifikasi) untuk melihat alasan atau saran mendetail.
 - Time Applied (Waktu Pengajuan): waktu saat template isi dibuat.
2. Klik **Edit** pada baris template isi dengan status **pending review** (menunggu tinjauan) atau **rejected** (ditolak), modifikasi informasinya, lalu klik **OK** untuk mengirimkannya agar ditinjau kembali.


## Menghapus Template Isi
Anda dapat menghapus template isi yang tidak lagi dibutuhkan. **Setelah dihapus, template isi tidak dapat dipulihkan secara langsung; sebagai gantinya, Anda harus mengirimkan aplikasi baru untuk ditinjau; oleh karena itu, lakukan langkah ini dengan hati-hati.**

1. Pada halaman [Template Isi](https://console.cloud.tencent.com/smsv2/csms-template), klik **Delete** (Hapus) pada baris template isi target.
2. Pada kotak dialog yang muncul, klik **Delete** (Hapus).

## Informasi Terkait

- Proses tinjauan
- Standar tinjauan template isi
- Sampel template isi
- [Pertanyaan Umum tentang template isi](https://intl.cloud.tencent.com/document/product/382/13301)
