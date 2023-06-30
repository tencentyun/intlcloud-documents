## Wilayah

### Ringkasan

Wilayah adalah lokasi fisik dari IDC. Di Tencent Cloud, wilayah sepenuhnya terisolasi satu sama lain, memastikan stabilitas lintas wilayah dan toleransi kesalahan. Sebaiknya Anda memilih wilayah yang paling dekat dengan pengguna akhir Anda untuk meminimalkan latensi akses dan meningkatkan kecepatan akses.

Silakan lihat tabel berikut atau gunakan [DescribeRegions](https://intl.cloud.tencent.com/document/product/213/15708) API untuk mendapatkan daftar wilayah dengan daftar lengkap.

### Karakteristik

- Jaringan dari berbagai wilayah sepenuhnya terisolasi. Layanan Tencent Cloud di berbagai wilayah **tidak dapat berkomunikasi melalui jaringan pribadi secara default**.
- Layanan Tencent Cloud di seluruh wilayah dapat berkomunikasi satu sama lain melalui [IP publik](https://intl.cloud.tencent.com/document/product/213/5224) melalui Internet, sedangkan layanan di VPC yang berbeda dapat berkomunikasi satu sama lain melalui [CCN](https://intl.cloud.tencent.com/document/product/1003), yang lebih cepat dan lebih stabil.
- [Cloud Load Balancer (CLB)](https://intl.cloud.tencent.com/document/product/214) saat ini mendukung penerusan lalu lintas dalam wilayah secara default. Jika Anda mengaktifkan fitur [pengikatan lintas wilayah](https://intl.cloud.tencent.com/document/product/214/38441), mendukung pengikatan lintas wilayah dari instans CLB dan CVM.

## Zona Ketersediaan

### Ringkasan

Zona ketersediaan (AZ) adalah IDC fisik Tencent Cloud dengan catu daya dan jaringan independen di wilayah yang sama. Ini dapat memastikan stabilitas bisnis, karena kegagalan (kecuali untuk bencana besar atau pemadaman listrik) di satu AZ yang diisolasi tanpa memengaruhi AZ lain di wilayah yang sama. Dengan memulai instans di zona ketersediaan independen, pengguna dapat melindungi aplikasi mereka agar tidak terpengaruh oleh satu titik kegagalan.
Silakan lihat tabel berikut atau gunakan [DescribeZones](https://intl.cloud.tencent.com/document/product/213/35071) API untuk mendapatkan daftar AZ yang lengkap.

### Karakteristik

Layanan Tencent Cloud di VPC yang sama saling terhubung melalui jaringan pribadi, yang berarti mereka dapat berkomunikasi menggunakan [IP pribadi](https://intl.cloud.tencent.com/document/product/213/5225), meskipun berada di AZ yang berbeda dengan wilayah yang sama.
>?Interkoneksi jaringan pribadi mengacu pada interkoneksi sumber daya dalam akun yang sama. Sumber daya dalam akun yang berbeda sepenuhnya terisolasi di jaringan pribadi.
>

<span id="MainlandChina"></span>
## Tiongkok
<table class="table-striped">
<tbody>
	<tr>
		<th>Wilayah</th>
		<th>AZ</th>
	</tr>
	<tr>
		<td rowspan="6">Tiongkok Selatan (Guangzhou)<br>ap-guangzhou</td>
		<td>Zona 1 Guangzhou (terjual habis)<br> ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>Zona 2 Guangzhou (terjual habis)<br>ap-guangzhou-2</td>
	</tr>
	<tr>
		<td>Zona 3 Guangzhou<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>Zona 4 Guangzhou<br>ap-guangzhou-4</td>
	</tr>
	<tr>
		<td>Zona 6 Guangzhou<br>ap-guangzhou-6</td>
	</tr>
	<tr>
                <td>Zona 7 Guangzhou<br>ap-guangzhou-7</td>
	</tr>
	<tr>
		<td rowspan="5">Tiongkok Timur (Shanghai)<br>ap-shanghai</td>
		<td>Zona 1 Shanghai (terjual habis)<br>ap-shanghai-1</td>
	</tr>
	<tr>
		<td>Zona 2 Shanghai<br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>Zona 3 Shanghai<br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>Zona 4 Shanghai<br>ap-shanghai-4</td>
	</tr>
        <tr>
		<td>Zona 5 Shanghai<br>ap-shanghai-5</td>
	</tr>
		<tr>
			<td rowspan="3">Tiongkok Timur (Nanjing)<br>ap-nanjing</td>
			<td>Zona 1 Nanjing<br>ap-nanjing-1</td>
	</tr>
	<tr>
			<td>Zona 2 Nanjing<br>ap-nanjing-2</td>
	</tr>
	<tr>
                        <td>Zona 3 Nanjing<br>ap-nanjing-3</td>
	</tr>
	<tr>
			<td rowspan="7">Tiongkok Utara (Beijing)<br>ap-beijing</td>
			<td>Zona 1 Beijing(terjual habis)<br>ap-beijing-1</td>
	</tr>
	<tr>
			<td>Zona 2 Beijing<br>ap-beijing-2</td>
	</tr>
	<tr>
			<td>Zona 3 Beijing<br>ap-beijing-3</td>
	</tr>
	<tr>
			<td>Zona 4 Beijing<br>ap-beijing-4</td>
	</tr>
	<tr>
			<td>Zona 5 Beijing <br>ap-beijing-5</td>
	</tr>
	<tr>
			<td>Zona 6 Beijing<br>ap-beijing-6</td>
	</tr>
	<tr>
			<td>Zona 7 Beijing<br>ap-beijing-7</td>
	</tr>
	<tr>
		<td rowspan="2">Tiongkok Barat Daya (Chengdu)<br>ap-chengdu</td>
		<td>Zona 1 Chengdu<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>Zona 2 Chengdu<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >Tiongkok Barat Daya (Chongqing)<br>ap-chongqing</td>
			<td>Zona 1 Chongqing<br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="3">Hong Kong, Makau dan Taiwan, Tiongkok (Hong Kong)<br>ap-hongkong</td>
			<td>Zona 1 Hong Kong (Node di Hong Kong, Tiongkok dapat mencakup wilayah Hong Kong/Makau/Taiwan) (terjual habis)<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>Zona 2 Hong Kong (Node di Hong Kong, Tiongkok dapat mencakup wilayah Hong Kong/Makau/Taiwan)<br>ap-hongkong-2</td>
	</tr>
	<tr>
			<td>Zona 3 Hong Kong (Node di Hong Kong, Tiongkok dapat mencakup wilayah Hong Kong/Makau/Taiwan)<br>ap-hongkong-3</td>
	</tr>
</tbody>
</table>	


<span id="InternationalArea"></span>

## Negara dan Wilayah Lain	
<table class="table-striped">
	<tbody>
	<tr>
			<th>Wilayah</th>
			<th>AZ</th>
		</tr>
		<tr>
			<td  rowspan="4">Asia Tenggara (Singapura)<br>ap-singapore</td>
			<td>Zona 1 Singapura (Node di Singapura dapat mencakup Asia Tenggara)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>Zona 2 Singapura (Node di Singapura dapat mencakup Asia Tenggara)<br>ap-singapore-2</td>
		</tr>
		<tr>
			<td>Zona 3 Singapura (Node di Singapura dapat mencakup Asia Tenggara)<br>ap-singapore-3</td>
		</tr>
		<tr>
                        <td>Zona 4 Singapura (Node di Singapura dapat mencakup Asia Tenggara)<br>ap-singapore-4</td>
		</tr>
		<tr>
			<td  rowspan="2">Asia Tenggara (Jakarta)<br>ap-jakarta</td>
			<td>Zona 1 Jakarta (Node di Jakarta dapat mencakup Asia Tenggara)<br>ap-jakarta-1</td>
		</tr>
		<tr>
                         <td>Zona 2 Jakarta (Node di Jakarta dapat mencakup Asia Tenggara)<br>ap-jakarta-2</td>
		</tr>
		<tr>
			<td  rowspan="2">Asia Timur Laut (Seoul)<br>ap-seoul</td>
			<td>Zona 1 Seoul (Node di Seoul dapat mencakup Asia Timur Laut)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>Zona 2 Seoul (Node di Seoul dapat mencakup Asia Timur Laut)<br>ap-seoul-2</td>
		</tr>
		<tr>
			<td rowspan="2">Asia Timur Laut (Tokyo)<br>ap-tokyo</td>
			<td>Zona 1 Tokyo (Node di Tokyo dapat mencakup Asia Timur Laut)<br>ap-tokyo-1</td>
		</tr>
		<tr>
			<td>Zona 2 Tokyo (Node di Tokyo dapat mencakup Asia Timur Laut)<br>ap-tokyo-2</td>
		</tr>
       <tr>
			<td  rowspan="2">Asia Selatan (Mumbai)<br>ap-mumbai</td>
			<td>Zona 1 Mumbai (Node di Mumbai dapat mencakup Asia Selatan)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>Zona 2 Mumbai (Node di Mumbai dapat mencakup Asia Selatan) <br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td rowspan="2">Asia Tenggara (Bangkok)<br>ap-bangkok </td>
				 <td >Zona 1 Bangkok (Node di Bangkok dapat mencakup Asia Tenggara Pasifik)<br>ap-bangkok-1</td>
		</tr>
		<tr>
                                 <td >Zona 2 Bangkok (Node di Bangkok dapat mencakup Asia Tenggara Pasifik)<br>ap-bangkok-2</td>
		</tr>
		<tr>
			<td>Amerika Utara (Toronto)<br>na-toronto</td>
			<td>Zona 1 Toronto (Node di Toronto dapat mencakup Amerika Utara)<br>na-toronto-1</td>
		</tr>
		<tr>
                        <td>Amerika Selatan (Saopaulo)<br>sa-saopaulo</td>
			<td>Zona 1 Saopaulo (Node di Saopaulo dapat mencakup Amerika Selatan)<br>sa-saopaulo-1</td>
		</tr>
		<tr>
			<td rowspan="2">AS Barat (Silicon Valley)<br>na-siliconvalley</td>
			<td>Zona 1 Silicon Valley (Node di Silicon Valley dapat mencakup AS Barat)<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>Zona 2 Silicon Valley (Node di Silicon Valley dapat mencakup AS Barat)<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">AS Timur (Virginia) <br>na-ashburn</td>
			<td>Zona 1 Virginia (Node di Virginia dapat mencakup AS Timur)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>Zona 2 Virginia (Node di Virginia dapat mencakup AS Timur)<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td rowspan="2">Eropa (Frankfurt)<br>eu-frankfurt</td>
			<td>Zona 1 Frankfurt (Node di Frankfurt dapat mencakup Eropa)<br>eu-frankfurt-1</td>
		</tr>
                <tr>
                        <td>Zona 2 Frankfurt (Node di Frankfurt dapat mencakup Eropa)<br>eu-frankfurt-2</td>
		</tr>
                <tr>
	</tbody>
</table>

## Cara Memilih Wilayah dan Zona Ketersediaan

Saat memilih wilayah dan zona ketersediaan, pertimbangkan hal berikut:
- Lokasi Anda, lokasi pengguna Anda, dan wilayah instans CVM.
Sebaiknya Anda memilih wilayah yang paling dekat dengan pengguna akhir Anda saat membeli instans CVM untuk meminimalkan latensi akses dan meningkatkan kecepatan akses.
- Layanan Tencent Cloud lain yang Anda gunakan.
Saat Anda memilih layanan Tencent Cloud lainnya, sebaiknya Anda mencoba menempatkan semuanya di wilayah dan zona ketersediaan yang sama agar layanan dapat berkomunikasi satu sama lain melalui jaringan pribadi, mengurangi latensi akses dan meningkatkan kecepatan akses.
- Ketersediaan tinggi dan pemulihan bencana.
Meskipun Anda hanya memiliki satu VPC, kami tetap menyarankan agar Anda menerapkan bisnis Anda di zona ketersediaan yang berbeda untuk mencegah satu titik kegagalan dan mengaktifkan pemulihan bencana lintas-AZ.
- Mungkin ada latensi jaringan di antara zona ketersediaan yang berbeda. Sebaiknya Anda menilai kebutuhan bisnis Anda dan menemukan keseimbangan optimal antara ketersediaan tinggi dan latensi rendah.
- Jika Anda memerlukan akses ke instans CVM di negara atau wilayah lain, sebaiknya pilih CVM di negara atau wilayah lain tersebut. Jika Anda menggunakan instans CVM di [Tiongkok](#MainlandChina) untuk mengakses [server di negara dan wilayah lain](#InternationalArea), Anda mungkin mengalami latensi jaringan yang jauh lebih tinggi.

## Ketersediaan Sumber Daya
Tabel berikut menjelaskan sumber daya Tencent Cloud mana yang bersifat global, yang bersifat regional, dan yang khusus untuk zona ketersediaan.

<table>
	<tr><th>Sumber Daya</th><th>Format ID Sumber Daya<br><Resource Abbreviation>-8-Digit String Angka dan Huruf</th><th>Jenis</th><th>Deskripsi</th></tr>
	<tbody>
	<tr>
	  <td>Akun Pengguna</td>
	  <td>Tidak ada batasan</td>
	  <td>Unik secara global</td>
	  <td>Pengguna dapat menggunakan akun yang sama untuk mengakses sumber daya Tencent Cloud dari seluruh dunia.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">Kunci SSH</a> </td>
	  <td>skey-xxxxxxxx</td>
	  <td>Global</td>
	  <td>Pengguna dapat menggunakan kunci SSH untuk mengikat CVM di wilayah mana pun dalam akun.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">Instans CVM</a> </td>
	  <td>ins-xxxxxxxx</td>
	  <td>Instans CVM khusus untuk zona ketersediaan</td>
	  <td>Instans CVM yang dibuat di zona ketersediaan tidak tersedia untuk zona ketersediaan lainnya.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941?from_cn_redirect=1">Citra Kustom</a> </td>
	  <td>img-xxxxxxxx</td>
	  <td>Regional</td>
	  <td>Citra kustom yang dibuat untuk instans tersedia untuk semua zona ketersediaan di wilayah yang sama. Gunakan <b>Salin Citra</b> untuk menyalin citra kustom jika Anda perlu menggunakannya di wilayah lain.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a> </td>
	  <td>eip-xxxxxxxx</td>
	  <td>Regional</td>
	  <td>EIP hanya dapat dikaitkan dengan instans di wilayah yang sama.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/12452?from_cn_redirect=1">Grup Keamanan</a> </td>
	  <td>sg-xxxxxxxx</td>
	  <td>Regional</td>
	  <td>Grup Keamanan hanya dapat dikaitkan dengan instans di wilayah yang sama. Tencent Cloud secara otomatis membuat tiga grup keamanan default untuk pengguna.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362">Cloud Block Storage</a> </td>
	  <td>disk-xxxxxxxx</td>
	  <td>Disk CBS khusus untuk zona ketersediaan.</td>
	  <td>Pengguna hanya dapat membuat disk Cloud Block Storage di AZ tertentu dan memasangnya ke instans di zona ketersediaan yang sama.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362/31638">Snapshot</a> </td>
	  <td>snap-xxxxxxxx</td>
	  <td>Regional</td>
	  <td>Snapshot yang dibuat dari disk cloud dapat digunakan untuk tujuan lain (seperti membuat disk cloud) di wilayah ini.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/214/524?from_cn_redirect=1">Cloud Load Balancer</a> </td>
	  <td>clb-xxxxxxxx</td>
	  <td>Regional</td>
	  <td>Cloud Load Balancer dapat diikat dengan CVM di zona ketersediaan yang berbeda dari satu wilayah untuk penerusan lalu lintas.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">VPC</a> </td>
	  <td>vpc-xxxxxxxx</td>
	  <td>Regional</td>
	  <td>VPC di satu wilayah dapat memiliki sumber daya yang dibuat di zona ketersediaan yang berbeda.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535#.E5.AD.90.E7.BD.91">Subnet</a> </td>
	  <td>subnet-xxxxxxxx</td>
	  <td>Subnet khusus untuk zona ketersediaan.</td>
	  <td>Pengguna tidak dapat membuat subnet di seluruh zona ketersediaan.</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/31810">Tabel Rute</a> </td>
	  <td> rtb-xxxxxxxx</td>
	  <td>Regional</td>
	  <td>Saat membuat tabel rute, pengguna harus menentukan VPC. Oleh karena itu, tabel rute juga bersifat regional.</td>
	</tr>
	</tbody>
</table>


## Operasi yang Relevan

### Memigrasikan instans ke zona ketersediaan lain

Setelah diluncurkan, sebuah instans tidak dapat dimigrasikan. Namun, Anda dapat membuat citra kustom instans CVM dan menggunakan citra tersebut untuk meluncurkan atau memperbarui instans di zona ketersediaan yang berbeda.
1. Buat citra khusus dari instans saat ini. Untuk informasi selengkapnya, lihat [Membuat Citra Kustom](https://intl.cloud.tencent.com/document/product/213/4942).
2. Jika instans berada di [VPC](https://intl.cloud.tencent.com/document/product/213/5227) dan Anda ingin mempertahankan alamat IP pribadinya saat ini setelah migrasi, pertama-tama hapus subnet di zona ketersediaan saat ini, lalu buat subnet di zona ketersediaan baru dengan rentang alamat IP yang sama. Perhatikan bahwa subnet hanya dapat dihapus jika tidak ada instans yang tersedia. Oleh karena itu, semua instans di subnet saat ini harus dimigrasikan ke subnet baru.
3. Buat instans baru di zona ketersediaan baru dengan menggunakan citra kustom yang baru saja Anda buat. Anda dapat memilih jenis dan konfigurasi yang sama seperti instans asli, atau memilih pengaturan baru. Untuk informasi selengkapnya, lihat [Membuat Instans melalui Halaman Pembelian CVM](https://intl.cloud.tencent.com/document/product/213/4855).
4. Jika IP elastis dikaitkan dengan instans asli, pisahkan dari instans lama dan kaitkan dengan instans baru. Untuk informasi selengkapnya, lihat [IP Elastis (EIP)](https://intl.cloud.tencent.com/document/product/213/5733).
5. (Opsional) Jika instans asli adalah [bayar sesuai pemakaian](https://intl.cloud.tencent.com/document/product/213/2180), Anda dapat memilih untuk menghentikannya. Untuk informasi selengkapnya, lihat [Menghentikan Instans](https://intl.cloud.tencent.com/document/product/213/4930).

### Menyalin citra ke wilayah lain

Operasi seperti meluncurkan dan melihat instans bersifat spesifik wilayah. Jika citra instans yang perlu Anda luncurkan tidak ada di wilayah tersebut, salin citra ke wilayah yang diinginkan. Untuk informasi selengkapnya, lihat [Menyalin Citra](https://intl.cloud.tencent.com/document/product/213/4943).
