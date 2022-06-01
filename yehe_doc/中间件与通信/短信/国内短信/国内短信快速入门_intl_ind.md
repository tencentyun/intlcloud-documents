Dokumen ini membantu Anda untuk memulai penggunaan layanan SMS Tiongkok Daratan secara cepat dengan menjelaskan cara pengguna organisasi mengirim pesan berikut `[Tencent Cloud] Kode verifikasi Anda adalah: XXXX` ke nomor ponsel di Tiongkok Daratan. Untuk konsep SMS selengkapnya, lihat [Glossary (Glosarium)](https://intl.cloud.tencent.com/document/product/382/13299).

>?Konsol versi baru ditampilkan kepada pengguna yang mengaktifkan layanan SMS setelah 18 September 2019 secara default.

## Langkah 1: Aktifkan layanan SMS
### Membuat akun Tencent Cloud
- Jika belum memiliki akun Tencent Cloud, Anda perlu [membuat akun Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985) dan [memverifikasi identitas organisasi Anda](https://intl.cloud.tencent.com/document/product/378/10496).
- Jika sudah memiliki akun Tencent Cloud dan sudah memverifikasi identitas, Anda dapat langsung melanjutkan ke langkah selanjutnya.

### Mengajukan permohonan aktivasi SMS
>?Saat login ke konsol SMS untuk pertama kalinya, Anda harus mengajukan permohonan untuk mengaktifkan layanan SMS.

1. Login ke [konsol SMS](https://console.cloud.tencent.com/smsv2), klik **I've read and agree to Tencent Cloud SMS Terms of Service** (Saya sudah membaca dan setuju dengan Ketentuan Layanan SMS Tencent Cloud), lalu klik **Access** (Akses) untuk mengaktifkan layanan.
2. Pilih **Getting Started** (Memulai) di bilah sisi kiri, lalu klik **Start creating** (Mulai membuat) untuk masuk ke halaman panduan pengiriman SMS.

## Langkah 2. Konfigurasikan konten SMS
 Pesan SMS lengkap terdiri dari **tanda tangan SMS** dan **isi SMS**. Anda dapat mengatur templat isi yang berbeda sesuai dengan kebutuhan dan kemudian menggabungkan tanda tangan dan isi ke dalam konten SMS akhir: `[tanda tangan SMS] isi SMS`. Tanda tangan atau templat SMS biasanya akan ditinjau dalam waktu dua jam setelah dikirim. Anda dapat mengatur nomor ponsel dan alamat email Anda untuk menerima pemberitahuan hasil peninjauan.

### Memilih wilayah
1. Di halaman [Memulai](https://console.cloud.tencent.com/smsv2/guide), pilih wilayah di sudut kiri atas.
Tencent Cloud International menawarkan layanan di banyak wilayah dengan fitur produk dan harga yang sama. Namun, data tidak dapat disimpan di wilayah lain dan, sebaliknya, harus disimpan di wilayah lokal. Silakan pilih wilayah sesuai dengan kebutuhan penyimpanan data Anda.
![](https://qcloudimg.tencent-cloud.cn/raw/75bdff7ee617e9fb7f2d71d7258b9b5f.png)

[](id:Sign)
### Membuat tanda tangan
1. Di halaman [Memulai](https://console.cloud.tencent.com/smsv2/guide), klik **Start creating** (Mulai membuat).
2. Atur parameter berikut sesuai dengan kebutuhan:
 - Signature Purpose (Tujuan Tanda Tangan): pilih **For verified entities (such as organizations, websites or product names with signatures verified by the account)** (Untuk entitas terverifikasi (seperti organisasi, situs web, atau nama produk dengan tanda tangan yang diverifikasi oleh akun).
 - Signature Type (Jenis Tanda Tangan): pilih **Company** (Perusahaan).
 - Signature Content (Konten Tanda Tangan): masukkan `Tencent Cloud`.
 - Certificate Type (Jenis Sertifikat): pilih **Three-in-one**.
 - Certificate Upload (Unggahan Sertifikat): unggah foto atau pindaian sertifikat.
3. Klik **OK** (Oke).
 Silakan tunggu peninjauan tanda tangan. Tanda tangan hanya akan tersedia setelah statusnya berubah menjadi **Approved** (Disetujui).

[](id:Template)
### Membuat templat isi
1. Di halaman [Memulai](https://console.cloud.tencent.com/smsv2/guide), klik **Start creating** (Mulai membuat).
2. Atur parameter berikut sesuai dengan kebutuhan:
 - Template Name (Nama Templat): masukkan `Verification Code` (Kode Verifikasi).
 - SMS Type (Jenis SMS): pilih **Regular SMS** (SMS Biasa).
 - SMS content (Konten SMS): masukkan `Your verification code is: {1}` (Kode verifikasi Anda adalah {1}).
3. Klik **OK** (Oke).
 Silakan tunggu peninjauan templat isi. Templat isi hanya akan tersedia setelah statusnya berubah menjadi **Approved** (Disetujui).

## Langkah 3. Tunggu persetujuan
Tanda tangan atau templat isi SMS umumnya akan ditinjau dalam waktu dua jam setelah dikirim. Anda dapat mengatur nomor ponsel dan alamat email Anda untuk menerima pemberitahuan hasil peninjauan.
Di halaman [Memulai](https://console.cloud.tencent.com/smsv2/guide), Anda dapat mengeklik **View** (Tampilkan) untuk melihat status peninjauan tanda tangan atau templat isi dengan cepat. Tanda tangan atau templat isi hanya akan tersedia setelah statusnya berubah menjadi **approved** (disetujui).

## Langkah 4. Kirim pesan SMS
>!
>1. Tanda tangan dan templat SMS untuk setiap wilayah harus dibuat secara terpisah, tetapi tanda tangan dan templat tersebut dapat disalin di seluruh wilayah. Sebelum mengirim pesan SMS, pastikan wilayah yang dipilih untuk aplikasi SMS sama dengan wilayah yang dipilih untuk pembuatan tanda tangan dan templat.
>2. Sebelum mengirim pesan SMS, pastikan tanda tangan dan templat isi SMS telah disetujui.  

Anda dapat mengirim pesan SMS melalui konsol atau [API](https://intl.cloud.tencent.com/document/product/382/40463). Dalam dokumen ini, konsol digunakan sebagai contoh.

1. Di halaman [Memulai](https://console.cloud.tencent.com/smsv2/guide), klik **Send SMS** (Kirim SMS).
2. Konfigurasikan parameter berikut sesuai dengan kebutuhan:
 - Signature Name (Nama Tanda Tangan): pilih tanda tangan **Tencent Cloud** yang dibuat di langkah [Membuat tanda tangan](#Sign).
 - Template Name (Nama Templat): pilih templat **Verification Code** (Kode Verifikasi) yang dibuat di langkah [Membuat templat isi](#Template).[](id:model)
 - Sending Time (Waktu Pengiriman): pilih **Send now** (Kirim sekarang).
 - Recipient (Penerima): pilih **Upload mobile numbers** (Unggah nomor ponsel), klik **Download Standard Template** (Unduh Templat Standar), masukkan nomor ponsel penerima dan konten SMS kustom dalam formulir, lalu klik **Click here** (Klik di sini) untuk mengunggahnya. Ukuran maksimum formulir yang didukung adalah 30 MB.
<table>
     <tr>
				 <th>Deskripsi Templat</th>
         <th width="50%">Nomor Ponsel Penerima</th>  
         <th>Variabel Konten SMS 1</th>
		</tr>
	 <tr>
		 <td>Sampel</td>
      <td>139xxxxxxxx</td> 
	     <td>9097</td>
     </tr> 
		 <td>Instruksi</td>
      <td>Silakan masukkan nomor ponsel penerima. Semua nomor ponsel dalam satu tugas pengiriman SMS harus terdaftar di Tiongkok Daratan. Sel harus dalam format biasa, yaitu tanpa format angka tertentu.</td> 
	     <td>Silakan masukkan konten variabel kustom pertama sesuai dengan templat isi, yaitu mengganti {1} di templat. </td>
     </tr>
</table>
<b>Ada tiga jenis penerima, yaitu sebagai berikut: </b><span id = "object"></span>
<table>
     <tr>
				 <th>Penerima</th>
         <th>Deskripsi</th>  
         <th>Templat Variabel</th>
		</tr>
	 <tr>
		 <td>Unggah nomor ponsel</td>
      <td><ul><li>Anda dapat mengunggah hingga 1 juta nomor ponsel dalam file CSV atau XLSX berukuran maksimum 30 MB untuk setiap tugas pengiriman SMS massal. </li><li>Dalam templat isi SMS yang dibuat oleh pengguna individu, setiap variabel dapat berisi hingga 12 karakter. <li>Tidak ada batasan panjang nilai variabel untuk pengguna organisasi.</li></ul></td> 
	     <td>Didukung</td>
     </tr>
		 <tr>
		 <td>Pilih grup pelanggan</td>
      <td>Klik **Customer Group** (Grup Pelanggan) dan pilih grup nomor yang telah dibuat di <a href = "https://console.cloud.tencent.com/smsv2/phone-manage/group-manage">Grup Pelanggan</a>. <br><b>Catatan:</b> Anda tidak dapat memilih templat dengan variabel untuk <a href = "#model">Nama Templat</a>.</td> 
	     <td>Tidak didukung</td>
     </tr> 		
		 		 <tr>
		 <td>Masukkan nomor ponsel</td>
      <td>Masukkan hingga 100 nomor ponsel dan pisahkan dengan menekan tombol Enter (satu nomor per baris).
Untuk nomor ponsel Tiongkok Daratan, silakan masukkan nomor ponsel secara langsung: <br>Misalnya, 1371481xxxx. <br><b>Catatan:</b> Anda tidak dapat memilih templat dengan variabel untuk <a href = "#model">Nama Templat</a>.</td> 
	     <td>Tidak didukung</td>
     </tr> 
</table>
 - Application (Aplikasi): pilih aplikasi yang perlu mengirim SMS. Untuk informasi selengkapnya, lihat [Creating Application (Membuat Aplikasi)](https://intl.cloud.tencent.com/document/product/382/35468).
3. Klik **OK** (Oke).
4. Periksa jumlah penerima, nyatakan persetujuan Anda di prompt tentang biaya, lalu klik **Send** (Kirim).
 Anda dapat melihat status tugas di daftar “Sending Records” (Catatan Pengiriman). Status **Sent** (Terkirim) menunjukkan bahwa tugas telah selesai.

## Langkah 5. Lihat hasil pengiriman SMS
Anda dapat melihat hasil pengiriman SMS dengan cara berikut:
- Di halaman **Chinese Mainland SMS** > **Bulk SMS** (SMS Tiongkok Daratan > SMS Massal), klik **Details & Receipt Analysis** (Detail & Analisis Penerimaan) di baris tugas target untuk melihat detail catatan dan analisis penerimaan.
- Pilih **Business Statistics** > **Chinese Mainland SMS** (Statistik Bisnis > SMS Tiongkok Daratan) agar Anda dapat memfilter dan melihat statistik dan analisis yang relevan untuk SMS Tiongkok Daratan berdasarkan aplikasi, tanda tangan, templat isi, dan waktu.


