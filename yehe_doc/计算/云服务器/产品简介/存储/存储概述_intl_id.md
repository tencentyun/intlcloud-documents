Tencent Cloud menyediakan berbagai perangkat penyimpanan data yang fleksibel dan hemat biaya untuk instans CVM. Performa dan harga berbeda-beda menurut jenis perangkat penyimpanan, yang cocok untuk skenario yang berbeda.


## Perangkat Penyimpanan
Perangkat penyimpanan berdasarkan dimensi dapat dibagi ke dalam kategori berikut:
<table>
        <tbody>
		<tr>
            <th style="width: 5%;">Dimensi</th>
            <th style="width: 5%;" >Kategori</th>
            <th style="width: 20%;" >Deskripsi</th>
        </tr>
        <tr>
            <td rowspan="2">Media Penyimpanan</td>
            <td>Disk HDD</td>
            <td>Menggunakan hard disk drive (HHD) sebagai media penyimpanan. HDD memberikan harga rendah dan kecepatan baca/tulis yang cepat.</td>
        </tr>
				<tr>
				    <td>Disk SSD</td>
					<td>Menggunakan solid state drive (SSD) sebagai media penyimpanan. SSD memberikan IOPS yang sangat baik dan kecepatan baca/tulis, dengan IOPS dan throughput hingga 20 kali dan 16 kali lebih tinggi daripada disk HDD. SSD lebih mahal daripada disk HDD.</td>
			    <tr>
            		<td rowspan="2">Kasus Penggunaan</td>
            		<td>Disk sistem</td>
            		<td>Digunakan untuk menyimpan kumpulan sistem yang mengontrol dan menjadwalkan pengoperasian CVM. Disk ini menggunakan citra.</td>
        </tr>
				<tr>
				    <td>Disk data</td>
						<td>Digunakan untuk menyimpan semua data pengguna.</td>
						<tr>
						<td rowspan="2">Arsitektur</td>
						<td><a href="https://intl.cloud.tencent.com/document/product/213/4953">Cloud Block Storage</a></td>
            <td>Cloud Block Storage (CBS) adalah perangkat blok jaringan yang elastis, sangat tersedia, sangat andal, berbiaya rendah, dan dapat disesuaikan yang bisa digunakan sebagai disk berskala mandiri untuk CVM. CBS menyediakan penyimpanan data pada tingkat blok data dan menggunakan 3-salinan mekanisme terdistribusi untuk memastikan keandalan data.<br><font style="font-weight:bold">Anda dapat menyesuaikan perangkat keras, disk, dan jaringan CVM dengan CBS.</font><br>
						</td>
        </tr>
				<td><a href="https://intl.cloud.tencent.com/document/product/213/4961">Cloud Object Storage</a></td>
						<td>Cloud Object Storage (COS) adalah perangkat penyimpanan data di Internet. COS memungkinkan pengambilan data dari lokasi mana pun di instans CVM atau Internet, sehingga mengurangi biaya penyimpanan. COS tidak cocok untuk skenario latensi rendah dan IO tinggi.
						</td>
				</tbody>
				</table>

## Pemetaan perangkat penyimpanan blok

Setiap instans memiliki disk sistem untuk memastikan operasi data dasar, dan dapat memasang lebih banyak disk data. Instans menggunakan pemetaan perangkat penyimpanan blok untuk memetakan perangkat penyimpanan ke lokasi yang dapat diidentifikasi.
CBS menempatkan data ke dalam blok dalam byte dan memungkinkan akses secara acak. Tencent Cloud mendukung dua jenis perangkat CBS: disk lokal dan disk cloud.
![](https://main.qcloudimg.com/raw/3815bb250f6178d67b8fe2be11a50bf8.svg)
Gambar ini menunjukkan cara CBS memetakan perangkat penyimpanan blok ke CVM: CBS memetakan `/dev/vda` ke disk sistem dan memetakan dua disk data ke `/dev/vdb` dan `/dev/vdc`, secara berurutan.
Instans CVM dapat secara otomatis membuat pemetaan perangkat penyimpanan blok untuk disk lokal dan disk cloud yang dipasang ke disk itu sendiri.

