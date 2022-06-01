### Apa yang harus saya lakukan jika pengajuan tanda tangan saya ditolak?

Anda harus memberikan sertifikat kualifikasi yang sesuai untuk mengajukan tanda tangan SMS. Silakan masukkan konten tanda tangan lagi, lalu unggah sertifikat yang sesuai dan asli berdasarkan [Signature Review Standards (Standar Peninjauan Tanda Tangan)](https://intl.cloud.tencent.com/document/product/382/40658).

### Mengapa pengajuan ditolak dengan alasan "non-identifiable signatures" (tanda tangan tidak dapat diidentifikasi)?

Tanda tangan yang tidak dapat diidentifikasi adalah tanda tangan yang tidak dapat mengidentifikasi identitas organisasi atau individu terkait. Misalnya, Anda tidak dapat menggunakan `test`, `aabb`, `verification code` (kode verifikasi), atau `notification` (pemberitahuan) sebagai tanda tangan. Kami menyarankan Anda untuk menggunakan nama organisasi atau aplikasi Anda sebagai tanda tangan. Untuk informasi selengkapnya, lihat [Signature Review Standards (Standar Peninjauan Tanda Tangan)](https://intl.cloud.tencent.com/document/product/382/40658).

### Apakah ada batasan untuk jumlah tanda tangan SMS?
Anda dapat mengajukan hingga 50 tanda tangan SMS. Untuk mengajukan beberapa tanda tangan, Anda harus menyertakan sertifikat kualifikasi yang sesuai untuk setiap tanda tangan.

### Apakah saya dapat mengubah tanda tangan SMS?
Tanda tangan yang telah disetujui tidak dapat diubah. Anda dapat membuat beberapa tanda tangan dan memilih tanda tangan yang sesuai saat mengirim pesan.

### Bagaimana cara mengajukan tanda tangan untuk produk yang masih dalam uji beta dan belum dapat dirilis?
Jika produk Anda belum dirilis, silakan gunakan nama organisasi Anda untuk mengajukan tanda tangan untuk pengujian produk. Setelah produk dirilis, Anda dapat mengajukan tanda tangan yang berisi nama produk Anda.

### Mengapa pengajuan tanda tangan SMS saya tidak lulus peninjauan?

Ada banyak kemungkinan alasan, misalnya tanda tangan tidak sesuai dengan sertifikat yang dikirimkan atau sertifikat terkait belum diunggah. Silakan ajukan tanda tangan yang sesuai seperti yang diinstruksikan di halaman pengajuan tanda tangan sesuai dengan [signature review standards (standar peninjauan tanda tangan)](https://intl.cloud.tencent.com/document/product/382/40658).

### Apa yang harus saya masukkan sebagai keterangan tanda tangan?
Anda harus memasukkan **application description** (deskripsi pengajuan) hanya jika tanda tangan termasuk dalam salah satu jenis berikut:
- Aplikasi: masukkan tautan ke halaman tampilan aplikasi di toko/pasar aplikasi mana pun.
- Situs web: masukkan nama domain situs web yang memiliki izin ICP.
- Akun Resmi WeChat (atau Program Mini WeChat): masukkan nama lengkap Akun Resmi WeChat (atau Program Mini WeChat).

### Bagaimana cara menentukan tanda tangan saat memanggil API untuk mengirim pesan jika saya memiliki banyak tanda tangan?[](id:Q8)
Saat memanggil API [SendSms](https://intl.cloud.tencent.com/document/product/382/34859), Anda dapat mengatur bidang `sign` untuk memilih tanda tangan SMS yang diperlukan.
 Misalnya, jika Anda memiliki dua tanda tangan `Tencent Technology` dan `Tencent Cloud`, dan perlu mengirim pesan SMS menggunakan tanda tangan kedua, Anda hanya perlu mengatur bidang `sign` ke `Tencent Cloud` dan memanggil API yang sesuai untuk mengirim pesan.

### Dokumen apa saja yang harus saya siapkan saat mengajukan tanda tangan SMS?[](id:Q9)
Anda harus menyiapkan sejumlah dokumen sesuai dengan tujuan tanda tangan SMS dan jenis akun Anda. Untuk informasi selengkapnya, lihat [Daftar File Sertifikat](https://intl.cloud.tencent.com/document/product/382/40658#.E8.AF.81.E6.98.8E.E6.96.87.E4.BB.B6.E8.A7.84.E8.8C.83).

### Apakah pengguna individu dapat mengajukan tanda tangan SMS?[](id:Q10)
Pengguna individu dapat mengeklik **[Create Signature](https://console.cloud.tencent.com/smsv2/csms-sign)** (Buat Tanda Tangan) di **Chinese Mainland SMS** > **Signatures** (SMS Tiongkok Daratan > Tanda Tangan) di **konsol**. Namun, pengguna individu juga harus mengirimkan sertifikat yang sesuai. Untuk informasi selengkapnya, lihat [Daftar File Sertifikat](https://intl.cloud.tencent.com/document/product/382/40658#.E4.B8.AA.E4.BA.BA.E8.AE.A4.E8.AF.81.E7.94.A8.E6.88.B7).



[](id:Q11)
### Bagaimana cara pengguna individu mengajukan tanda tangan SMS?
Saat mengajukan tanda tangan SMS sebagai pengguna individu, Anda sebaiknya menggunakan nama aplikasi yang diluncurkan, Akun Resmi WeChat, Program Mini WeChat, atau situs web yang diajukan dengan MIIT sebagai tanda tangan dan mengirimkan sertifikat yang sesuai.
Saat membuat tanda tangan untuk penggunaan sendiri, Anda perlu mengunggah materi sertifikat berikut:
 <table>
<tr>
<th>Jenis Tanda Tangan</th>
<th>File Sertifikat</th>
</tr>
<tr>
<td>Aplikasi</td>
<td>Anda perlu mengunggah <b>tangkapan layar backend toko/pasar aplikasi</b></td>
</tr>
<tr>
<td>Situs Web</td>
<td>Anda perlu mengunggah <b>tangkapan layar backend izin ICP situs web</b></td>
</tr>
<tr>
<td>Akun Resmi WeChat atau Program Mini WeChat</td>
<td>Anda perlu mengunggah <b>tangkapan layar kepemilikan Akun Resmi WeChat atau Program Mini WeChat</b>: <ul><li>Akun Resmi WeChat: tangkapan layar halaman **Account Information** > **Account Details** (Informasi Akun > Detail Akun)</li><li>Program Mini WeChat: tangkapan layar halaman **Settings** > **Basic Settings** (Pengaturan > Pengaturan Dasar)</li></ul></td>
</tr>
</table>

[](id:Q12)
### Bagaimana cara mengajukan tanda tangan SMS untuk membantu perusahaan atau lembaga publik mengirim pesan SMS?
Saat ini, hanya perusahaan dan lembaga publik yang diizinkan untuk memberi otorisasi kepada orang lain untuk mengajukan tanda tangan bagi perusahaan atau lembaga publik tersebut. Jenis tanda tangan harus dipilih sebagai **For unverified entities** (Untuk entitas yang belum terverifikasi), dan [sertifikat] berikut(https://intl.cloud.tencent.com/document/product/382/40658#.E8.AF.81.E6.98.8E.E6.96.87.E4.BB.B6.E6.B8.85.E5.8D.95.EF.BC.88.E4.BB.96.E7.94.A8.E7.AD.BE.E5.90.8D.EF.BC.89) harus diunggah:
>?Saat ini, hanya perusahaan dan lembaga publik yang diizinkan untuk memberi otorisasi kepada orang lain untuk mengajukan tanda tangan bagi perusahaan atau lembaga publik tersebut.

 <table>
<tr>
<th>Jenis Tanda Tangan</th>
<th>File Sertifikat</th>
</tr>
<tr>
<td>Perusahaan</td>
<td rowspan="4">Anda perlu mengunggah <b><a href="https://sms-1258344699.cos.ap-guangzhou.myqcloud.com/Declaration%20of%20Authorisation%20(SMS%20Signature).docx">surat otorisasi</a> </b>dan salah satu sertifikat perusahaan dan lembaga publik<b> berikut dari entitas yang memiliki tanda tangan: </b><ul><li>Three-in-one</li><li>Izin usaha</li><li>Sertifikat kode organisasi</li><li>Sertifikat kode kredit sosial</li></ul></td>
</tr>
<tr>
<td>Aplikasi</td>
</tr>
<tr>
<td>Situs Web</td>
</tr>
<tr>
<td>Akun Resmi WeChat atau Program Mini WeChat</td>
</tr>
<tr>
<td>Merek Dagang</td>
<td>Anda perlu mengunggah <b><a href="https://sms-1258344699.cos.ap-guangzhou.myqcloud.com/Declaration%20of%20Authorisation%20(SMS%20Signature).docx">surat otorisasi</a></b> dan <b>sertifikat pendaftaran merek dagang</b></td>
</tr>
<tr>
<td nowrap="nowrap">Pemerintah/lembaga publik/lainnya</td>
<td>Anda perlu mengunggah <b><a href="https://sms-1258344699.cos.ap-guangzhou.myqcloud.com/Declaration%20of%20Authorisation%20(SMS%20Signature).docx">surat otorisasi</a> </b>dan salah satu sertifikat perusahaan dan lembaga publik<b> berikut dari entitas yang memiliki tanda tangan: <ul><li>Sertifikat kode organisasi</li><li>Sertifikat kode kredit sosial</li><li>Sertifikat badan hukum lembaga publik</li></ul></td>
</tr>
</table>
