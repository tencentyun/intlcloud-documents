
## Wilayah
### Ikhtisar
Wilayah adalah lokasi fisik dari IDC. Di Tencent Cloud, wilayah sepenuhnya terisolasi satu sama lain, memastikan stabilitas lintas wilayah dan toleransi kesalahan. Saat membeli layanan Tencent Cloud, sebaiknya pilih wilayah yang paling dekat dengan pengguna akhir Anda untuk meminimalkan latensi akses dan meningkatkan kecepatan pengunduhan.

### Karakteristik
- Jaringan dari berbagai wilayah sepenuhnya terisolasi. Layanan Tencent Cloud di berbagai wilayah **tidak dapat berkomunikasi melalui jaringan pribadi secara default**.
Layanan Tencent Cloud di VPC yang berbeda dapat saling berkomunikasi melalui [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003), yang lebih cepat dan stabil.

## Zona Ketersediaan
### Ikhtisar
Zona ketersediaan (AZ) adalah IDC fisik Tencent Cloud dengan catu daya dan jaringan independen di wilayah yang sama. Ini dapat memastikan stabilitas bisnis, karena kegagalan (kecuali untuk bencana besar atau pemadaman listrik) di satu AZ yang diisolasi tanpa memengaruhi AZ lain di wilayah yang sama. Dengan memulai instans di zona ketersediaan independen, pengguna dapat melindungi aplikasi mereka agar tidak terpengaruh oleh satu titik kegagalan.

### Karakteristik
Layanan Tencent Cloud di VPC yang sama saling terhubung melalui jaringan pribadi, yang berarti mereka dapat berkomunikasi menggunakan [IP pribadi](https://intl.cloud.tencent.com/document/product/213/5225), meskipun berada di zona ketersediaan yang berbeda dengan wilayah yang sama.
>? Interkoneksi jaringan pribadi mengacu pada interkoneksi sumber daya dalam akun yang sama. Sumber daya dalam akun yang berbeda sepenuhnya terisolasi di jaringan pribadi.
>

## Daftar Wilayah dan AZ
## Tiongkok
<table class="table-striped">
<tbody><tr><th>Wilayah</th><th>Zona Ketersediaan</th><th>ID Zona</th></tr>
<tr>
<td rowspan="6">Tiongkok Selatan (Guangzhou)<br>ap-guangzhou</td>
<td>Zona Guangzhou 1<br> ap-guangzhou-1</td><td>100001</td></tr>	
<tr>
<td>Zona Guangzhou 2<br> ap-guangzhou-2</td><td>100002</td></tr>
<tr>
<td>Zona Guangzhou 3<br> ap-guangzhou-3</td><td>100003</td></tr>
<tr>
<td>Zona Guangzhou 4<br> ap-guangzhou-4</td><td>100004</td></tr>
<tr>
<td>Zona Guangzhou 6<br> ap-guangzhou-6</td><td>100006</td></tr>
<tr>
<td>Zona Guangzhou 7<br> ap-guangzhou-7</td><td>100007</td></tr>
<tr>
<td rowspan="7">Tiongkok Timur (Shanghai)<br>ap-shanghai</td>
<td>Zona Shanghai 1<br>ap-shanghai-1</td><td>200001</td></tr>
<tr>
<td>Zona Shanghai 2<br>ap-shanghai-2</td><td>200002</td></tr>
<tr>
<td>Zona Shanghai 3<br>ap-shanghai-3</td><td>200003</td></tr>
<tr>
<td>Zona Shanghai 4<br>ap-shanghai-4</td><td>200004</td></tr>
<tr>
<td>Zona Shanghai 5<br>ap-shanghai-5</td><td>200005</td></tr>
<tr>
<td>Zona Shanghai 6<br>ap-shanghai-6</td><td>200006</td></tr>
<tr>
<td>Zona Shanghai 7<br>ap-shanghai-7</td><td>200007</td></tr>
<tr>
<td rowspan="2">Tiongkok Timur (Nanjing)<br>ap-nanjing</td>
<td>Zona Nanjing 1<br>ap-nanjing-1</td><td>330001</td></tr>
<tr>
<td>Zona Nanjing 2<br>ap-nanjing-2</td><td>330002</td></tr>
<tr>
<td rowspan="7">Tiongkok Utara (Beijing)<br>ap-beijing</td>
<td>Zona Beijing 1<br>ap-beijing-1</td><td>800001</td></tr>
<tr>
<td>Zona Beijing 1<br>ap-beijing-1</td><td>800002</td></tr>
<tr>
<td>Zona Beijing 3<br>ap-beijing-3</td><td>800003</td></tr>
<tr>
<td>Zona Beijing 4<br>ap-beijing-4</td><td>800004</td></tr>
<tr>
<td>Zona Beijing 5<br>ap-beijing-5</td><td>800005</td></tr>
<tr>
<td>Zona Beijing 6<br>ap-beijing-6</td><td>80006</td></tr>
<tr>
<td>Zona Beijing 7<br>ap-beijing-7</td><td>800007</td></tr>
<tr>
<td rowspan="2">Tiongkok Barat Daya (Chengdu)<br>ap-chengdu</td>
<td>Zona Chengdu 1<br>ap-chengdu-1</td><td>16001</td></tr>
<tr>
<td>Zona Chengdu 2<br>ap-chengdu-2</td><td>160002</td></tr>    
<tr>
<td>Tiongkok Barat Daya (Chongqing)<br>ap-chongqing</td>
<td>Zona Chongqing 1<br>ap-chongqing-1</td><td>19001</td></tr>
<tr>
<td rowspan="3">Hong Kong/Makau/Taiwan (Hong Kong, Tiongkok)<br>ap-hongkong</td>
<td>Zona Hong Kong 1 (Node Hong Kong mencakup layanan di wilayah Tiongkok di Hong Kong, Makau, dan Taiwan)<br>ap-hongkong-1</td><td>300001</td></tr>
<tr>
<td>Zona Hong Kong 2 (Node di Hong Kong, Tiongkok mencakup wilayah Hong Kong/Macao/Taiwan)<br>ap-hongkong-2</td><td>300002</td></tr>
<tr>
<td>Zona Hong Kong 3 (Node Hong Kong mencakup layanan di wilayah Tiongkok di Hong Kong, Makau, dan Taiwan)<br>ap-hongkong-3</td><td>300003</td></tr>
</tbody></table>	

### Negara dan wilayah lain
<table class="table-striped">
<tbody><tr><th>Wilayah</th><th>Zona Ketersediaan</th><th>ID Zona</th></tr>
<tr>
<td rowspan="3">Asia Tenggara (Singapura)<br>ap-singapore</td>
<td>Zona Singapura 1 (Node Singapura mencakup layanan di Asia Tenggara)<br>ap-singapore-1</td><td>900001</td></tr>
<tr>
<td>Zona Singapura 2 (Node Singapura mencakup layanan di Asia Tenggara)<br>ap-singapore-2</td><td>900002</td></tr>
<tr>
<td>Zona Singapura 3 (Node Singapura mencakup layanan di Asia Tenggara)<br>ap-singapore-3</td><td>900003</td></tr>
<tr>
<td>Asia Tenggara (Jakarta)<br>ap-jakarta</td>
<td>Zona Jakarta 1 (Node Jakarta mencakup layanan di Asia Tenggara)<br>ap-jakarta-1</td><td>720001</td></tr>
<tr>
<td rowspan="2">Asia Tenggara (Bangkok)<br>ap-bangkok</td>
<td>Zona Bangkok 1 (Node Bangkok mencakup layanan di Asia Tenggara)<br>ap-bangkok-1</td><td>230001</td></tr>
<tr>
<td>Zona Bangkok 2 (Node Bangkok mencakup layanan di Asia Tenggara)<br>ap-bangkok-2</td><td>230002</td></tr>
<tr>
<td rowspan="2">Asia Selatan (Mumbai)<br>ap-mumbai</td>
<td>Zona Mumbai 1 (Node Mumbai mencakup layanan di Asia Selatan)<br>ap-mumbai-1</td><td>210001</td></tr>
<tr>
<td>Zona Mumbai 2 (layanan node Mumbai mencakup di Asia Selatan)<br>ap-mumbai-2</td><td>210002</td></tr>		
<tr>
<td rowspan="2">Asia Timur Laut (Seoul)<br>ap-seoul</td>
<td>Zona Seoul 1 (Node Seoul mencakup layanan di Asia Timur Laut)<br>ap-seoul-1</td><td>180001</td></tr>
<tr>
<td>Zona Seoul 2 (Node Seoul mencakup layanan di Asia Timur Laut)<br>ap-seoul-2</td><td>180002</td></tr>
<tr>
<td rowspan="2">Asia Timur Laut (Tokyo)<br>ap-tokyo</td>
<td>Zona Tokyo 1 (Node Tokyo mencakup layanan di Asia Timur Laut)<br>ap-tokyo-1</td><td>250001</td></tr>
<tr>
<td>Zona Tokyo 2 (Node Tokyo mencakup layanan di Asia Timur Laut)<br>ap-tokyo-2</td><td>250002</td></tr>
<tr>
<td rowspan="2">AS Barat (Silicon Valley)<br>na-siliconvalley</td>
<td>Zona Silicon Valley 1 (Node Silicon Valley mencakup layanan di AS Barat)<br>na-siliconvalley-1</td><td>150001</td></tr>
<tr>
<td>Zona Silicon Valley 2 (Node Silicon Valley mencakup layanan di AS Barat)<br>na-siliconvalley-2</td><td>150002</td></tr>
<tr>
<td rowspan="2">AS Timur (Virginia)<br>na-ashburn</td>
<td>Zona Virginia 1 (Node Virginia mencakup layanan di AS Timur)<br>na-ashburn-1</td><td>220001</td></tr>
<tr>
<td>Zona Virginia 2 (Node Virginia mencakup layanan di AS Timur)<br>na-ashburn-2</td><td>220002</td></tr>
<tr>
<td>Amerika Utara (Toronto)<br>na-toronto</td>
<td>Zona Toronto 1 (Node Toronto mencakup layanan di Amerika Utara)<br>na-toronto-1</td><td>400001</td></tr>
<tr>
<td rowspan="2">Eropa (Frankfurt)<br>eu-frankfurt</td>
<td>Zona Frankfurt 1 (Node Frankfurt mencakup layanan di Eropa)<br>eu-frankfurt-1</td><td>170001</td></tr>
<tr>
<td>Zona Frankfurt 2 (Node Frankfurt mencakup layanan di Eropa)<br>eu-frankfurt-2</td><td>170002</td></tr>
<td >Eropa (Moskow)<br>eu-moscow</td>
<td>Zona Moskwa 1 (Node Moskow mencakup layanan di Eropa)<br>eu-moscow-1</td><td>240001</td></tr>
<tr>
<td>Amerika Selatan (Sao Paulo)<br>sa-saopaulo</td>
<td>ZonA Sao Paulo 1 (Node Sao Paulo mencakup layanan di Amerika Selatan)<br>sa-saopaulo-1</td><td>740001</td></tr>
</tbody></table>

## Pemilihan Wilayah dan AZ
Saat membeli layanan Tencent Cloud, sebaiknya pilih wilayah yang paling dekat dengan pengguna akhir Anda untuk meminimalkan latensi akses dan meningkatkan kecepatan pengunduhan.

