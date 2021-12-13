Siklus pemakaian instans Tencent Cloud CVM mengacu pada semua status dari peluncuran instans hingga rilisnya. Mengelola instans Tencent Cloud dengan benar dalam berbagai status dapat memastikan bahwa aplikasi yang berjalan pada instans menyediakan layanan secara ekonomis dan efisien.

Status Instans

- **Sebuah instans memiliki status berikut:**
	<table>
	<tr><th>Nama Status</th><th>Atribut Status</th><th>Deskripsi</th></tr>
	<tr><td>Membuat</td><td>Status menengah</td><td>Instans telah dibuat tetapi belum berjalan.</td></tr>
	<tr><td>Berjalan</td><td>Status stabil</td><td>Instans berjalan normal, dan Anda dapat menjalankan layanan pada instans ini.</td></tr>
	<tr><td>Memulai ulang</td><td>Status menengah</td><td>Operasi mulai ulang telah dilakukan untuk instans melalui konsol atau API, tetapi instans belum berjalan. Jika status ini bertahan lama, mungkin ada pengecualian.</td></tr>
	<tr><td>Menginstal ulang</td><td>Status menengah</td><td>Sistem instans telah diinstal ulang atau disknya telah dikonfigurasi ulang melalui konsol atau API, tetapi instans belum berjalan.</td></tr>
	<tr><td>Mematikan</td><td>Status menengah</td><td>Operasi pematian telah dilakukan untuk instans melalui konsol atau API, tetapi instans belum dimatikan. Jika status ini bertahan lama, mungkin ada pengecualian. Kami tidak menyarankan pematian paksa.</td></tr>
	<tr><td>Pematian</td><td>Status stabil</td><td>Instans telah dimatikan secara normal dan tidak dapat menyediakan layanan eksternal. Beberapa atribut instans hanya dapat diubah saat instans dalam status mati.</td></tr>
	<tr><td>Menghentikan</td><td>Status menengah</td><td>Instans telah kedaluwarsa selama 7 hari atau pengguna telah melakukan operasi penghentian, namun belum selesai.</td></tr>
	<tr><td>Klaim ulang</td><td>Status stabil</td><td>Instans bayar sesuai pemakaian telah dihentikan secara manual selama kurang dari 2 jam dan dimasukkan ke tempat sampah. Dalam status ini, instans tidak menyediakan layanan eksternal.</td></tr>
	<tr><td>Dirilis</td><td>Status stabil</td><td>Operasi rilis telah selesai. Instans asli tidak ada lagi, tidak dapat menyediakan layanan, dan datanya benar-benar dihapus.</td></tr>
</table>
- **Transisi Status Instans:**
![](https://main.qcloudimg.com/raw/2de51f523cc5592c5daeecf179945cfe.jpg)

## Meluncurkan instans
 - Setelah instans diluncurkan, instans tersebut akan memasuki status pembuatan. Misalnya dalam status ini, spesifikasi perangkat kerasnya akan dikonfigurasi sesuai dengan [jenis instans](https://intl.cloud.tencent.com/document/product/213/11518) yang ditentukan, dan sistem akan meluncurkan instans menggunakan citra yang ditentukan saat peluncuran.
 - Instans akan memasuki status berjalan setelah dibuat. Instans dalam status berjalan dapat dihubungkan dan diakses secara normal.

Untuk informasi selengkapnya tentang startup instans, lihat [Membuat instans](https://intl.cloud.tencent.com/document/product/213/4855), [Login ke instans Windows](https://intl.cloud.tencent.com/document/product/213/5435), dan [Login ke instans Linux](https://intl.cloud.tencent.com/document/product/213/5436).

## Memulai ulang instans
Sebaiknya Anda memulai ulang instans melalui Tencent Cloud Console atau Tencent Cloud API daripada menjalankan perintah mulai ulang OS dalam instans.
 - Setelah operasi mulai ulang dilakukan, instans akan memasuki status mulai ulang.
 - Memulai ulang instans seperti memulai ulang komputer. Setelah dimulai ulang, instans akan mempertahankan alamat IP publik, alamat IP pribadi, dan semua data di disknya.
 - Bergantung pada konfigurasinya, memulai ulang instans biasanya membutuhkan waktu puluhan detik hingga beberapa menit.

Untuk informasi selengkapnya tentang cara memulai ulang instans, lihat [Memulai Ulang Instans](https://intl.cloud.tencent.com/document/product/213/4928).

## Mematikan instans
Anda dapat mematikan instans melalui konsol atau API.
 - Mematikan instans seperti mematikan komputer.
 - Instans pematian tidak lagi menyediakan layanan eksternal, tetapi penagihan instans berlanjut.
 - Instans pematian akan tetap ditampilkan di konsol.
 - Pematian diperlukan untuk beberapa operasi konfigurasi seperti menyesuaikan konfigurasi perangkat keras dan mengatur ulang kata sandi.
 - Operasi pematian tidak mengubah IP publik CVM, IP pribadi, atau data apa pun pada disknya.
 
Untuk informasi selengkapnya tentang mematikan instans, lihat [Mematikan Instans](https://intl.cloud.tencent.com/document/product/213/4929).

## Menghentikan dan merilis instans
Jika tidak lagi memerlukan instans, Anda dapat menghentikan dan merilisnya melalui Tencent Cloud Console atau API.

- Penghentian manual: instans bayar sesuai pemakaian akan dirilis setelah disimpan di tempat sampah selama maksimal 2 jam.
- Penghentian otomatis karena pembayaran kedaluwarsa atau lewat jatuh tempo: instans bayar sesuai pemakaian akan otomatis dihentikan ketika saldo turun di bawah 0 selama 2 jam 15 hari. Penagihan akan berlanjut selama 2 jam pertama, kemudian instans akan dimatikan dan tidak lagi ditagih. Instans bayar sesuai pemakaian yang lewat jatuh tempo tidak akan masuk ke tempat sampah dan dapat dilihat di daftar instans. Anda dapat terus menggunakan instans jika Anda memperbaruinya dalam waktu yang ditentukan.

Ketika sebuah instans dihentikan, disk sistem dan disk datanya yang ditentukan saat pembelian akan dirilis. Namun, disk cloud yang dipasang pada instans tidak akan terpengaruh.
Untuk informasi selengkapnya tentang menghentikan instans, lihat [Menghentikan Instans](https://intl.cloud.tencent.com/document/product/213/4930).
