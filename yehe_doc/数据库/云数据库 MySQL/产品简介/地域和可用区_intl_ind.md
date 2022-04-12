Pusat data TencentDB di-host di beberapa lokasi di seluruh dunia. Lokasi-lokasi ini dikenal sebagai wilayah. Setiap wilayah berisi beberapa zona ketersediaan (AZ).
Setiap wilayah adalah wilayah geografis independen yang berisi beberapa AZ yang terisolasi. AZ terpisah di wilayah yang sama terhubung melalui jaringan pribadi dengan latensi rendah. Tencent Cloud memberi Anda kemampuan untuk mendistribusikan sumber daya Tencent Cloud di berbagai lokasi. Sebaiknya tempatkan sumber daya di AZ yang berbeda untuk menghilangkan satu titik kegagalan yang dapat menyebabkan tidak tersedianya layanan.

Nama wilayah dan nama AZ dapat secara langsung mewujudkan cakupan pusat data. Konvensi penamaan berikut digunakan untuk kenyamanan Anda:
- Nama wilayah terdiri dari **region + city** (wilayah + kota). `region` menunjukkan area geografis yang dicakup oleh pusat data, sedangkan `city` mewakili kota di dalam atau di dekat pusat data tersebut.
- Nama AZ menggunakan format **city + number** (kota + nomor).

## Wilayah
Wilayah Tencent Cloud benar-benar terisolasi. Ini menjamin stabilitas lintas wilayah maksimum dan toleransi kesalahan. Saat membeli layanan Tencent Cloud, sebaiknya pilih wilayah yang paling dekat dengan pengguna akhir Anda untuk meminimalkan latensi akses dan meningkatkan kecepatan pengunduhan. Operasi seperti meluncurkan atau melihat instans dilakukan di tingkat wilayah.
Komunikasi jaringan pribadi:

- Sumber daya Tencent Cloud di VPC yang sama dalam wilayah yang sama di bawah akun yang sama dapat berkomunikasi satu sama lain melalui jaringan pribadi. Mereka juga dapat diakses melalui [IP pribadi](https://intl.cloud.tencent.com/document/product/213/5225).
- Jaringan dari wilayah yang berbeda sepenuhnya terisolasi satu sama lain, dan layanan Tencent Cloud di wilayah yang berbeda tidak dapat berkomunikasi menggunakan jaringan pribadi secara default.
- Layanan Tencent Cloud di seluruh wilayah dapat berkomunikasi satu sama lain melalui [IP publik](https://intl.cloud.tencent.com/document/product/213/5224) melalui Internet, sedangkan layanan di VPC yang berbeda dapat berkomunikasi satu sama lain melalui [CCN](https://intl.cloud.tencent.com/document/product/1003) yang lebih cepat dan stabil.
- [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) saat ini mendukung penerusan lalu lintas intra-wilayah secara default. Jika Anda mengaktifkan fitur [pengikatan lintas wilayah](https://intl.cloud.tencent.com/document/product/214/38441), instans CLB dapat diikat ke instans CVM di wilayah lain.

## Zona Ketersediaan
Zona ketersediaan (AZ) adalah IDC fisik Tencent Cloud dengan catu daya dan jaringan independen di wilayah yang sama. Ini dapat memastikan stabilitas bisnis, karena kegagalan (kecuali untuk bencana besar atau pemadaman listrik) di satu AZ yang diisolasi tanpa memengaruhi AZ lain di wilayah yang sama. Dengan memulai instans di zona ketersediaan independen, pengguna dapat melindungi aplikasi mereka agar tidak terpengaruh oleh satu titik kegagalan.
Saat meluncurkan instans, Anda dapat memilih AZ mana pun di wilayah yang ditentukan. Untuk keandalan yang tinggi, Anda dapat mengadopsi solusi deployment lintas AZ untuk memastikan bahwa layanan tetap tersedia saat instans di satu lokasi gagal. Contoh solusi tersebut termasuk [CLB](https://intl.cloud.tencent.com/document/product/214) dan [EIP](https://intl.cloud.tencent.com/document/product/213/5733).

## Detail Wilayah dan AZ
Wilayah dan AZ yang didukung adalah sebagai berikut:
>?Saat ini, akses jaringan publik hanya didukung di wilayah berikut:
>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing, Hong Kong (Tiongkok), Singapura, Seoul, Tokyo, Silicon Valley, dan Frankfurt

### Tiongkok
<table class="table-striped">
<tbody>
<tr><th>Wilayah</th><th>Zona Ketersediaan</th></tr>
<tr>
<td rowspan="6">Tiongkok Selatan (Guangzhou)<br>ap-guangzhou</td>
<td>Zona Guangzhou 1 (terjual habis)<br> ap-guangzhou-1</td></tr>	
<tr>
<td>Zona Guangzhou 2<br> ap-guangzhou-2</td></tr>
<tr>
<td>Zona Guangzhou 3<br> ap-guangzhou-3</td></tr>
<tr>
<td>Zona Guangzhou 4<br> ap-guangzhou-4</td></tr>
<tr>
<td>Zona Guangzhou 6<br> ap-guangzhou-6</td></tr>
<tr>
<td>Zona Guangzhou 7<br> ap-guangzhou-7</td></tr>
<tr>
<td rowspan="5">Tiongkok Timur (Shanghai)<br>ap-shanghai</td>
<td>Zona Shanghai 1<br>ap-shanghai-1</td></tr>
<tr>
<td>Zona Shanghai 2<br>ap-shanghai-2</td></tr>
<tr>
<td>Zona Shanghai 3<br>ap-shanghai-3</td></tr>
<tr>
<td>Zona Shanghai 4<br>ap-shanghai-4</td></tr>
<tr>
<td>Zona Shanghai 5<br>ap-shanghai-5</td></tr>
<td rowspan="3">Tiongkok Timur (Nanjing)<br>ap-nanjing</td>
<td>Zona Nanjing 1<br>ap-nanjing-1</td></tr>
<tr>
<td>Zona Nanjing 2<br>ap-nanjing-2</td></tr>
<tr>
<td>Zona Nanjing 3<br>ap-nanjing-3</td></tr>
<tr>
<td rowspan="7">Tiongkok Utara (Beijing)<br>ap-beijing</td>
<td>Zona Beijing 1<br>ap-beijing-1</td></tr>
<tr>
<td>Zona Beijing 2<br>ap-beijing-2</td></tr>
<tr>
<td>Zona Beijing 3<br>ap-beijing-3</td></tr>
<tr>
<td>Zona Beijing 4<br>ap-beijing-4</td></tr>
<tr>
<td>Zona Beijing 5<br>ap-beijing-5</td></tr>
<tr>
<td>Zona Beijing 6<br>ap-beijing-6</td></tr>
<tr>
<td>Zona Beijing 7<br>ap-beijing-7</td></tr>
<tr>
<td rowspan="2">Tiongkok Barat Daya (Chengdu)<br>ap-chengdu</td>
<td>Zona Chengdu 1<br>ap-chengdu-1</td></tr>
<tr>
<td>Zona Chengdu 2<br>ap-chengdu-2</td></tr>    
<tr>
<td>Tiongkok Barat Daya (Chongqing)<br>ap-chongqing</td>
<td>Zona Chongqing 1<br>ap-chongqing-1</td></tr>
<tr>
<td rowspan="3">Hong Kong/Makau/Taiwan (Hong Kong, Tiongkok)<br>ap-hongkong</td>
<td>Zona Hong Kong 1 (Node Hong Kong mencakup layanan di wilayah Tiongkok di Hong Kong, Makau, dan Taiwan)<br>ap-hongkong-1</td></tr>
<tr>
<td>Zona Hong Kong 2 (Node Hong Kong mencakup layanan di wilayah Tiongkok di Hong Kong, Makau, dan Taiwan)<br>ap-hongkong-2</td></tr>
<tr>
<td>Zona Hong Kong 3 (Node Hong Kong mencakup layanan di wilayah Tiongkok di Hong Kong, Makau, dan Taiwan)<br>ap-hongkong-3</td></tr>
</tbody></table>	


### [Negara dan wilayah lain](id:Area Internasional)
<table class="table-striped">
<tbody>
<tr><th>Wilayah</th><th>Zona Ketersediaan</th></tr>
<tr>
<td rowspan="4">Asia Tenggara (Singapura)<br>ap-singapore</td>
<td>Zona Singapura 1 (Node Singapura mencakup layanan di Asia Tenggara)<br>ap-singapore-1</td></tr>
<tr>
<td>Zona Singapura 2 (Node Singapura mencakup layanan di Asia Tenggara)<br>ap-singapore-2</td></tr>
<tr>
<td>Zona Singapura 3 (Node Singapura mencakup layanan di Asia Tenggara)<br>ap-singapore-3</td></tr>
<tr>
<td>Zona Singapura 4 (Node Singapura mencakup layanan di Asia Tenggara)<br>ap-singapore-4</td></tr>
<tr>
<td>Asia Tenggara (Jakarta)<br>ap-jakarta</td>
<td>Zona Jakarta 1 (Node Jakarta mencakup layanan di Asia Tenggara)<br>ap-jakarta-1</td></tr>
<tr>
<td rowspan="2">Asia Tenggara (Bangkok)<br>ap-bangkok</td>
<td>Zona Bangkok 1 (Node Bangkok mencakup layanan di Asia Tenggara)<br>ap-bangkok-1</td>
<tr>
<td>Zona Bangkok 2 (Node Bangkok mencakup layanan di Asia Tenggara)<br>ap-bangkok-2</td>
<tr>
<td  rowspan="2">Asia Selatan (Mumbai)<br>ap-mumbai</td>
<td>Zona Mumbai 1 (Node Mumbai mencakup layanan di Asia Selatan)<br>ap-mumbai-1</td></tr>
<tr>
<td>Zona Mumbai 2 (layanan node Mumbai mencakup di Asia Selatan)<br>ap-mumbai-2</td></tr>		
<tr>
<td  rowspan="2">Asia Timur Laut (Seoul)<br>ap-seoul</td>
<td>Zona Seoul 1 (Node Seoul mencakup layanan di Asia Timur Laut)<br>ap-seoul-1</td></tr>
<tr>
<td>Zona Seoul 2 (Node Seoul mencakup layanan di Asia Timur Laut)<br>ap-seoul-2</td></tr>
<tr>
<td rowspan="2">Asia Timur Laut (Tokyo)<br>ap-tokyo</td>
<td>Zona Tokyo 1 (Node Tokyo mencakup layanan di Asia Timur Laut)<br>ap-tokyo-1</td></tr>
<tr>
<td>Zona Tokyo 2 (Node Tokyo mencakup layanan di Asia Timur Laut)<br>ap-tokyo-2</td></tr>
<tr>
<td rowspan="2">AS Barat (Silicon Valley)<br>na-siliconvalley</td>
<td>Zona Silicon Valley 1 (Node Silicon Valley mencakup layanan di AS Barat)<br>na-siliconvalley-1</td></tr>
<tr>
<td>Zona Silicon Valley 2 (Node Silicon Valley mencakup layanan di AS Barat)<br>na-siliconvalley-2</td></tr>
<tr>
<td rowspan="2">AS Timur (Virginia) <br>na-ashburn</td>
<td>Zona Virginia 1 (Node Virginia mencakup layanan di AS Timur)<br>na-ashburn-1</td></tr>
<tr>
<td>Zona Virginia 2 (Node Virginia mencakup layanan di AS Timur)<br>na-ashburn-2</td></tr>
<tr>
<td>Amerika Utara (Toronto)<br>na-toronto</td>
<td>Zona Toronto 1 (Node Toronto mencakup layanan di Amerika Utara)<br>na-toronto-1</td></tr>
<tr>
<td rowspan="2">Eropa (Frankfurt)<br>eu-frankfurt</td>
<td>Zona Frankfurt 1 (Node Frankfurt mencakup layanan di Eropa)<br>eu-frankfurt-1</td></tr>
<tr>
<td>Zona Frankfurt 2 (Node Frankfurt mencakup layanan di Eropa)<br>eu-frankfurt-2</td></tr>
<tr>
<td >Eropa (Moskow)<br>eu-moscow</td>
<td>Zona Moscow 1 (Node Moskow mencakup layanan di Eropa)<br>eu-moscow-1</td></tr>
</tbody></table>

## Memilih Wilayah dan AZ
Saat membeli layanan Tencent Cloud, sebaiknya pilih wilayah yang paling dekat dengan pengguna akhir Anda untuk meminimalkan latensi akses dan meningkatkan kecepatan pengunduhan.
