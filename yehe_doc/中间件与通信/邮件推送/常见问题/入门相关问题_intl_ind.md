[](id:que1) 
### Bagaimana cara menguji pengiriman email dengan beberapa cara sederhana?
Anda dapat menggunakan akun Anda sendiri untuk pengujian. Saat ini, SES menawarkan tingkat 1.000 email gratis tetapi tidak menawarkan akun pengujian.

[](id:que5) 
### Dapatkah saya mengirim email dalam jumlah besar sejak awal?
Tidak. Volume pengiriman harus ditingkatkan secara bertahap dari hari ke hari, dan tidak dapat dinaikkan ke tingkat yang diinginkan dengan sekali tekan. Untuk mendapatkan reputasi yang baik dengan ISP Anda, warm-up otomatis diperlukan sebelum pengiriman email. Aturan warm-up standar berlaku secara default di bawah mode pengiriman batch. Silakan lihat [Fitur](https://intl.cloud.tencent.com/document/product/1084/43285).

[](id:que6) 
### Apa yang dimaksud dengan warm-up?
Warm-up adalah cara membangun reputasi IP baru. Umumnya, semua penyedia layanan email memiliki batasan jumlah harian email yang dikirim dari IP. Anda harus mulai dengan jumlah email yang lebih sedikit dan secara bertahap meningkatkan jumlahnya setiap hari.

[](id:que7) 
Aturan warm-up standar berlaku secara default di bawah mode pengiriman batch. Backend akan menentukan kemajuan warm-up berdasarkan serangkaian kebijakan dan secara otomatis menetapkan kuota pengiriman harian. Seluruh proses sepenuhnya berjalan otomatis. Ketika jumlah maksimum email terkirim yang diizinkan per hari tercapai, pengiriman email akan berhenti dan email tambahan akan masuk ke antrean cache dan dikirim dalam 24 jam kemudian. Rencana warm-up standar adalah sebagai berikut:
<table style="width: 200px;">
   <tr>
      <th width="0px" style="text-align:center">Hari</td>
      <th width="0px" style="text-align:center">Volume Pengiriman/Hari</td>
   </tr>
	<tr>
		<td style="text-align:center"style="text-align:center">1</td>
		<td style="text-align:center">100</td>
	</tr>
	<tr>
		<td style="text-align:center">2</td>
		<td style="text-align:center"sdval="200" >200</td>
	</tr>
	<tr>
		<td style="text-align:center">3</td>
		<td style="text-align:center"sdval="500" >500</td>
	</tr>
	<tr>
		<td style="text-align:center">4</td>
		<td style="text-align:center"sdval="1000" >1.000</td>
	</tr>
	<tr>
		<td style="text-align:center">5</td>
		<td style="text-align:center"sdval="2000" >2.000</td>
	</tr>
	<tr>
		<td style="text-align:center">6</td>
		<td style="text-align:center"sdval="5000" >5.000</td>
	</tr>
	<tr>
		<td style="text-align:center">7</td>
		<td style="text-align:center"sdval="10,000" >10.000</td>
	</tr>
	<tr>
		<td style="text-align:center">8</td>
		<td style="text-align:center"sdval="20,000" >20.000</td>
	</tr>
	<tr>
		<td style="text-align:center">9</td>
		<td style="text-align:center"sdval="30000" >30.000</td>
	</tr>
	<tr>
		<td style="text-align:center">10</td>
		<td style="text-align:center"sdval="40000" >40.000</td>
	</tr>
	<tr>
		<td style="text-align:center">11</td>
		<td style="text-align:center"sdval="60000" >60.000</td>
	</tr>
	<tr>
		<td style="text-align:center">12</td>
		<td style="text-align:center"sdval="80000" >80.000</td>
	</tr>
	<tr>
		<td style="text-align:center">13</td>
		<td style="text-align:center"sdval="100000" >100.000</td>
	</tr>
	<tr>
		<td style="text-align:center">14</td>
		<td style="text-align:center"sdval="120000" >120.000</td>
	</tr>
	<tr>
		<td style="text-align:center">15</td>
		<td style="text-align:center"sdval="150000" >150.000</td>
	</tr>
	<tr>
		<td style="text-align:center">16</td>
		<td style="text-align:center"sdval="200000" >200.000</td>
	</tr>
	<tr>
		<td style="text-align:center">17</td>
		<td style="text-align:center"sdval="400000" >400.000</td>
	</tr>
	<tr>
		<td style="text-align:center">18</td>
		<td style="text-align:center"sdval="600000" >600.000</td>
	</tr>
	<tr>
		<td style="text-align:center">19</td>
		<td style="text-align:center"sdval="800000" >800.000</td>
	</tr>
		<tr>
		<td style="text-align:center">20</td>
		<td style="text-align:center"sdval="800000" >1.000.000</td>
	</tr>
</table>

Aturan kustom:

Untuk email berkualitas tinggi, jika rencana warm-up standar tidak dapat memenuhi kebutuhan Anda, Anda dapat menggunakan rencana warm-up kustom. Untuk mengetahui detailnya, hubungi perwakilan penjualan Anda untuk mengajukan rencana tersebut.
