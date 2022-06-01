Pesan SMS lengkap terdiri dari **tanda tangan SMS** dan **isi SMS**. Anda dapat memilih jenis template isi sesuai kebutuhan bisnis Anda, lalu menggabungkan tanda tangan dan isi ke dalam konten SMS akhir: `[Tanda tangan SMS] Isi SMS`.
Tanda tangan SMS yang telah dikirim biasanya akan ditinjau dalam waktu dua jam. Jam peninjauan: Senin–Minggu, 9:00–23:00 (jadwal dapat berubah jika terdapat hari libur nasional). Anda dapat mencantumkan nomor ponsel dan alamat email untuk menerima pemberitahuan hasil tinjauan.



## Membuat Tanda Tangan

1. Login ke [SMS Console (Konsol SMS)](https://console.cloud.tencent.com/smsv2).

2. Pilih **Chinese Mainland SMS** > **Signatures** (SMS Tiongkok Daratan > Tanda Tangan) di bilah sisi kiri dan klik **Create Signature** (Buat Tanda Tangan).

3. Pertimbangkan kebutuhan Anda yang sebenarnya dan

    

   standar tinjauan tanda tangan

    

   untuk mengatur parameter berikut:

   - Signature Type (Jenis Tanda Tangan): jenis tanda tangan SMS.
     Pengguna organisasi dapat memilih **Company** (Perusahaan), **App** (Aplikasi), **Website** (Situs Web), **Official Account/Mini Program** (Akun Resmi/Proram Mini), **Trademark** (Merek dagang), atau **Government/public institution/other** (Pemerintah/lembaga publik/lainnya).
     Pengguna individu dapat memilih **App** (Aplikasi), **Website** (Situs Web), atau **Official Account/Mini Program** (Akun Resmi/Program Mini).
   - Signature Purpose (Tujuan Tanda Tangan): tujuan tanda tangan SMS. Anda dapat memilih **For verified entities** (Untuk entitas yang terverifikasi) (seperti organisasi, situs web, atau nama produk dengan tanda tangan yang diverifikasi oleh akun) atau **For unverified entities** (Untuk entitas yang tidak terverifikasi) (seperti organisasi, situs web, atau nama produk dengan tanda tangan yang tidak diverifikasi oleh akun).
   - Signature Content (Konten Tanda Tangan): konten sebenarnya dari tanda tangan SMS. Tidak perlu memasukkan [], seperti `Tencent Cloud`.
   - Certificate Type (Jenis Sertifikat): jenis sertifikat kualifikasi dan identitas yang digunakan untuk mengajukan tanda tangan SMS.
   - Certificate Upload (Unggahan Sertifikat): unggah foto atau pindaian sertifikat terkait sesuai dengan **Certificate Type** (Jenis Sertifikat) yang dipilih. Format gambar yang didukung adalah .jpg atau .png dengan ukuran kurang dari 5 MB.
   - Authorization (Otorisasi): parameter ini hanya muncul jika **Signature Purpose** (Tujuan Tanda Tangan) diatur ke "For unverified entities" (Untuk entitas yang tidak terverifikasi).
     i. Unduh dan isi [surat otorisasi](https://sms-1258344699.cos.ap-guangzhou.myqcloud.com/Declaration%20of%20Authorisation%20(SMS%20Signature).docx). Dalam surat ini, pihak yang diotorisasi harus diisi dengan nama lengkap individu/organisasi yang diverifikasi di bawah akun Tencent Cloud saat ini dan pihak yang memberi otorisasi harus diisi dengan nama lengkap entitas tempat tanda tangan tersebut berasal.
     ii. Tempelkan stempel resmi pihak pemberi otorisasi pada surat otorisasi.
     iii. Unggah foto atau pindaian surat otorisasi yang dicap dengan stempel resmi pihak pemberi otorisasi. Format gambar yang didukung adalah .jpg atau .png dengan ukuran kurang dari 5 MB.
   - Catatan: saat mengajukan tanda tangan jenis **app** (aplikasi), **website** (situs web), atau **WeChat Official Account or WeChat Mini Program** (Akun Resmi WeChat atau Program Mini WeChat), Anda harus memasukkan informasi sesuai dengan Standar Tinjauan Tanda Tangan. Parameter ini opsional untuk aplikasi tanda tangan jenis lain.

4. Klik **OK**.
   Menunggu tinjauan tanda tangan. Tanda tangan SMS hanya akan tersedia setelah statusnya berubah menjadi **approved** (disetujui).

## Memodifikasi Tanda Tangan


>!
> Modifikasi hanya dapat dilakukan jika status tanda tangan adalah **pending review** (menunggu tinjauan) atau **rejected** (ditolak). Tanda tangan dengan status **Approved** (Disetujui) tidak dapat dimodifikasi.

1. Pada halaman

    

   Tanda Tangan

    

   Anda dapat melihat informasi tanda tangan.

   - ID: ID tanda tangan yang secara otomatis dihasilkan oleh sistem.
   - Content (Konten): konten sebenarnya dari tanda tangan SMS. Konten tanda tangan yang disetujui dapat ditetapkan sebagai nilai parameter `sign` saat mengirim SMS melalui API atau SDK. Jika parameter ini tidak ditentukan, konten tanda tangan pertama yang disetujui akan digunakan secara default.
   - Status/Reason (Status/Alasan): status tanda tangan, yang meliputi **pending review** (menunggu tinjauan), **rejected** (ditolak), dan **approved** (disetujui). Jika status tanda tangan adalah **rejected** (ditolak), Anda dapat mengeklik **View Failure Reason and Modify** (Lihat Alasan Kegagalan dan Modifikasi) untuk melihat alasan atau saran mendetail.
   - Time Applied (Waktu Pengajuan): waktu saat tanda tangan dibuat.

2. Klik **Edit** pada baris tanda tangan dengan status **pending review** (menunggu tinjauan) atau **rejected** (ditolak), modifikasi informasinya, lalu klik **Confirm** (Konfirmasi) untuk mengirimkannya agar ditinjau kembali.

## Menghapus Tanda Tangan

Anda dapat menghapus tanda tangan yang tidak lagi dibutuhkan. **Setelah dihapus, tanda tangan tidak dapat dipulihkan secara langsung; sebagai gantinya, Anda harus mengirimkan aplikasi baru untuk ditinjau; oleh karena itu, lakukan langkah ini dengan hati-hati.**

1. Pada halaman [Tanda Tangan](https://console.cloud.tencent.com/smsv2/csms-sign), klik **Delete** (Hapus) pada baris tanda tangan target.
2. Pada kotak dialog yang muncul, klik **Delete** (Hapus).
