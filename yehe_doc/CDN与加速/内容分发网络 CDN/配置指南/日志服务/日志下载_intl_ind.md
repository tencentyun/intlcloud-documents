## Ikhtisar Fitur

Setelah nama domain terhubung ke CDN, semua permintaan akan dijadwalkan ke simpul CDN. Jika sumber daya yang diminta di-cache pada simpul, sumber daya akan dikembalikan secara langsung; jika tidak, permintaan akan diteruskan ke server asal untuk menarik sumber daya yang diminta.

Saat simpul CDN merespons sebagian besar permintaan pengguna, untuk membantu Anda menganalisis akses pengguna, CDN mengemas log akses seluruh jaringan dengan perincian per jam dan menyimpannya selama 30 hari secara default. Log ini juga dapat diunduh.

>? 
>- Saat ini, log tarik-asal tidak disediakan. Hanya log akses simpul yang disediakan.
>- Log offline nama domain ECDN tidak dapat dikueri berdasarkan wilayah untuk saat ini. Untuk informasi selengkapnya, lihat [Pengelolaan Log](https://intl.cloud.tencent.com/document/product/570/15258).

## Ikhtisar
### Analisis perilaku akses
Anda dapat mengunduh log akses dan menganalisis sumber daya populer dan pengguna aktif.

### Pemantauan kualitas layanan
Dengan mengunduh log akses, Anda dapat tetap mengetahui status layanan semua simpul CDN dan menghitung waktu respons rata-rata, kecepatan unduhan rata-rata, dan metrik lainnya.

## Petunjuk
### Cara penggunaan
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), klik **Log Service** (Layanan Log) di bilah samping kiri, lalu pilih nama domain dan rentang waktu untuk menanyakan log akses. Anda dapat memilih beberapa paket log dan mengunduhnya dalam batch:

>!
>- Log akses disimpan dalam paket berdasarkan jam secara default. Jika tidak ada permintaan ke nama domain untuk jam tersebut, tidak ada paket log yang akan dibuat untuk jam ini.
>- Untuk nama domain yang sama, log akses dari dalam dan luar Tiongkok Daratan disimpan dalam paket secara terpisah. Paket log diberi nama dalam format "[waktu]-[nama domain]-[wilayah akselerasi]".
>- Log akses dikumpulkan dari setiap simpul cache CDN sehingga penundaan dapat berbeda. Umumnya, paket log dapat dikueri dan diunduh setelah sekitar 30 menit. Paket log akan ditambahkan terus menerus dan akan stabil setelah 2-3 jam.
>- Paket log akses dari nama domain disimpan selama 30 hari. Anda dapat menggunakan fungsi SCF untuk mentransfer paket log ke COS seperti yang diinstruksikan di [Menyimpan Log CDN Secara Teratur](https://intl.cloud.tencent.com/zh/document/product/228/36014) untuk penyimpanan permanen.

### Bidang
Bidang (dari kiri ke kanan) dalam log terdaftar sebagai berikut:
<table style="width:660px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">No.</th>
<th align="left" style="width:560px;font-weight:700">Bidang  </th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>Waktu permintaan</td>
</tr>
</tbody>
<tbody><tr>
<td>2</td>
<td>IP Klien</td>
</tr>
</tbody>
<tbody><tr>
<td>3</td>
<td>Nama domain</td>
</tr>
</tbody>
<tbody><tr>
<td>4</td>
<td>Jalur permintaan</td>
</tr>
</tbody>
<tbody><tr>
<td>5</td>
<td>Jumlah byte yang diakses saat ini, termasuk ukuran file itu sendiri dan ukuran header permintaan.</td>
</tr>
</tbody>
<tbody><tr>
<td>6</td>
<td>Nomor provinsi untuk log Tiongkok Daratan; nomor wilayah untuk log di luar Tiongkok Daratan (lihat tabel pemetaan di bawah).</td>
</tr>
</tbody>
<tbody><tr>
<td>7</td>
<td>Nomor ISP untuk log Tiongkok Daratan; `-1` akan digunakan untuk log di luar Tiongkok Daratan (lihat tabel pemetaan di bawah).</td>
</tr>
</tbody>
<tbody><tr>
<td>8</td>
<td>Kode status HTTP</td>
</tr>
</tbody>
<tbody><tr>
<td>9</td>
<td>Informasi referer</td>
</tr>
</tbody>
<tbody><tr>
<td>10</td>
<td>Waktu respons (dalam milidetik), yang mengacu pada waktu yang diperlukan simpul untuk mengembalikan semua paket ke klien setelah menerima permintaan.</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>11</td>
<td>Informasi User-Agent</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>12</td>
<td>Parameter rentang</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>13</td>
<td>Metode HTTP</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>14</td>
<td>Pengidentifikasi protokol HTTP</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>15</td>
<td>Cache hit/miss. Hit di server edge CDN atau simpul induk akan ditandai sebagai hit.</td>
</tr>
<td>16</td>
<td>Port yang menghubungkan klien dan simpul CDN. Nilainya adalah <code> -</code> jika tidak ada port. </td>
</tr>
</tbody></table>

### Pemetaan Wilayah/ISP

[](id:.E7.9C.81.E4.BB.BD.E6.98.A0.E5.B0.84)
#### Provinsi Tiongkok Daratan
<table style="width:660px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">ID Wilayah</th>
<th align="left" style="width:120px;font-weight:700">Wilayah</th>
<th align="left" style="width:100px;font-weight:700">ID Wilayah</th>
<th align="left" style="width:120px;font-weight:700">Wilayah</th>
<th align="left" style="width:100px;font-weight:700">ID Wilayah</th>
<th align="left" style="width:120px;font-weight:700">Wilayah</th>
</tr>
</thead>
<tbody><tr>
<td>22</td>
<td>Beijing</td>
<td>86</td>
<td>Mongolia Dalam</td>
<td>146</td>
<td>Shanxi</td>
</tr>
<tr>
<td>1069</td>
<td>Hebei</td>
<td>1177</td>
<td>Tianjin</td>
<td>119</td>
<td>Ningxia</td>
</tr>
<tr>
<td>152</td>
<td>Shaanxi</td>
<td>1208</td>
<td>Gansu</td>
<td>1467</td>
<td>Qinghai</td>
</tr>
<tr>
<td>1468</td>
<td>Xinjiang</td>
<td>145</td>
<td>Heilongjiang</td>
<td>1445</td>
<td>Jilin</td>
</tr>
<tr>
<td>1464</td>
<td>Liaoning</td>
<td>2</td>
<td>Fujian</td>
<td>120</td>
<td>Jiangsu</td>
</tr>
<tr>
<td>121</td>
<td>Anhui</td>
<td>122</td>
<td>Shandong</td>
<td>1050</td>
<td>Shanghai</td>
</tr>
<tr>
<td>1442</td>
<td>Zhejiang</td>
<td>182</td>
<td>Henan</td>
<td>1135</td>
<td>Hubei</td>
</tr>
<tr>
<td>1465</td>
<td>Jiangxi</td>
<td>1466</td>
<td>Hunan</td>
<td>118</td>
<td>Guizhou</td>
</tr>
<tr>
<td>153</td>
<td>Yunnan</td>
<td>1051</td>
<td>Chongqing</td>
<td>1068</td>
<td>Sichuan</td>
</tr>
<tr>
<td>1155</td>
<td>Tibet</td>
<td>4</td>
<td>Guangdong</td>
<td>173</td>
<td>Guangxi</td>
</tr>
<tr>
<td>1441</td>
<td>Hainan</td>
<td>0</td>
<td>Lainnya</td>
<td>1</td>
<td>Hong Kong (Tiongkok), Makau (Tiongkok), dan Taiwan (Tiongkok)</td>
</tr>
<tr>
<td>-1</td>
<td>Di luar Tiongkok Daratan</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody></table>


#### ISP Tiongkok Daratan
<table style="width:660px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">ID ISP</th>
<th align="left" style="width:120px;font-weight:700">ISP</th>
<th align="left" style="width:100px;font-weight:700">ID ISP</th>
<th align="left" style="width:120px;font-weight:700">ISP</th>
<th align="left" style="width:100px;font-weight:700">ID ISP</th>
<th align="left" style="width:120px;font-weight:700">ISP</th>
</tr>
</thead>
<tbody><tr>
<td>2</td>
<td>China Telecom</td>
<td>26</td>
<td>China Unicom</td>
<td>38</td>
<td>CERNET</td>
</tr>
</tbody>
<tbody><tr>
<td>43</td>
<td>Great Wall Broadband Network</td>
<td>1046</td>
<td>China Mobile</td>
<td>3947</td>
<td>China Mobile Tietong</td>
</tr>
</tbody>
<tbody><tr>
<td>-1</td>
<td>ISP di luar Tiongkok Daratan</td>
<td>0</td>
<td>ISP Lainnya</td>
<td></td>
<td></td>
</tr>
</tbody>
</table>


#### Wilayah di luar Tiongkok Daratan
<table style="width:710px">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">ID Wilayah</th>
<th align="left" style="width:170px;font-weight:700">Wilayah</th>
<th align="left" style="width:100px;font-weight:700">ID Wilayah</th>
<th align="left" style="width:120px;font-weight:700">Wilayah</th>
<th align="left" style="width:100px;font-weight:700">ID Wilayah</th>
<th align="left" style="width:120px;font-weight:700">Wilayah</th>
</tr>
</thead>
<tbody><tr>
<td>2000000001</td>
<td>Zona Asia Pasifik 1 (area layanan)</td>
<td>765</td>
<td>Slowakia</td>
<td>1613</td>
<td>Angola</td>
</tr>
<tr>
<td>2000000002</td>
<td>Zona Asia Pasifik 2 (area layanan)</td>
<td>766</td>
<td>Serbia</td>
<td>1617</td>
<td>Pantai Gading</td>
</tr>
<tr>
<td>2000000003</td>
<td>Zona Asia Pasifik 3 (area layanan)</td>
<td>770</td>
<td>Finlandia</td>
<td>1620</td>
<td>Sudan</td>
</tr>
<tr>
<td>2000000004</td>
<td>Timur Tengah (area layanan)</td>
<td>773</td>
<td>Belgia</td>
<td>1681</td>
<td>Mauritius</td>
</tr>
<tr>
<td>2000000005</td>
<td>Amerika Utara (area layanan)</td>
<td>809</td>
<td>Bulgaria</td>
<td>1693</td>
<td>Maroko</td>
</tr>
<tr>
<td>2000000006</td>
<td>Eropa (area layanan)</td>
<td>811</td>
<td>Slovenia</td>
<td>1695</td>
<td>Algeria</td>
</tr>
<tr>
<td>2000000007</td>
<td>Amerika Selatan (area layanan)</td>
<td>812</td>
<td>Moldova</td>
<td>1698</td>
<td>Guinea</td>
</tr>
<tr>
<td>2000000008</td>
<td>Afrika (area layanan)</td>
<td>813</td>
<td>Makedonia</td>
<td>1730</td>
<td>Senegal</td>
</tr>
<tr>
<td>-20</td>
<td>Asia (area klien)</td>
<td>824</td>
<td>Estonia</td>
<td>1864</td>
<td>Tunisia</td>
</tr>
<tr>
<td>-21</td>
<td>Amerika Selatan (area klien)</td>
<td>835</td>
<td>Kroasia</td>
<td>1909</td>
<td>Uruguay</td>
</tr>
<tr>
<td>-22</td>
<td>Amerika Utara (area klien)</td>
<td>837</td>
<td>Polandia</td>
<td>1916</td>
<td>Greenland</td>
</tr>
<tr>
<td>-23</td>
<td>Eropa (area klien)</td>
<td>852</td>
<td>Latvia</td>
<td>2026</td>
<td>Taiwan (Tiongkok)</td>
</tr>
<tr>
<td>-24</td>
<td>Afrika (area klien)</td>
<td>857</td>
<td>Yordania</td>
<td>2083</td>
<td>Myanmar</td>
</tr>
<tr>
<td>-25</td>
<td>Oseania (area klien)</td>
<td>884</td>
<td>Kirgistan</td>
<td>2087</td>
<td>Brunei</td>
</tr>
<tr>
<td>35</td>
<td>Nepal</td>
<td>896</td>
<td>Irlandia</td>
<td>2094</td>
<td>Sri Lanka</td>
</tr>
<tr>
<td>57</td>
<td>Thailand</td>
<td>901</td>
<td>Libya</td>
<td>2150</td>
<td>Panama</td>
</tr>
<tr>
<td>73</td>
<td>India</td>
<td>904</td>
<td>Armenia</td>
<td>2175</td>
<td>Kolombia</td>
</tr>
<tr>
<td>144</td>
<td>Vietnam</td>
<td>921</td>
<td>Yaman</td>
<td>2273</td>
<td>Monako</td>
</tr>
<tr>
<td>192</td>
<td>Prancis</td>
<td>926</td>
<td>Belarus</td>
<td>2343</td>
<td>Andorra</td>
</tr>
<tr>
<td>207</td>
<td>Britania Raya</td>
<td>971</td>
<td>Luksemburg</td>
<td>2421</td>
<td>Turkmenistan</td>
</tr>
<tr>
<td>208</td>
<td>Swedia</td>
<td>1036</td>
<td>Selandia Baru</td>
<td>2435</td>
<td>Laos</td>
</tr>
<tr>
<td>209</td>
<td>Jerman</td>
<td>1044</td>
<td>Jepang</td>
<td>2488</td>
<td>Timor Timur</td>
</tr>
<tr>
<td>213</td>
<td>Italia</td>
<td>1066</td>
<td>Pakistan</td>
<td>2490</td>
<td>Tonga</td>
</tr>
<tr>
<td>214</td>
<td>Spanyol</td>
<td>1070</td>
<td>Malta</td>
<td>2588</td>
<td>Filipina</td>
</tr>
<tr>
<td>386</td>
<td>Uni Emirat Arab</td>
<td>1091</td>
<td>Bahama</td>
<td>2609</td>
<td>Venezuela</td>
</tr>
<tr>
<td>391</td>
<td>Israel</td>
<td>1129</td>
<td>Argentina</td>
<td>2612</td>
<td>Bolivia</td>
</tr>
<tr>
<td>397</td>
<td>Ukraina</td>
<td>1134</td>
<td>Bangladesh</td>
<td>2613</td>
<td>Brazil</td>
</tr>
<tr>
<td>-</td>
<td>-</td>
<td>1158</td>
<td>Kamboja</td>
<td>2623</td>
<td>Kosta Rika</td>
</tr>
<tr>
<td>417</td>
<td>Kazakhstan</td>
<td>1159</td>
<td>Makau (Tiongkok)</td>
<td>2626</td>
<td>Meksiko</td>
</tr>
<tr>
<td>428</td>
<td>Portugal</td>
<td>1176</td>
<td>Singapura</td>
<td>2639</td>
<td>Honduras</td>
</tr>
<tr>
<td>443</td>
<td>Yunani</td>
<td>1179</td>
<td>Maladewa</td>
<td>2645</td>
<td>El Salvador</td>
</tr>
<tr>
<td>471</td>
<td>Arab Saudi</td>
<td>1180</td>
<td>Afghanistan</td>
<td>2647</td>
<td>Paraguay</td>
</tr>
<tr>
<td>529</td>
<td>Denmark</td>
<td>1185</td>
<td>Fiji</td>
<td>2661</td>
<td>Peru</td>
</tr>
<tr>
<td>565</td>
<td>Iran</td>
<td>1186</td>
<td>Mongolia</td>
<td>2728</td>
<td>Nikaragua</td>
</tr>
<tr>
<td>578</td>
<td>Norwegia</td>
<td>1195</td>
<td>Indonesia</td>
<td>2734</td>
<td>Ekuador</td>
</tr>
<tr>
<td>669</td>
<td>Amerika Serikat</td>
<td>1200</td>
<td>Hong Kong (Tiongkok)</td>
<td>2768</td>
<td>Guatemala</td>
</tr>
<tr>
<td>692</td>
<td>Suriah</td>
<td>1233</td>
<td>Qatar</td>
<td>2999</td>
<td>Aruba</td>
</tr>
<tr>
<td>704</td>
<td>Siprus</td>
<td>1255</td>
<td>Islandia</td>
<td>3058</td>
<td>Etiopia</td>
</tr>
<tr>
<td>706</td>
<td>Ceko</td>
<td>1289</td>
<td>Albania</td>
<td>3144</td>
<td>Bosnia dan Herzegovina</td>
</tr>
<tr>
<td>707</td>
<td>Swiss</td>
<td>1353</td>
<td>Uzbekistan</td>
<td>3216</td>
<td>Dominika</td>
</tr>
<tr>
<td>708</td>
<td>Irak</td>
<td>1407</td>
<td>San Marino</td>
<td>3379</td>
<td>Korea Selatan</td>
</tr>
<tr>
<td>714</td>
<td>Belanda</td>
<td>1416</td>
<td>Kuwait</td>
<td>3701</td>
<td>Malaysia</td>
</tr>
<tr>
<td>717</td>
<td>Rumania</td>
<td>1417</td>
<td>Montenegro</td>
<td>3839</td>
<td>Kanada</td>
</tr>
<tr>
<td>721</td>
<td>Lebanon</td>
<td>1493</td>
<td>Tajikistan</td>
<td>4450</td>
<td>Australia</td>
</tr>
<tr>
<td>725</td>
<td>Hongaria</td>
<td>1501</td>
<td>Bahrain</td>
<td>4460</td>
<td>Tiongkok Daratan</td>
</tr>
<tr>
<td>726</td>
<td>Georgia</td>
<td>1543</td>
<td>Chili</td>
<td>-15</td>
<td>Asia - lainnya</td>
</tr>
<tr>
<td>731</td>
<td>Azerbaijan</td>
<td>1559</td>
<td>Afrika Selatan</td>
<td>-14</td>
<td>Amerika Selatan - lainnya</td>
</tr>
<tr>
<td>734</td>
<td>Austria</td>
<td>1567</td>
<td>Mesir</td>
<td>-13</td>
<td>Amerika Utara - lainnya</td>
</tr>
<tr>
<td>736</td>
<td>Palestina</td>
<td>1590</td>
<td>Kenya</td>
<td>-12</td>
<td>Eropa - lainnya</td>
</tr>
<tr>
<td>737</td>
<td>Turki</td>
<td>1592</td>
<td>Nigeria</td>
<td>-11</td>
<td>Afrika - lainnya</td>
</tr>
<tr>
<td>759</td>
<td>Lituania</td>
<td>1598</td>
<td>Tanzania</td>
<td>-10</td>
<td>Oseania - lainnya</td>
</tr>
<tr>
<td>763</td>
<td>Oman</td>
<td>1611</td>
<td>Madagaskar</td>
<td>-2</td>
<td>Di luar Tiongkok Daratan - lainnya</td>
</tr>
</tbody></table>


#### ISP di luar Tiongkok Daratan
<table style="width:220px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">ID ISP</th>
<th align="left" style="width:120px;font-weight:700">ISP</th>
</tr>
</thead>
<tbody><tr>
<td>-1</td>
<td>ISP di luar Tiongkok Daratan</td>
</tr>
</tbody>
</table>

### Catatan
Data lalu lintas/bandwidth yang dihitung berdasarkan jumlah byte yang direkam di bidang kelima dari log akses berbeda dari data lalu lintas/bandwidth CDN yang dapat ditagih karena alasan berikut:
- Hanya data lapisan aplikasi yang dapat direkam dalam log akses. Lalu lintas yang dihasilkan selama transfer data aktual melalui jaringan sekitar 5 hingga 15% lebih banyak dari lalu lintas lapisan aplikasi, termasuk dua bagian berikut:
	- Konsumsi oleh header TCP/IP: dalam permintaan HTTP berbasis TCP/IP, setiap paket memiliki ukuran maksimum 1.500 byte. Ini termasuk header TCP dan IP yang berjumlah 40 byte dan menghasilkan lalu lintas selama transfer tetapi tidak dapat dihitung oleh lapisan aplikasi. Overhead bagian ini adalah sekitar 3%.
	- Transmisi ulang TCP: selama transfer data normal melalui jaringan, sekitar 3% hingga 10% paket hilang di internet dan dikirim ulang oleh server. Jenis lalu lintas ini tidak dapat dihitung oleh lapisan aplikasi, yang berjumlah 3% hingga 7% dari total lalu lintas.
- Sesuai standar industri, lalu lintas yang dapat ditagih adalah jumlah lalu lintas lapisan aplikasi dan biaya overhead yang dijelaskan di atas. CDN Tencent Cloud mengambil 10% sebagai proporsi overhead sehingga lalu lintas yang dipantau adalah sekitar 110% dari lalu lintas yang dicatat.

## Kasus Penggunaan

### Sampel log akses Tiongkok Daratan
![](https://mc.qcloudimg.com/static/img/a3ef1ea051dc277872ec10a7135872df/logs.png)

### Sampel log akses di luar Tiongkok Daratan
![](https://main.qcloudimg.com/raw/b0612a5204abdbdc6a4364ad02972900.png)
