## Rilis Instans
### Mengapa instans spot dirilis secara otomatis?
Fitur penting instans spot adalah bahwa sistem akan mengambil kembali instans yang ditetapkan berdasarkan harga atau hubungan pasokan-permintaan. Jika harga pasar lebih tinggi dari tawaran Anda atau jika kumpulan sumber daya CVM yang sesuai dengan instans spot Anda kekurangan pasokan, prosesnya akan terganggu oleh sistem.

### Apakah bisa menggunakan penawaran untuk menghindari agar tidak diambil alih oleh sistem?
Tidak. Karena kepemilikan kembali yang dipicu oleh inventaris yang tidak mencukupi tidak dapat dihindari. Anda harus menerima bahwa kepemilikan kembali instans dapat terjadi saat Anda men-deploy bisnis instans spot.

### Bagaimana saya tahu bahwa sebuah instans akan mengalami gangguan?
Dua menit sebelum gangguan, kami akan memberi tahu Anda dalam bentuk metadata bahwa instans akan mengalami gangguan dan diambil alih.
Untuk informasi selengkapnya, lihat [Mengkueri Status Kepemilikan Kembali dari Instans Spot](https://intl.cloud.tencent.com/document/product/213/32487).

### Bagaimana cara mengajukan instans spot secara otomatis setelah pemulihan inventaris?
Anda dapat menggunakan produk cloud yang dapat mempertahankan kluster CVM secara otomatis, seperti [BatchCompute](http://console.cloud.tencent.com/batch/env), [Auto Scaling](http://console.cloud.tencent.com/autoscaling). Dengan kemampuan lintas model dan lintas zona ketersediaan, Anda dapat mempertahankan sejumlah kluster CVM tertentu dengan lebih efektif.

## Harga dan Penagihan
### Apa persamaan dan perbedaan antara instans spot dan instans berbasis pembayaran sesuai pemakaian?
<table>
	<tr><th style="width: 14%">Metode Penagihan</th><th style="width: 43%">Persamaan</th><th style="width: 43%">Perbedaan</th></tr>
	<tr><td>Instans Spot</td><td rowspan=2>Keduanya berbasis pembayaran sesuai pemakaian. Tidak perlu membayar di muka tetapi biaya tertentu harus dibekukan. Anda dapat mengaktifkan/mengakhiri CVM kapan saja dan membayar sesuai dengan pemakaian aktual. Perincian waktu penagihan bersifat akurat hingga hitungan detik, dan akun akan diselesaikan per jam. </td><td rowspan=2><ul  style="margin: 0;"><li><b>Harga</b>: Dalam kebanyakan kasus, harga instans spot adalah 10%-20% dari harga instans berbasis pembayaran sesuai pemakaian dengan spesifikasi yang sama. </li><li><b>Mekanisme rilis</b>: Siklus pemakaian instans berbasis pembayaran sesuai pemakaian dikendalikan oleh pengguna, sementara instans spot mungkin secara aktif diambil alih oleh sistem. </li><li><b>Batasan fitur</b>：Penyesuaian konfigurasi tidak diizinkan. </li></ul></td></tr>
	<tr><td>Instans berbasis pembayaran sesuai pemakaian</td></tr>
</table>

### Harga manakah yang akan digunakan untuk penagihan, harga pasar dan tawaran tertinggi yang ditentukan oleh pengguna?
Harga pasar akan digunakan untuk penagihan. Anda dapat menentukan tawaran tinggi untuk mencegah agar instans tidak diambil alih karena harga. Namun, sistem hanya akan menagih Anda dengan harga pasar saat ini (harga pasar saat ini akan tetap).

### Bagaimana periode penagihan dihitung untuk instans spot?
Anda akan ditagih untuk periode dari saat Anda mengajukan permohonan instans spot hingga saat instans spot dilepaskan secara manual atau terganggu oleh sistem. Periode penagihan akurat untuk yang kedua.

### Di mana saya bisa menemukan harga pasar semua instans spot saat ini?
Selama periode pengujian beta, kami tidak dapat menyediakan halaman tempat Anda bisa menanyakan harga pasar semua instans, tetapi halaman ini akan tersedia di masa mendatang. Saat ini, sebagian besar instans spot akan diberi harga 20% dari instans berbasis pembayaran sesuai pemakaian reguler dengan model dan spesifikasi yang sama.

### Di mana saya bisa melihat detail konsumsi terkait instans spot?
Seperti halnya instans berbasis pembayaran sesuai pemakaian, Anda dapat menemukan detail penggunaan dan informasi tagihan instans spot di **Billing Center** (Pusat Tagihan) > **Bills** (Tagihan) di bagian atas konsol. Instans spot adalah layanan berbasis pembayaran sesuai pemakaian.

## Kuota dan Batasan
### Di wilayah mana instans spot tersedia? Model dan spesifikasi instans mana yang didukung instans spot?
<table>
<tr><th>Wilayah</th><th>Model yang didukung oleh instans spot</th><th>Diskon</th></tr>
<tr><td>Beijing, Shanghai, Chengdu, Chongqing, Guangzhou Open</td><td rowspan="4">Semua model yang didukung oleh instans berbasis pembayaran sesuai pemakaian</td><td rowspan="4">Diskon 80% dari harga instans berbasis pembayaran sesuai pemakaian dengan spesifikasi yang sama yang diterbitkan</td></tr>
<tr><td>Guangzhou (tidak termasuk Zona Guangzhou 1)</td></tr>
<tr><td>Hong Kong (Tiongkok), Singapura, Bangkok, Seoul, Tokyo, Mumbai, Toronto, Silicon Valley, Virginia, Frankfurt</td></tr>
</table>

### Apakah batas kuota instans spot dibagikan dengan instans berbasis pembayaran sesuai pemakaian?
Tidak. Setiap pengguna dapat memiliki maksimal 50 inti vCPU instans spot di setiap zona ketersediaan. Untuk meningkatkan batas kuota, harap kirimkan tiket.

### Bisakah saya meningkatkan atau menurunkan spesifikasi instans spot?
Meningkatkan atau menurunkan spesifikasi instans spot tidak didukung.

### Apakah instans spot mendukung tanpa biaya alias gratis saat dihentikan?
Instans spot tidak mendukung tanpa biaya saat dihentikan.

### Apakah instans spot mendukung penginstalan ulang sistem?
Instans spot tidak mendukung penginstalan ulang sistem.
