[](id:senderConfig)
## Opsi Konfigurasi Pengirim
Simple Email Service (SES) menyediakan tiga cara untuk mengirim email: Konsol SES, SES API, dan SES SMTP. Anda dapat menggunakan antarmuka baris perintah SES (SES CLI) atau [SES SDK untuk memanggil API](https://intl.cloud.tencent.com/document/product/1084/39387)  atau memanggil API SMTP untuk mengirim email.

Untuk mengirim email, lihat [**Panduan Konsol** > **Pengiriman Email**](https://intl.cloud.tencent.com/document/product/1084/40178).
## Opsi Deployment Fleksibel
### Alamat IP Bersama
Umumnya, SES mengirim email dari alamat IP bersama di kumpulan IP bersama secara default. Alamat bersama adalah opsi yang cepat dan mudah digunakan bagi pengguna yang ingin segera mulai mengirim dengan IP yang sudah ada. Tencent Cloud membantu memastikan kualitas IP bersama dan tingkat pengiriman yang tinggi.
### Alamat IP Khusus
IP khusus adalah IP yang ditetapkan secara khusus kepada Anda oleh Tencent Cloud untuk mengirim email. Umumnya, IP Khusus ini tidak pernah digunakan untuk pengiriman email atau telah menikmati reputasi yang baik selama ini, yang memastikan bahwa itu tidak akan ditandai sebagai IP spam oleh organisasi anti-spam. Anda dapat mengajukan permohonan IP khusus untuk volume pengiriman Anda. Jika Anda perlu mengirim email dalam jumlah besar, hubungi perwakilan penjualan Anda untuk mengajukan IP khusus.


## Manajemen dan Keamanan Identitas Pengirim
Saat menerima email, penyedia layanan internet (ISP) akan memeriksa apakah itu diautentikasi sebelum mengirimkannya ke penerima. Autentikasi membuktikan kepada ISP bahwa Anda adalah pemilik alamat email yang Anda gunakan untuk mengirim. SES mendukung semua mekanisme autentikasi standar industri, termasuk Sender Policy Framework (SPF), Domain Keys Identified Mail (DKIM), dan Domain-based Message Authentication. Ini dapat memastikan bahwa email Anda lulus pemeriksaan ISP dan berhasil dikirim ke penerima.
## Statistik Pengiriman
SES menyediakan berbagai metode untuk memantau aktivitas pengiriman email. Misalnya, statistik ini dapat menangkap informasi tentang seluruh saluran tanggapan email (termasuk jumlah pengiriman, dibuka, diklik, pentalan, dll.) dan memberikan analisis data yang akurat. Selain itu, Anda dapat memeriksa status pengiriman email tertentu dengan memanggil [GetSendEmailStatus](https://intl.cloud.tencent.com/document/product/1084/39502) untuk membantu Anda menyesuaikan kebijakan pengiriman email.

[](id:warmUp)
## Warm-up Otomatis 
### Fitur
Proses pengiriman email bisa sangat rumit. Reputasi IP/domain sangat penting untuk meningkatkan kemampuan pengiriman. Warm-up adalah proses membangun reputasi pengiriman Anda. Volume pengiriman harus ditingkatkan secara bertahap dari hari ke hari, dan tidak dapat diangkat ke tingkat yang diinginkan dengan sekali tekan. Warm-up yang baik membantu membangun reputasi yang baik dengan ISP Anda.
>? Warm-up otomatis mengacu pada pemanasan secara otomatis alamat IP atau domain pengirim Anda tanpa intervensi manual selama proses berlangsung.
### Deskripsi
Warm-up otomatis dibagi menjadi dua kategori: [Aturan Standar (Default)](#default) dan [Aturan yang Ditingkatkan](#customize).

#### Aturan default:
Aturan warm-up standar berlaku secara default di bawah mode pengiriman batch. Backend akan menentukan kemajuan warm-up berdasarkan serangkaian kebijakan dan secara otomatis menetapkan kuota pengiriman harian. Seluruh proses sepenuhnya berjalan otomatis. Ketika jumlah maksimum email terkirim yang diizinkan per hari tercapai, pengiriman email akan berhenti dan email tambahan akan masuk ke antrean cache dan dikirim dalam 24 jam kemudian. Rencana warm-up standar adalah sebagai berikut: [](id:default)

<table style="width: 200px;">
   <tr>
      <th width="0px" style="text-align:center">Hari</td>
      <th width="0px" style="text-align:center">Volume Pengiriman/Hari</td>
   </tr>
	<tr>
		<td style="text-align:center"style="text-align:center">1</td>
		<td style="text-align:center">500</td>
	</tr>
	<tr>
		<td style="text-align:center">2</td>
		<td style="text-align:center"sdval="200" >1.000</td>
	</tr>
	<tr>
		<td style="text-align:center">3</td>
		<td style="text-align:center"sdval="500" >2.000</td>
	</tr>
	<tr>
		<td style="text-align:center">4</td>
		<td style="text-align:center"sdval="1000" >5.000</td>
	</tr>
	<tr>
		<td style="text-align:center">5</td>
		<td style="text-align:center"sdval="2000" >10.000</td>
	</tr>
	<tr>
		<td style="text-align:center">6</td>
		<td style="text-align:center"sdval="5000" >20.000</td>
	</tr>
	<tr>
		<td style="text-align:center">7</td>
		<td style="text-align:center"sdval="10000" >40.000</td>
	</tr>
	<tr>
		<td style="text-align:center">8</td>
		<td style="text-align:center"sdval="20000" >60.000</td>
	</tr>
	<tr>
		<td style="text-align:center">9</td>
		<td style="text-align:center"sdval="30000" >80.000</td>
	</tr>
	<tr>
		<td style="text-align:center">10</td>
		<td style="text-align:center"sdval="40000" >100.000</td>
	</tr>
	<tr>
		<td style="text-align:center">11</td>
		<td style="text-align:center"sdval="60000" >150.000</td>
	</tr>
	<tr>
		<td style="text-align:center">12</td>
		<td style="text-align:center"sdval="80000" >200.000</td>
	</tr>
	<tr>
		<td style="text-align:center">13</td>
		<td style="text-align:center"sdval="100000" >300.000</td>
	</tr>
	<tr>
		<td style="text-align:center">14</td>
		<td style="text-align:center"sdval="120000" >400.000</td>
	</tr>
	<tr>
		<td style="text-align:center">15</td>
		<td style="text-align:center"sdval="150000" >500.000</td>
	</tr>
	<tr>
		<td style="text-align:center">16</td>
		<td style="text-align:center"sdval="200000" >600.000</td>
	</tr>
	<tr>
		<td style="text-align:center">17</td>
		<td style="text-align:center"sdval="400000" >700.000</td>
	</tr>
	<tr>
		<td style="text-align:center">18</td>
		<td style="text-align:center"sdval="600000" >800.000</td>
	</tr>
	<tr>
		<td style="text-align:center">19</td>
		<td style="text-align:center"sdval="800000" >900.000</td>
	</tr>
		<tr>
		<td style="text-align:center">20</td>
		<td style="text-align:center"sdval="800000" >1.000.000</td>
	</tr>
</table>

[](id:customize)
#### Aturan kustom:
Untuk email berkualitas tinggi, jika paket warm-up standar tidak dapat memenuhi kebutuhan Anda, Anda dapat mengajukan permohonan untuk paket warm-up yang ditingkatkan. Untuk mengetahui detailnya, hubungi perwakilan penjualan Anda untuk mengajukan rencana tersebut.
[](id:batch)
## Kumpulan Fitur Batch
Ini cocok untuk pengiriman batch email pemasaran atau pemberitahuan. Untuk mengirim email berbasis pemicu (seperti autentikasi dan email transaksional), sebaiknya panggil API `SendEmail`.
### Fitur
Anda dapat menggunakan fitur pengiriman batch SES dengan salah satu cara berikut:
• Konsol: Diperlukan templat, ukuran email tidak boleh melebihi 10 MB, dan lampiran tidak didukung.
• API: Diperlukan templat, ukuran email tidak boleh melebihi 10 MB, dan lampiran didukung.

### Deskripsi
Di konsol, Anda dapat mengelola alamat pengirim di halaman **Pengiriman Email** > **Grup Penerima**.

Fitur pengiriman batch diatur untuk menggunakan rencana pemanasan standar. Paket akan secara otomatis mengidentifikasi reputasi IP/domain, menetapkan kuota pengiriman harian, dan menentukan apakah total volume pengiriman melebihi jumlah maksimum yang diizinkan per hari. Jika demikian, pengiriman email akan berhenti dan email tambahan akan masuk ke antrean cache dan dikirim dalam waktu 24 jam kemudian.

## Batch
Untuk mengirim email dalam batch, buat tugas pengiriman di konsol, pilih **Batch** (Batch) untuk **Task Type** (Jenis Tugas), dan atur semua bidang yang diperlukan untuk tugas tersebut.
## Dijadwalkan
Email dapat dikirim pada waktu yang dijadwalkan. Pilih **Start Time** (Waktu Mulai) untuk tugas dan email akan dikirim secara otomatis pada waktu yang ditentukan.
## Berulang
Anda dapat mengatur email berulang di konsol dengan menentukan bidang tugas termasuk **Start Time** (Waktu Mulai) dan **Recurrence** (Pengulangan). Konsol akan secara otomatis mengirim email berdasarkan pengulangan yang ditentukan.
