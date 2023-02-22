## Wilayah
Wilayah adalah lokasi fisik dari IDC.Di Tencent Cloud, wilayah sepenuhnya terisolasi satu sama lain, memastikan stabilitas lintas wilayah dan toleransi kesalahan.Saat membeli layanan Tencent Cloud, sebaiknya pilih wilayah yang paling dekat dengan pengguna akhir Anda untuk meminimalkan latensi akses dan meningkatkan kecepatan unduh.
Wilayah memiliki ciri-ciri sebagai berikut:

- Jaringan dari berbagai wilayah sepenuhnya terisolasi.Layanan Tencent Cloud di berbagai wilayah **tidak dapat berkomunikasi melalui jaringan pribadi secara default**.
- Layanan Tencent Cloud di seluruh wilayah dapat berkomunikasi satu sama lain melalui [IP publik](https://intl.cloud.tencent.com/document/product/213/5224) melalui Internet, sedangkan layanan di VPC dapat menggunakan koneksi peering untuk berkomunikasi satu sama lain melalui jaringan berkecepatan tinggi Tencent Cloud, yang lebih cepat dan stabil.
- [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) saat ini mendukung penerusan traffic intra-wilayah secara default.Jika Anda mengaktifkan fitur [pengikatan lintas wilayah](https://intl.cloud.tencent.com/document/product/214/12014), instance CLB dapat diikat ke instance CVM di wilayah lain.


## Zona Ketersediaan
Zona ketersediaan (AZ) adalah IDC fisik Tencent Cloud dengan catu daya dan jaringan independen di wilayah yang sama.Ini dapat memastikan stabilitas bisnis, karena kegagalan (kecuali untuk bencana besar atau pemadaman listrik) di satu AZ yang diisolasi tanpa memengaruhi AZ lain di wilayah yang sama.Dengan memulai instance di zona ketersediaan independen, pengguna dapat melindungi aplikasi mereka agar tidak terpengaruh oleh satu titik kegagalan.
Zona ketersediaan memiliki karakteristik sebagai berikut:
- Layanan Tencent Cloud di bawah akun yang sama di [VPC](https://intl.cloud.tencent.com/document/product/215) yang sama saling terhubung melalui jaringan privat, artinya layanan tersebut dapat berkomunikasi menggunakan [IP privat]( https://intl.cloud.tencent.com/document/product/213/5225), meskipun layanan tersebut berada di zona ketersediaan yang berbeda di wilayah yang sama.
- Sumber daya di bawah akun Tencent Cloud yang berbeda adalah khusus zona ketersediaan, artinya sumber daya tersebut tidak dapat berkomunikasi melalui jaringan privat, meskipun berada di wilayah yang sama.

[](id:MainlandChina)
## Tiongkok
<table class="table-striped">
<tbody>
<tr>
<th>Wilayah</th>
<th>AZ</th>
</tr>
<tr>
<td rowspan="5">Tiongkok Selatan (Guangzhou)<br>ap-guangzhou</td>
<td>Zona Guangzhou 1 (terjual habis)<br>ap-guangzhou-1</td>
</tr>
<tr>
<td>Zona Guangzhou 2 (terjual habis)<br>ap-guangzhou-2</td>
</tr>
<tr>
<td>Zona Guangzhou 3 <br>ap-guangzhou-3</td>
</tr>
<tr>
<td>Zona Guangzhou 4 <br>ap-guangzhou-4</td>
</tr>
<tr>
<td>Zona Guangzhou 6 <br>ap-guangzhou-6</td>
</tr>

<tr>
<td rowspan="5">Tiongkok Timur (Shanghai)<br>ap-shanghai</td>
<td>Zona Shanghai 1 <br>ap-shanghai-1</td>
</tr>
<tr>
<td>Zona Shanghai 2 <br>ap-shanghai-2</td>
</tr>
<tr>
<td>Zona Shanghai 3 <br>ap-shanghai-3</td>
</tr>
<tr>
<td>Zona Shanghai 4 <br>ap-shanghai-4</td>	
</tr>
<tr>
<td>Zona Shanghai 5 <br>ap-shanghai-5</td>
</tr>
	
<tr>
<td rowspan="3">Tiongkok Timur (Nanjing)<br>ap-nanjing</td>
<td>Zona Nanjing 1 <br>ap-nanjing-1</td>
</tr>
<tr>
<td>Zona Nanjing 2 <br>ap-nanjing-2</td>
</tr>
<tr>
<td>Zona Nanjing 3 <br>ap-nanjing-3</td>
</tr>
<tr>
<td rowspan="7">Tiongkok Utara (Beijing)<br>ap-beijing</td>
<td>Zona Beijing 1 <br>ap-beijing-1</td>
</tr>
<tr>
<td>Zona Beijing 2 <br>ap-beijing-2</td>
</tr>
<tr>
<td>Zona Beijing 3 <br>ap-beijing-3</td>
</tr>
<tr>
<td>Zona Beijing 4 <br>ap-beijing-4</td>
</tr>
<tr>
<td>Zona Beijing 5 <br>ap-beijing-5</td>
</tr>
<tr>
<td>Zona Beijing 6 <br>ap-beijing-6</td>
</tr>
<tr>
<td>Zona Beijing 7 <br>ap-beijing-7</td>
</tr>
<tr>
<td rowspan="2">Tiongkok Barat Daya (Chengdu)<br>ap-chengdu</td>
<td>Zona Chengdu 1<br>ap-chengdu-1</td>
</tr>
<tr>
<td>Zona Chengdu 2<br>ap-chengdu-2</td>
</tr>
<tr>
<td >Tiongkok Barat Daya (Chongqing)<br>ap-chongqing</td>
<td>Zona Chongqing 1<br>ap-chongqing-1</td>
</tr>
<tr>
<td rowspan="3">Hong Kong, Makau dan Taiwan, Tiongkok (Hong Kong)<br>ap-hongkong</td>
<td>Zona Hong Kong 1 (Simpul di Hong Kong, Tiongkok dapat mencakup wilayah Hong Kong/Makau/Taiwan)<br>ap-hongkong-1</td>
</tr>
<tr>
<td>Zona Hong Kong 2 (Simpul di Hong Kong, Tiongkok dapat mencakup wilayah Hong Kong/Makau/Taiwan)<br>ap-hongkong-2</td>
</tr>
<tr>
<td>Zona Hong Kong 3 (Simpul di Hong Kong, Tiongkok dapat mencakup wilayah Hong Kong/Makau/Taiwan)<br>ap-hongkong-3</td>
</tr>
</tbody>
</table>

[](id:InternationalArea)
## Negara dan Wilayah Lain
<table class="table-striped">
<tbody>
<tr>
<th>Wilayah</th>
<th>AZ</th>
</tr>
<tr>
<td  rowspan="2">Asia Tenggara (Singapura)<br>ap-singapore</td>
<td>Zona Singapura 1 (Simpul di Singapura dapat mencakup Asia Tenggara)<br>ap-singapore-1</td>
</tr>
<tr>
<td>Zona Singapura 2 (Simpul di Singapura dapat mencakup Asia Tenggara)<br>ap-singapore-2</td>
</tr>
<tr>
<td>Asia Tenggara (Jakarta)<br>ap-jakarta</td>
<td>Zona Jakarta 1 (Simpul di Jakarta dapat mencakup Asia Tenggara)<br>ap-jakarta-1</td>
</tr>
<tr>
<td  rowspan="2">Asia Timur Laut (Seoul)<br>ap-seoul</td>
<td>Zona Seoul 1 (Simpul di Seoul dapat mencakup Asia Timur Laut)<br>ap-seoul-1</td>
</tr>
<tr>
<td>Zona Seoul 2 (Simpul di Seoul dapat mencakup Asia Timur Laut)<br>ap-seoul-2</td>
</tr>
<tr>
<td rowspan="2">Asia Timur Laut (Tokyo)<br>ap-tokyo</td>
<td>Zona Tokyo 1 (Simpul di Tokyo dapat mencakup Asia Timur Laut)<br>ap-tokyo-1</td>
</tr>
<tr>
<td>Zona Tokyo 2 (Simpul di Tokyo dapat mencakup Asia Timur Laut)<br>ap-tokyo-2</td>
</tr>
<tr>
<td  rowspan="2">Asia Selatan (Mumbai)<br>ap-mumbai</td>
<td>Zona Mumbai 1 (Simpul di Mumbai dapat mencakup Asia Selatan)<br>ap-mumbai-1</td>
</tr>
<tr>
<td>Zona Mumbai 2 (Simpul di Mumbai dapat mencakup Asia Selatan) <br>ap-mumbai-2</td>
</tr>
<tr>
<td >Asia Tenggara (Bangkok)<br>ap-bangkok </td>
<td >Zona Bangkok 1 (Simpul di Bangkok dapat mencakup Asia Tenggara)<br>ap-bangkok-1</td>
<tr>
<td>Amerika Utara (Toronto)<br>na-toronto</td>
<td>Zona Toronto 1 (Simpul di Toronto dapat mencakup Amerika Utara)<br>na-toronto-1</td>
</tr>
<tr>
<td rowspan="2">AS Barat (Silicon Valley)<br>na-siliconvalley</td>
<td>Zona Silicon Valley 1 (Simpul di Silicon Valley dapat mencakup AS Barat)<br>na-siliconvalley-1</td>
</tr>
<tr>
<td>Zona Silicon Valley 2 (Simpul di Silicon Valley dapat mencakup AS Barat)<br>na-siliconvalley-2</td>
</tr>
<tr>
<td rowspan="2">AS Timur (Virginia)<br>na-ashburn</td>
<td>Zona Virginia 1 (Simpul di Virginia dapat mencakup AS Timur)<br>na-ashburn-1</td>
</tr>
<tr>
<td>Zona Virginia 2 (Simpul di Virginia dapat mencakup AS Timur)<br>na-ashburn-2</td>
</tr>
<tr>
<td rowspan="2">Eropa (Frankfurt)<br>eu-frankfurt</td>
<td>Zona Frankfurt 1 (Simpul di Frankfurt dapat mencakup Eropa)<br>eu-frankfurt-1</td>
</tr>
<tr>
<td>Zona Frankfurt 2 (Simpul di Frankfurt dapat mencakup Eropa)<br>eu-frankfurt-2</td>
</tr>
<td >Eropa (Moskow)<br>eu-moscow</td>
<td>Zona Moskow 1 (Simpul di Moskow dapat mencakup Eropa)<br>eu-moscow-1</td>
</tr>
</tbody>
</table>

## Cara Memilih Wilayah dan Zona Ketersediaan
Saat memilih wilayah dan zona ketersediaan, pertimbangkan hal berikut:
- Sebuah disk cloud hanya dapat dilampirkan ke CVM di zona ketersediaan yang sama.
- Wilayah CVM tempat disk cloud akan digunakan, lokasi Anda, dan lokasi pengguna Anda.Kami menyarankan Anda memilih wilayah yang paling dekat dengan pengguna akhir Anda saat membeli layanan Tencent Cloud untuk meminimalkan latensi akses dan meningkatkan kecepatan akses.
- Hubungan antara CVM tempat disk cloud akan digunakan dan layanan Tencent Cloud lainnya.Saat Anda memilih layanan Tencent Cloud lainnya, kami menyarankan Anda untuk mencoba menempatkan semuanya di zona ketersediaan yang sama dari satu wilayah untuk memungkinkan layanan tersebut berkomunikasi satu sama lain melalui jaringan privat, mengurangi latensi akses dan meningkatkan kecepatan akses.
- Ketersediaan tinggi dan pemulihan bencana.Meskipun Anda hanya memiliki satu VPC, kami tetap menyarankan agar Anda men-deploy bisnis Anda di zona ketersediaan yang berbeda untuk mencegah satu titik kegagalan dan mengaktifkan pemulihan bencana lintas-AZ.
- Mungkin ada latensi jaringan di antara zona ketersediaan yang berbeda.Sebaiknya Anda menilai kebutuhan bisnis Anda dan menemukan keseimbangan optimal antara ketersediaan tinggi dan latensi rendah.

## Operasi yang Relevan
Tindakan seperti penggunaan dan tampilan disk cloud bersifat khusus wilayah.Untuk memigrasikan data dan layanan ke wilayah lain dengan mudah atau membangun sistem pemulihan bencana lintas wilayah, Anda dapat menyalin snapshot ke wilayah lain.Untuk informasi selengkapnya, lihat [Mereplikasi Snapshot Lintas Wilayah](https://intl.cloud.tencent.com/document/product/362/31623).
