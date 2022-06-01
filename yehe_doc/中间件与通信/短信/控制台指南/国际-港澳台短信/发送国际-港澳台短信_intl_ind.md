
## Prasyarat

- Template isi SMS telah disetujui.
- Jika Anda ingin menyertakan tanda tangan dalam pesan, Anda harus memiliki tanda tangan SMS yang disetujui.

## Petunjuk
1. Login ke [SMS Console (Konsol SMS)](https://console.cloud.tencent.com/sms).
2. Pilih **Global SMS** > **Bulk SMS** (SMS Global > SMS Massal) di bilah sisi kiri dan klik **Create Bulk SMS Sending Task** (Buat Tugas Pengiriman SMS Massal).
4. Konfigurasikan parameter berikut sesuai kebutuhan:
 - Template Name (Nama Template): pilih template isi yang disetujui untuk digunakan (ragam template dibedakan berdasarkan nama template).
 - Signature Name (Nama Tanda Tangan): pilih tanda tangan SMS yang disetujui untuk digunakan (ragam tanda tangan dibedakan berdasarkan nama tanda tangan), yang bersifat opsional.
 - Sending Time (Waktu Pengiriman): pilih **Send now** (Kirim sekarang) atau **Send by schedule** (Kirim berdasarkan jadwal).
 - Recipient (Penerima): klik **Template Download** (Unduh Template), masukkan nomor ponsel penerima dan konten SMS kustom dalam formulir, lalu klik **Click here** (Klik di sini) untuk mengunggahnya. Ukuran formulir maksimum yang didukung adalah 30 MB.
   >!Hingga 1.000 pesan SMS Global dapat dikirim per hari di bawah satu akun Tencent Cloud.
   >
   <table>
     <tr>
         <th width="22.5%">Nomor Ponsel Penerima</th>  
         <th width="22.5%">Variabel Konten SMS 1</th>  
         <th width="22.5%">Variabel Konten SMS 2</th>
				 <th width="10%">……</th>
				 <th>Variabel Konten SMS N</th>
		</tr>
	 <tr>      
        <td>Contoh: 139xxxxxxxx <br>Instruksi: silakan masukkan nomor ponsel penerima. Semua nomor ponsel dalam satu pengiriman SMS harus terdaftar di luar Tiongkok Daratan. Gunakan format sel biasa, yaitu tanpa format angka tertentu. </td>   
	     <td>Contoh: perusahaan tes A <br>Instruksi: silakan masukkan konten variabel kustom pertama sesuai dengan template isi, yaitu mengganti {1} dalam template. </td>   
	     <td>Contoh: server B <br>Instruksi: silakan masukkan konten variabel kustom kedua sesuai dengan template isi, yaitu mengganti {2} dalam template. </td>      
	     <td>……</td>        
	     <td>Contoh: 100 USD <br>Instruksi: silakan masukkan konten variabel khusus ke-N sesuai dengan template isi, yaitu mengganti {N} dalam template. </td>  
     </tr> 
</table>
 - Application (Aplikasi): pilih aplikasi yang perlu mengirim SMS.
4. Klik **OK**.
5. Periksa jumlah penerima, tunjukkan persetujuan Anda pada prompt tentang biaya, lalu klik **Send** (Kirim).
 Anda dapat melihat status tugas dalam daftar Catatan Pengiriman. Ketika statusnya **terkirim**, tugas telah selesai.

## Operasi Berikutnya

Anda dapat melihat hasil pengiriman SMS dengan cara berikut:
- Pada halaman **Global SMS** > **Bulk SMS** (SMS Global > SMS Massal), klik **Details & Report Analysis** (Analisis Detail & Laporan) pada baris tugas target untuk melihat catatan mendetail dan analisis laporan.
- Pilih **Business Statistics** > **Global SMS** (Statistik Bisnis > SMS Global). Di sana, Anda dapat memfilter serta melihat statistik dan analisis yang relevan dari SMS Global berdasarkan aplikasi, tanda tangan, template isi, dan waktu.

## Dokumentasi Terkait
Anda juga dapat mengirim SMS melalui API atau SDK. Untuk petunjuk lengkapnya, silakan lihat [dokumentasi API](https://intl.cloud.tencent.com/document/product/382/39155) atau [dokumentasi SDK](https://intl.cloud.tencent.com/document/product/382/36788).
