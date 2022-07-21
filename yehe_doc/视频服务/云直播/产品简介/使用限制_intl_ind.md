Sebelum menggunakan CSS, Anda perlu mengetahui batas penggunaan berikut:

<table>
<tr><th>Deskripsi</th><th>Item</th></tr>
<tr>
<td>Nama domain CSS</td>
<td><ul style="margin:0">
 <li>Anda dapat membuat beberapa nama domain pemutaran ulang dan push dalam satu akun. Jika Tiongkok Daratan atau global dipilih sebagai wilayah akselerasi suatu nama domain, nama domain tersebut harus memiliki izin ICP dari MIIT, dan informasi izin harus masih berlaku dan tersedia.</li>
    <li>Anda dapat mengelola hingga 100 nama domain dalam satu akun secara default. Jika memiliki bisnis berskala besar, Anda dapat <a href="https://console.cloud.tencent.com/workorder/category">mengirimkan tiket</a> untuk mengajukan permohonan penambahan jumlah maksimum nama domain.</li>
    <li>Panjang nama domain sebaiknya tidak lebih dari 45 karakter. Jika ingin menggunakan nama domain yang <strong>lebih panjang</strong>, Anda harus <a href="https://console.cloud.tencent.com/workorder/category">mengirimkan tiket</a> untuk mendapatkan bantuan.</li>
<li>Nama domain yang dikelola CSS dapat digunakan untuk melakukan push atau memutar ulang streaming langsung secara normal hanya jika nama domain sudah jadi. Informasi selengkapnya dapat dilihat di <a href="https://intl.cloud.tencent.com/document/product/267/31057">Configuring CNAME for Domain Name (Mengonfigurasikan CNAME untuk Nama Domain)</a>.</li></ul></td>
</tr><tr>
<td>Push langsung</td>
<td>Layanan CSS tidak membatasi bitrate push serta mendukung resolusi umum dan bitrate yang sesuai. Untuk mencegah lag pada push, sebaiknya gunakan bitrate di bawah 4 Mbps.</td>
</tr><tr>
<td>Pemutaran ulang langsung</td>
<td><ul style="margin:0">
	<li>Streaming dapat diputar ulang hanya jika `StreamName` alamat pemutaran ulang sama dengan `StreamName` alamat push.</li>
	<li>Tidak ada batasan untuk jumlah pemirsa streaming langsung. Anda dapat mengatur sendiri batas bandwidth untuk streaming langsung.</li>
	<li/>Jika memerlukan dukungan tambahan untuk lonjakan skala besar pada lalu lintas streaming langsung, Anda perlu mengirimkan tiket atau menghubungi perwakilan Tencent Cloud tiga hari kerja sebelumnya untuk mendapatkan bantuan. Lonjakan tersebut umumnya meliputi dua jenis sebagai berikut:<ul style="margin:0">
		<li/>Bandwidth puncak harian tiba-tiba melebihi 200 Gbps, dan lonjakannya sebesar 200% dari puncak harian.
		<li/>Bandwidth puncak harian tiba-tiba melebihi 500 Gbps.
	</ul>
</ul></td>
</tr><tr>
<td>Konfigurasi templat</td>
<td>Setelah templat berhasil diikat, penerapannya memerlukan waktu 5–10 menit.</td>
</tr><tr>
<td>Pergantian mode penagihan harian</td>
<td>Anda dapat memilih tagihan berdasarkan lalu lintas atau tagihan berdasarkan bandwidth untuk penagihan harian. Anda hanya dapat mengubah mode penagihan satu kali per hari, dan perubahan akan berlaku pada hari berikutnya.</td>
</tr><tr>
<td>Protokol push yang didukung</td>
<td>CSS mendukung protokol RTMP dan SRT. Informasi selengkapnya dapat dilihat di <a href="https://intl.cloud.tencent.com/document/product/267/7968">Live Streaming Basics (Penjelasan Dasar tentang Streaming Langsung)</a>.</td>
</tr><tr>
<td>Protokol pemutaran ulang yang didukung</td>
<td><ul style="margin:0">
	<li>CSS mendukung protokol pemutaran ulang RTMP, FLV, dan HLS. Informasi selengkapnya dapat dilihat di <a href="https://intl.cloud.tencent.com/document/product/267/7968">Live Streaming Basics (Penjelasan Dasar tentang Streaming Langsung)</a>.</li>
	<li>LEB mendukung protokol pemutaran ulang WebRTC.</li>
</ul></td>
</tr></table>


