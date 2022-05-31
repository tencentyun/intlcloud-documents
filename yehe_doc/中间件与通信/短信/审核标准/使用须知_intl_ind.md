
## Mode Verifikasi
### Ikhtisar verifikasi identitas
[Verifikasi identitas] Tencent Cloud(https://intl.cloud.tencent.com/document/product/378/3629) terdiri dari verifikasi individu dan organisasi. **Mode verifikasi yang berbeda sesuai dengan fitur SMS yang berbeda. Sebaiknya Anda memilih mode verifikasi identitas berdasarkan kepemilikan akun Anda yang sebenarnya.**

| Jenis             | Objek                           | Kepemilikan Akun | Panduan Pengoperasian                                                     |
| :--------------- | :--------------------------------- | :------- | :----------------------------------------------------------- |
| Verifikasi Individu | Individu                               | Individu      | [Panduan Verifikasi Individu](https://intl.cloud.tencent.com/document/product/378/10495) |
| Verifikasi Organisasi | Perusahaan, pemerintah, lembaga publik, sekolah, dan organisasi | Organisasi     | [Panduan Verifikasi Organisasi](https://intl.cloud.tencent.com/document/product/378/10496) |

Jika sudah menyelesaikan Verifikasi Individu untuk akun Anda, Anda dapat mengajukan perubahan identitas organisasi. Pengguna yang belum menyelesaikan verifikasi identitas tidak dapat membeli sumber daya di Tiongkok Daratan.

### Perbedaan hak

<table>
     <tr>
         <th>Fitur</th>  
         <th width="40%">Pengguna Individu</th>  
         <th width="40%">Pengguna Organisasi</th>  
     </tr>
	 <tr>      
         <td>Paket gratis</td>   
	     <td>Sebanyak 100 pesan SMS Tiongkok Daratan diberikan secara gratis setelah aktivasi layanan untuk pertama kalinya</td>   
	     <td>Sebanyak 1.000 pesan SMS Tiongkok Daratan diberikan secara gratis setelah aktivasi layanan untuk pertama kalinya</td>   
     </tr> 
	 <tr>
	     <td>SMS Tiongkok Daratan Biasa</td>   
	     <td>Didukung</td>   
	     <td>Didukung</td> 
     </tr> 
	 <tr>
	     <td>SMS Tiongkok Daratan Pemasaran</td>   
	     <td>Tidak Didukung</td>   
	     <td>Didukung</td> 
     </tr> 
	 <tr>      
         <td>SMS Global</td>    
	     <td>Didukung</td>   
	     <td>Didukung</td> 
     </tr>  
	 <tr>      
         <td>Jenis tanda tangan</td>  
	     <td>Jika tanda tangan dimiliki oleh individu, jenis tanda tangan berikut tidak didukung: <b>perusahaan</b>, <b>merek dagang</b>, dan <b>pemerintah/lembaga publik/lainnya</b></td>   
	     <td>Jika tanda tangan dimiliki oleh perusahaan atau lembaga publik, semua jenis tanda tangan didukung</td> 
     </tr> 
	 <tr>      
         <td>Templat isi</td>
	     <td>Sebuah variabel dapat berisi hingga 12 karakter<br>Satu karakter, huruf, angka, tanda baca bahasa Mandarin (dalam bentuk fullwidth atau halfwidth), atau spasi akan dihitung sebagai satu karakter</td>   
	     <td>Tidak ada batasan jumlah karakter dalam setiap variabel, tetapi templat tidak boleh hanya berisi variabel</td> 
     </tr>     
		      <tr> 
         <td>Kontrol batas frekuensi kustom</td>     
	     <td>Tidak Didukung</td>   
	     <td>Didukung</td> 
     </tr> 
		      <tr> 
         <td>API tanda tangan dan templat isi</td>     
	     <td>Tidak didukung. Tanda tangan dan templat isi hanya dapat dikelola di konsol SMS</td>   
	     <td>Didukung</td> 
     </tr> 		 
</table>


## Standar Peninjauan
Pesan SMS terdiri atas tanda tangan dan isi. Sebelum mengirim pesan SMS, Anda harus membuat tanda tangan SMS dan templat isi SMS.

| Komponen | Deskripsi | Standar Peninjauan |
|---------|---------|---------|
| Tanda Tangan | Tanda tangan SMS harus sesuai dengan atribut pemiliknya. Anda harus memberikan sertifikat kualifikasi yang sesuai saat membuat tanda tangan, yang hanya dapat digunakan setelah disetujui. | [Signature Review Standards (Standar Peninjauan Tanda Tangan)](https://intl.cloud.tencent.com/document/product/382/40658) |
| Konten isi | Anda harus mengajukan templat isi SMS untuk konten SMS terlebih dahulu, yang hanya dapat digunakan setelah disetujui. <br>Templat ini memungkinkan Anda menggunakan variabel untuk melakukan kustomisasi konten SMS, dan makna serta skenario pesan harus dapat diidentifikasi melalui konten teks (tidak termasuk variabel). | [Body Template Review Standards (Standar Peninjauan Templat Isi)](https://intl.cloud.tencent.com/document/product/382/40659) |

## Proses Peninjauan
### Durasi peninjauan
Umumnya, hasil tinjauan akan dikembalikan dalam waktu sekitar 2 jam setelah Anda membuat tanda tangan SMS atau templat isi (waktu peninjauan: pukul 09.00–23.00 setiap hari).
Jika Anda membutuhkan fitur SMS dengan segera, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category), dan kami akan mempercepat peninjauan.

### Deskripsi status peninjauan
- Peninjauan tertunda: Anda telah mengirimkan tanda tangan SMS atau templat isi, dan menunggu untuk ditinjau. Hasil peninjauan akan diberikan dalam waktu sekitar 2 jam.
- Disetujui: tanda tangan SMS atau templat isi Anda telah disetujui. Jika keduanya disetujui, Anda dapat mulai mengirim pesan SMS.
 Templat isi yang disetujui tidak berarti pesan akan berhasil dikirim (karena ISP juga memiliki mekanisme peninjauan berbasis sampel). Jika pesan SMS Anda gagal terkirim, Anda dapat melihat [Bantuan SMS](https://intl.cloud.tencent.com/document/product/382/3773) untuk mendapatkan bantuan.
- Ditolak: tanda tangan atau templat isi Anda ditolak karena beberapa alasan.
  Anda dapat login ke konsol [SMS](https://console.cloud.tencent.com/sms/smsSign/1400054957/0/10) dan klik **View Failure Reason and Modify** (Lihat Alasan Kegagalan dan Modifikasi) di sebelah tanda tangan atau templat target untuk melihat alasan spesifik penolakan. Anda juga dapat [mengirim tiket](https://console.cloud.tencent.com/workorder/category) untuk mendapatkan bantuan.

## Aturan Penangguhan
Kami akan meninjau tanda tangan SMS dan templat isi yang Anda buat dan memantau serta memeriksa konten pesan SMS yang benar-benar terkirim untuk mencegah pelanggaran undang-undang dan hukum nasional yang berlaku.
Jika konten SMS yang tidak mematuhi persyaratan layanan ditemukan, akun Anda akan ditangguhkan, dan uang jaminan Anda akan dipotong, atau Anda akan dimintai pertanggungjawaban sesuai dengan situasi sebenarnya. Setelah akun Anda ditangguhkan, Anda tidak dapat terus menggunakan layanan SMS lagi dan tidak dapat mengajukan aktivasi kembali pada masa mendatang, dan paket layanan SMS yang tidak digunakan di akun Anda tidak dapat digunakan.
Silakan patuhi persyaratan dalam [Spesifikasi Tanda Tangan SMS](https://intl.cloud.tencent.com/document/product/382/40658) dan [Spesifikasi Templat Isi SMS](https://intl.cloud.tencent.com/document/product/382/40659), perkuat keamanan bisnis Anda, dan kirim pesan SMS yang mematuhi persyaratan.

