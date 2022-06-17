
Ucapan selamat ulang tahun, liburan, dan hal-hal lain merupakan cara penting bagi perusahaan untuk mempertahankan pelanggan yang sudah ada. Anda dapat menggunakan SMS Tencent Cloud untuk mengirim pesan tersebut kepada pengguna pada hari-hari khusus, seperti hari libur, ulang tahun (peringatan tertentu) anggota, dan hari-hari dengan perubahan cuaca besar untuk layanan pelanggan.
>?Ucapan selamat termasuk ke dalam SMS pemasaran dan dapat dikirim hanya oleh **pengguna organisasi terverifikasi**. Untuk informasi selengkapnya, lihat [Perbedaan Hak](https://intl.cloud.tencent.com/document/product/382/13444#.E6.9D.83.E7.9B.8A.E5.8C.BA.E5.88.AB).

Dalam dokumen ini, pengiriman ucapan selamat Festival Musim Semi oleh perusahaan A kepada para anggota digunakan sebagai contoh untuk menjelaskan cara mengirim pesan tersebut dengan cepat.

## Persiapan
- [Buat akun Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985) dan verifikasi identitas organisasi Anda.
- [Beli](https://intl.cloud.tencent.com/document/product/382/35450) paket SMS.
- Siapkan sertifikat kualifikasi pemilik tanda tangan SMS.
 Misalnya, dokumen ini menggunakan izin usaha sebagai sertifikat kualifikasi.
- Pahami standar peninjauan konten isi SMS.



## Langkah 1. Buat tanda tangan

>?Setelah dikirimkan, tanda tangan SMS biasanya akan ditinjau dalam waktu dua jam. Anda dapat [mengonfigurasikan kontak alarm](https://intl.cloud.tencent.com/document/product/382/35470) untuk menerima pemberitahuan hasil peninjauan.

1. Login ke [Konsol SMS](https://console.cloud.tencent.com/smsv2).
2. Pilih **Chinese Mainland SMS** > **Signatures** (SMS Tiongkok Daratan > Tanda Tangan) di bilah sisi kiri, lalu klik **Create Signature** (Buat Tanda Tangan).
3. Atur parameter berikut sesuai dengan kebutuhan dan standar peninjauan tanda tangan:
 <table>
     <tr>
         <th>Parameter</th>  
         <th nowrap="nowrap">Nilai Sampel</th>  
     </tr>
	 <tr>      
       <td>Penggunaan tanda tangan</td>   
	     <td>Untuk entitas terverifikasi (seperti organisasi, situs web, atau nama produk dengan tanda tangan yang diverifikasi oleh akun)</td>   
     </tr> 
	 <tr>      
       <td>Jenis tanda tangan</td>   
	     <td>Perusahaan</td>   
     </tr> 
	 <tr>      
       <td>Konten tanda tangan</td>   
	     <td>A Co., Ltd.</td>   
     </tr> 
	 <tr>      
       <td>Jenis sertifikat</td>   
	     <td>Izin usaha</td>   
     </tr> 
	 <tr>      
       <td>Unggahan sertifikat</td>   
	<td><img src="https://main.qcloudimg.com/raw/d7547d5ca6c257be994112409cf88a53.jpg" width=200/></td>     
     </tr> 
</table>
3. Klik **OK** (Oke).
 Tunggu peninjauan tanda tangan. Tanda tangan SMS hanya akan tersedia setelah statusnya berubah menjadi **approved** (disetujui).


## Langkah 2. Buat templat isi
>Templat isi SMS umumnya akan ditinjau dalam waktu dua jam setelah dikirimkan. Anda dapat [mengonfigurasikan kontak alarm](https://intl.cloud.tencent.com/document/product/382/35470) untuk menerima pemberitahuan hasil peninjauan.

1. Login ke [Konsol SMS](https://console.cloud.tencent.com/smsv2).
2. Pilih **Chinese Mainland SMS** > **Body Templates** (SMS Tiongkok Daratan > Templat Isi) di bilah sisi kiri, lalu klik **Create Body Template** (Buat Templat Isi).
3. Atur parameter berikut sesuai dengan kebutuhan dan standar peninjauan templat isi:
 <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th nowrap="nowrap">Nilai Sampel</th>  
     </tr>
	 <tr>      
        <td>Nama templat</td>   
	     <td>Pesan ucapan selamat</td>   
     </tr> 
	 <tr>      
        <td>Jenis SMS</td>   
	     <td>SMS pemasaran</td>   
     </tr> 
	 <tr>      
        <td>Konten SMS</td>   
	     <td>Halo Ibu/Bapak {1}, terima kasih atas dukungan dan kepercayaan Anda. Kami ingin mengucapkan selamat menyambut Festival Musim Semi. Semoga semua harapan Anda dan orang terkasih dapat terwujud.</td>   
     </tr> 
</table>
4. Klik **OK** (Oke).
 Tunggu peninjauan templat isi. Templat isi hanya akan tersedia setelah statusnya berubah menjadi **approved** (disetujui).



## Langkah 3. Kirim SMS
Sebelum mengirim SMS, Anda perlu mengonfirmasi bahwa tanda tangan dan templat isi SMS telah disetujui.
Anda dapat mengirim SMS melalui konsol atau [API](https://intl.cloud.tencent.com/document/product/382/34859). Dalam dokumen ini, konsol digunakan sebagai contoh.

1. Login ke [Konsol SMS](https://console.cloud.tencent.com/smsv2).
2. Pilih **Chinese Mainland SMS** > **Bulk SMS** (SMS Tiongkok Daratan > SMS Massal) di bilah sisi kiri, lalu klik **Create Bulk SMS Sending Task** (Buat Tugas Pengiriman SMS Massal).
3. Konfigurasikan parameter berikut sesuai dengan kebutuhan:

 <table>
     <tr>
         <th nowrap="nowrap">Parameter</th>  
         <th>Nilai Sampel</th>  
     </tr>
	 <tr>
	     <td>Nama tanda tangan</td>   
	     <td>Pilih tanda tangan [A Co., Ltd.] yang dibuat di <a href="#Step1">langkah 1</a></td>   
     </tr> 
	 <tr>
	     <td>Nama templat</td>   
	     <td>Pilih **Best wishes message** (Pesan ucapan selamat) yang dibuat di <a href="#Step2">langkah 2</a></td>   
     </tr> 
	 <tr>
	     <td>Waktu terkirim</td>   
	     <td>Pilih **Send by schedule** (Kirim berdasarkan jadwal) dan tentukan titik waktu yang wajar hingga detik, misalnya **2020-01-25 00:00:00**. <br>Karena hanya titik waktu dalam satu bulan yang dapat ditentukan untuk jadwal, konfigurasikan tugas pengiriman dengan tepat.</td>   
     </tr> 
	 <tr>
	     <td>Penerima</td>   
	     <td>Klik **Download Standard Template** (Unduh Templat Standar), masukkan nomor ponsel penerima dan konten SMS kustom di formulir dengan merujuk ke <a href="#Table2">tabel sampel</a>, lalu klik **Click here** (Klik di sini) untuk mengunggahnya. Ukuran formulir maksimum yang didukung adalah 30 MB.</td>   
     </tr> 
</table>
 Berikut adalah tabel sampel:

 <table>
     <tr>
         <th width="50%">Nomor Ponsel Penerima</th>  
         <th>Variabel Konten SMS 1</th>
		</tr>
	 <tr>      
      <td>Contoh: 139xxxxxxxx <br>Instruksi: silakan masukkan nomor ponsel penerima. Semua nomor ponsel dalam satu pengiriman SMS harus terdaftar di Tiongkok Daratan. Sel harus dalam format biasa, yaitu tanpa format angka tertentu. </td> 
	     <td>Contoh: John Smith <br>Instruksi: silakan masukkan konten variabel kustom pertama sesuai dengan templat isi, yaitu mengganti {1} di templat. </td>
     </tr> 
</table>
3. Klik **OK** (Oke).
4. Periksa jumlah penerima, nyatakan persetujuan Anda di prompt tentang biaya, lalu klik **Send** (Kirim).
 Anda dapat melihat status tugas di daftar Delivery Records (Catatan Pengiriman). Jika statusnya **sent** (terkirim), tugas telah selesai.

## Langkah 4. Lihat hasil pengiriman SMS
Anda dapat melihat hasil pengiriman SMS dengan cara berikut:
- Di halaman **Chinese Mainland SMS** > **Bulk SMS** (SMS Tiongkok Daratan > SMS Massal), klik **Details & Receipt Analysis** (Detail & Analisis Penerimaan) di baris tugas target untuk melihat detail catatan dan analisis laporan.
- Pilih **Business Statistics** > **Chinese Mainland SMS** (Statistik Bisnis > SMS Tiongkok Daratan) agar Anda dapat memfilter dan melihat statistik dan analisis yang relevan untuk SMS Tiongkok Daratan berdasarkan aplikasi, tanda tangan, templat isi, dan waktu.
