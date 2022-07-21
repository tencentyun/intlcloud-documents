>? Anda dapat menggunakan [kalkulator harga CSS](https://buy.cloud.tencent.com/price/css/calculator) untuk menghitung perkiraan biaya LVB dan LEB.

Item CSS yang dapat dikenai tagihan meliputi layanan dasar dan layanan dengan nilai tambah. Biaya layanan tambahan akan dikenakan jika fitur bernilai tambah yang disediakan bersama oleh CSS dan layanan lain Tencent Cloud digunakan. Silakan lihat gambar berikut sebagai referensi.

![](https://main.qcloudimg.com/raw/0897e5dd41b3a2960a30b45cd9351b21.png)


- [Biaya layanan dasar](#base): dikenakan berdasarkan pemakaian sumber daya streaming langsung ketika LVB atau LEB digunakan. Anda dapat beralih antara mode penagihan lalu lintas dan mode penagihan bandwidth puncak.
- [Biaya layanan bernilai tambah](#appreciation): dikenakan ketika fitur bernilai tambah, misalnya transcoding, perekaman, pengambilan tangkapan layar, deteksi pornografi, dan relai, digunakan. Fitur-fitur tersebut dinonaktifkan secara default dan hanya dikenai biaya jika digunakan.
- [Biaya layanan tambahan](#extensions): dikenakan ketika fitur bernilai tambah yang disediakan bersama oleh CSS dan layanan lain Tencent Cloud digunakan. Setiap layanan Tencent Cloud akan dikenai biaya berdasarkan aturan penagihan masing-masing.

[](id:base)
## Biaya Layanan Dasar

Cara berbeda digunakan untuk penagihan biaya layanan dasar LVB dan LEB.

<table>
<tr><th width="20%">Item yang Dapat Dikenai Tagihan</th><th width="60%">Deskripsi</th><th>Mode Penagihan</th></tr>
<tr>
<td>Lalu lintas LVB<br> (default)</td>
<td>
<li/>Ditagih berdasarkan lalu lintas downstream dan upstream yang dihasilkan oleh push dan pull LVB. Secara default, penagihan akan dilakukan hanya untuk lalu lintas downstream.
<li/>Harga berbeda-beda untuk wilayah di dalam dan di luar Tiongkok Daratan.
</td>
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/2818">Bayar sesuai pemakaian harian</a></li>
<li/>Bayar sesuai pemakaian harian
</td>
</tr><tr>
<td>Bandwidth puncak LVB</td>
<td>
<li/>Ditagih berdasarkan bandwidth downstream dan upstream yang dihasilkan oleh push dan pull LVB. Secara default, penagihan akan dilakukan hanya untuk lalu lintas downstream.
<li/>Harga berbeda-beda untuk wilayah di dalam dan di luar Tiongkok Daratan.
</td><td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/2818">Bayar sesuai pemakaian harian</a></li>
<li/>Bayar sesuai pemakaian bulanan
</td>
</tr><tr>
<td>Lalu lintas LEB<br> (default)</td>
<td>
<li/>Ditagih berdasarkan lalu lintas downstream dan upstream yang dihasilkan oleh push dan pull LEB. Secara default, penagihan akan dilakukan hanya untuk lalu lintas downstream.
<li/>Harga berbeda-beda untuk wilayah di dalam dan di luar Tiongkok Daratan.
</td>
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39969">Bayar sesuai pemakaian harian</a></li>
<li/>Bayar sesuai pemakaian bulanan
</td>
</tr><tr>
<td>Bandwidth puncak LEB</td>
<td>
<li/>Ditagih berdasarkan bandwidth downstream dan upstream yang dihasilkan oleh push dan pull LEB. Secara default, penagihan akan dilakukan hanya untuk lalu lintas downstream.
<li/>Harga berbeda-beda untuk wilayah di dalam dan di luar Tiongkok Daratan.
</td>
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39969">Bayar sesuai pemakaian harian</a></li>
<li/>Bayar sesuai pemakaian bulanan
</td>
</tr></table>


>! 
>- Karena LEB menggunakan saluran dengan latensi ultra-rendah, biaya lalu lintas//bandwidth LEB sedikit lebih tinggi daripada biaya lalu lintas/bandwidth LVB.
>- CSS menyediakan mode penagihan bulanan untuk pelanggan dengan permintaan bulanan yang besar. Anda dapat menghubungi perwakilan penjualan untuk mengubah mode penagihan.
>- Anda dapat mengubah mode penagihan dengan mengikuti petunjuk di [Changing Billing Modes (Mengubah Mode Penagihan)](https://intl.cloud.tencent.com/document/product/267/30411).  


[](id:appreciation)
## Biaya Layanan dengan Nilai Tambah

<table>
<tr><th colspan=2 width="20%">Item yang Dapat Dikenai Tagihan</th><th width="60%">Deskripsi</th><th>Mode Penagihan</th></tr>
<tr>
<td rowspan=3>Transcoding langsung</td>
<td>Transcoding standar</td>
<td><ul style="margin:0">
<li/>Penggunaan transcoding langsung standar akan dikenai biaya.
<li/>Biaya transcoding standar akan dikenakan ketika <a href="https://intl.cloud.tencent.com/document/product/267/31064">pemberian watermark</a>, <a href="https://intl.cloud.tencent.com/document/product/267/31071">transcoding standar</a>, atau <a href="https://intl.cloud.tencent.com/document/product/267/37665">pencampuran streaming</a> digunakan selama streaming langsung.
<li/>Biaya yang dikenakan akan ditagih berdasarkan <b>durasi transcoding</b> menurut tingkat penagihan resolusi video streaming langsung output.
</ul></td>
<td>
  <li><a href="https://intl.cloud.tencent.com/document/product/267/39604">Bayar sesuai pemakaian harian</a></li></ul>
	<li/>Bayar sesuai pemakaian bulanan
</td>
</tr><tr>
<td>Transcoding codec kecepatan puncak</td>
<td><ul style="margin:0">
<li/>Penggunaan transcoding codec kecepatan tinggi selama streaming langsung akan dikenai biaya.
<li/>Biaya transcoding codec kecepatan tinggi akan dikenai biaya ketika <a href="https://intl.cloud.tencent.com/document/product/267/31071">transcoding codec kecepatan tinggi</a> digunakan.
<li/>Biaya yang dikenakan akan ditagih berdasarkan <b>durasi transcoding</b> menurut tingkat penagihan resolusi video streaming langsung output.
</ul><td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604">Bayar sesuai pemakaian harian</a></li>
<li/>Bayar sesuai pemakaian bulanan
</td>
</tr><tr>
<td>Transcoding audio</td>
<td>
<li/>Penggunaan transcoding audio selama streaming langsung akan dikenai biaya.
<li/>Biaya transcoding audio akan dikenakan ketika <a href="https://intl.cloud.tencent.com/document/product/267/31071">transcoding audio</a>, pencampuran streaming audio, atau pemisahan streaming audio/video digunakan.
<li/>Biaya ini akan ditagih berdasarkan <b>durasi transcoding audio</b>.
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604">Bayar sesuai pemakaian harian</a></li>
<li/>Bayar sesuai pemakaian bulanan
</td>
</tr><tr>
  <td colspan=2>Perekaman langsung</td>
  <td>
    <li>Selama perekaman langsung, file rekaman akan dibuat berdasarkan templat perekaman dan disimpan di dalam VOD.</li>
    <li>Biaya layanan yang dikenakan untuk perekaman langsung akan <b>ditagih berdasarkan jumlah puncak saluran perekaman langsung bersamaan</b>.</li>
  </td>
<td><a href = "https://intl.cloud.tencent.com/document/product/267/39605">Bayar sesuai pemakaian bulanan</a></td>
</tr><tr>
<td colspan=2>Tangkapan layar langsung</td>
<td>
  <li>Selama pengambilan tangkapan layar langsung, tangkapan layar streaming langsung akan diambil pada titik-titik waktu terjadwal sesuai dengan templat dan disimpan di dalam COS.</li>
  <li>Biaya layanan yang dikenakan untuk pengambilan tangkapan layar akan <b>ditagih berdasarkan jumlah tangkapan layar</b>. Sebanyak 1.000 tangkapan layar pertama setiap bulan tidak akan dikenai biaya.</li>
</td>
<td><a href = "https://intl.cloud.tencent.com/document/product/267/39606">Bayar sesuai pemakaian bulanan</a></td>
</tr><tr>
  <td colspan=2>Pengambilan tangkapan layar dan deteksi pornografi cerdas</td>
  <td>Fitur pengambilan tangkapan layar dan deteksi pornografi akan dikenai biaya secara terpisah.
    <li>Biaya layanan yang dikenakan untuk deteksi pornografi akan <b>ditagih berdasarkan jumlah tangkapan layar mengandung pornografi yang terdeteksi</b>. Sebanyak 1.000 tangkapan layar pertama setiap bulan tidak akan dikenai biaya.</li>
    <li>Biaya layanan yang dikenakan untuk pengambilan tangkapan layar akan <b>ditagih berdasarkan jumlah tangkapan layar</b>. Sebanyak 1.000 tangkapan layar pertama setiap bulan tidak akan dikenai biaya.</li>
</td>
<td><a href = "https://intl.cloud.tencent.com/document/product/267/39607">Bayar sesuai pemakaian bulanan</a></td>
</tr><tr>
<td colspan=2>Lisensi SDK MLVB</td>
<td>Dengan lisensi ini, Anda dapat menggunakan SDK MLVB edisi dasar di perangkat iOS dan Android. Anda dapat menghubungi tim penjualan untuk membeli lisensi ini.</td>
<td><a href="https://intl.cloud.tencent.com/contact-us">Hubungi tim penjualan</a></td>
</tr><tr>
<tr><td colspan=2>Relai</td>
<td>Ditagih berdasarkan durasi tugas relai</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/41059">Bayar sesuai pemakaian harian</a>
</td>
</tr><tr>
<td colspan=2>Push ke URL pihak ketiga</td>
<td>Push ke URL selain URL push CSS akun Tencent Cloud saat ini akan dikenai biaya push ke URL pihak ketiga.</td>
<td>
<a href = "https://intl.cloud.tencent.com/document/product/267/41059">Bayar sesuai pemakaian bulanan</a>
</td>
</tr>
</table>



[](id:extensions)

## Biaya Layanan Tambahan

<table>
<tr><th width="20%">Item yang Dapat Dikenai Tagihan</th><th width="60%">Deskripsi</th><th>Mode Penagihan</th></tr>
<tr>
<td>Penyimpanan rekaman</td>
<td>File rekaman yang dihasilkan oleh perekaman langsung harus disimpan di dalam VOD. Biaya layanan yang dikenakan akan <b>ditagih berdasarkan durasi penyimpanan dan volume data aktual</b>. Anda akan dikenai tagihan untuk penyimpanan VOD secara terpisah.
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/39506">Bayar sesuai pemakaian VOD</a></td>
</tr><tr>
<td>Penyimpanan tangkapan layar</td>
<td>File tangkapan layar yang dihasilkan pengambilan tangkapan layar dan deteksi pornografi langsung harus disimpan di dalam COS. Biaya layanan yang dikenakan akan <strong>ditagih berdasarkan durasi penyimpanan dan volume data aktual</strong>. Anda akan dikenai tagihan untuk penyimpanan COS secara terpisah.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">Bayar sesuai pemakaian COS</a></td>
</tr></table>
