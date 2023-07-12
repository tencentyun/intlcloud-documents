### Disk cloud telah mengadopsi mekanisme redundansi tiga salinan untuk keamanan data.Mengapa kita masih perlu menggunakan snapshot?
Dalam situasi ketika kesalahan data tingkat logika terjadi, misalnya, anggaplah pengguna menghapus data secara tidak sengaja, atau jika data rusak oleh virus atau pengecualian sistem file, ketiga salinan data yang disimpan akan terpengaruh dan data riwayat tidak dapat dipulihkan.Jika Anda telah membuat snapshot sebelumnya, Anda dapat menggunakan snapshot untuk memulihkan data ke titik waktu snapshot dibuat.
![](https://main.qcloudimg.com/raw/824b34d077d2e58114e08de86edae2b8.png)
Misalkan administrator membuat snapshot A untuk disk cloud pada pukul 11:00, dan disk cloud terinfeksi virus pada pukul 12:00, yang menyebabkan data tersebut tidak dapat digunakan.Dalam hal ini, tiga salinan data akan diperbarui ke status 2, dan data tidak dapat dipulihkan.Untuk memulihkan data ke status tidak terinfeksi 1, Anda harus menggunakan snapshot A yang dibuat pada pukul 11:00.

### Mengapa penyimpanan disk yang digunakan yang ditampilkan di sistem file berbeda dari ukuran snapshot?
Snapshot disk cloud adalah kloning atau cadangan tingkat blok.Secara umum, ukuran snapshot akan lebih besar dari ukuran data yang ditampilkan di sistem file karena:
- Blok data yang mendasarinya menyimpan metadata dari sistem file.
- Beberapa data dihapus.Menghapus data akan mengubah blok data tertulis, yang akan dicadangkan ke snapshot.


### Apa perbedaan antara snapshot dan image?
Jika tidak ada disk data yang dilampirkan ke instance dan semua data ditulis pada disk sistem, data pada disk sistem tidak dapat dilindungi dengan membuat image.Image tidak bisa dijadwalkan untuk pencadangan berkelanjutan.Setelah data disk sistem rusak, Anda hanya dapat memulihkan data ke status saat image pertama kali dibuat.Oleh karena itu, image tidak cocok untuk perlindungan data.Perbedaannya secara khusus adalah sebagai berikut:

<table>
<tr>
<th width="10%">Nama</th>
<td width="45%">Snapshot</td>
<td><a href="https://intl.cloud.tencent.com/document/product/213/4940">Image</a></td>
</tr>
<tr>
<th>Karakteristik</th>
<td>Data cadangan disk cloud pada titik waktu tertentu</td>
<td>Templat konfigurasi perangkat lunak CVM, yang berisi informasi tentang sistem operasi dan program yang sudah diinstal sebelumnya</td>
</tr>
<tr>
<th>Kasus Penggunaan</th>
<td>
<ul>
<li>Cadangkan data bisnis penting secara teratur</li>
<li>Cadangkan data sebelum operasi besar</li>
<li>Buat beberapa salinan data</li>
</ul>
</td>
<td>
<ul>
<li>Cadangkan sistem yang tidak akan berubah dalam jangka pendek</li>
<li>Deploy aplikasi secara berkelompok</li>
<li>Migrasikan sistem</li>
</ul>
</td>
</tr>
</table>


### Mengapa sebagian snapshot tidak dapat digunakan untuk membuat image?
Anda dapat membuat snapshot untuk disk sistem dan disk data.Namun, hanya snapshot dari disk sistem yang dapat digunakan untuk membuat image khusus.

### Mengapa saya tidak bisa menghapus snapshot?
Untuk menghapus snapshot, pastikan snapshot yang ingin Anda hapus tidak terkait dengan image apa pun.Untuk mengueri snapshot image terkait, buka halaman [image](https://console.cloud.tencent.com/cvm/image) dan klik ID/Nama image.

### Bagaimana snapshot yang dibuat dari image ditagih?
Image menggunakan layanan snapshot CBS untuk penyimpanan data.Snapshot terkait dari image khusus akan ditagih berdasarkan ukuran penyimpanan.Untuk melihat ukuran snapshot Anda, buka [Ikhtisar Snapshot](https://console.cloud.tencent.com/cvm/snapshot/overview).

### Bagaimana image yang dibagikan ditagih?
Pemilik image yang dibagikan dikenakan biaya snapshot, sedangkan akun penerima tidak akan dikenakan biaya.Untuk informasi selengkapnya tentang penagihan snapshot, lihat [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/362/32415).



### Apa itu snapshot terjadwal?
Snapshot terjadwal dibuat secara otomatis untuk disk cloud sesuai dengan kebijakan snapshot terjadwal terkait.Untuk menggunakan fitur ini, Anda harus terlebih dahulu membuat kebijakan snapshot terjadwal dan mengaitkannya dengan disk cloud.Untuk informasi selengkapnya, lihat [Menjadwalkan snapshot](https://intl.cloud.tencent.com/document/product/362/35238).


### Batasan apa yang dimiliki snapshot terjadwal?
Maksimal 30 kebijakan snapshot terjadwal dapat dibuat di satu wilayah.Setiap kebijakan snapshot terjadwal dapat dikaitkan dengan hingga 200 disk cloud.Selain itu, snapshot yang dibuat sesuai dengan kebijakan snapshot terjadwal harus sesuai dengan kuota snapshot.Untuk informasi selengkapnya, lihat [Batas Penggunaan](https://intl.cloud.tencent.com/document/product/362/32406).

### Bagaimana snapshot dibuat?
Anda dapat membuat snapshot menggunakan metode berikut:
- Snapshot khusus: Anda dapat membuat snapshot secara manual untuk menyimpan data disk cloud dengan cepat pada titik waktu tertentu.Untuk informasi selengkapnya, lihat [Membuat Snapshot](https://intl.cloud.tencent.com/document/product/362/5755).
- Snapshot terjadwal: Anda dapat mengaitkan kebijakan snapshot terjadwal dengan disk cloud untuk membuat dan menghapus snapshot secara berkala.Untuk informasi selengkapnya, lihat [Snapshot Terjadwal](https://intl.cloud.tencent.com/document/product/362/35238).

### Apakah snapshot tersedia di semua zona ketersediaan?
Ya.

### Bagaimana snapshot ditagih?
Snapshot ditagih sesuai dengan ukuran penyimpanan snapshot total Anda di setiap wilayah dengan cara **dibayar sesuai pemakaian**; dan biaya dihitung dan dipotong pada titik setiap jam.Untuk informasi selengkapnya tentang penagihan, lihat [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/362/32415) dan [Ikhtisar Harga](https://intl.cloud.tencent.com/document/product/362/2413).

### Apakah saya perlu melepas disk atau menghentikan semua operasi baca dan tulis sebelum membuat snapshot?
Tidak. Anda dapat membuat snapshot real-time saat disk terhubung dan digunakan, tanpa memengaruhi operasi normal bisnis Anda.Namun, snapshot hanya dapat menangkap data tertulis, bukan data yang di-cache dari disk cloud.Untuk memastikan semua data aplikasi diambil, kami menyarankan Anda menangguhkan semua operasi I/O disk sebelum membuat snapshot.Untuk disk cloud yang digunakan sebagai disk sistem, kami sarankan Anda mematikan CVM untuk membuat snapshot yang lebih lengkap.

### Apakah membuat snapshot akan memengaruhi performa disk?
Membuat snapshot akan menempati sejumlah kecil I/O disk cloud. Kami sarankan Anda untuk membuat snapshot selama jam sibuk bisnis Anda.

### Berapa lama waktu yang dibutuhkan untuk membuat snapshot?
Waktu yang diperlukan untuk membuat snapshot dipengaruhi oleh faktor-faktor seperti jumlah penulisan disk dan operasi baca-tulis yang mendasarinya.Membuat snapshot tidak akan memengaruhi penggunaan disk Anda.

### Bagaimana cara membuat disk cloud menggunakan snapshot?
Untuk informasi selengkapnya, lihat [Membuat Disk Cloud Menggunakan Snapshot](https://intl.cloud.tencent.com/document/product/362/5757).

### Bagaimana cara mengembalikan snapshot?
Untuk informasi selengkapnya, lihat [Mengembalikan Snapshot](https://intl.cloud.tencent.com/document/product/362/5756).

### Apakah saya perlu mematikan CVM untuk mengembalikan ke snapshot?
- Untuk disk cloud yang telah dilampirkan ke CVM, Anda harus mematikan CVM untuk mengembalikannya ke snapshot.
- Untuk disk cloud yang belum dilampirkan ke CVM, Anda dapat langsung mengembalikannya ke snapshot.

### Dapatkah saya membaca snapshot sebelumnya untuk memulihkan disk cloud?
Ya.Anda dapat menggunakan snapshot yang ada yang dibuat kapan saja untuk memulihkan data, terlepas dari titik waktu snapshot.

### Dapatkah saya menghapus snapshot sumber saat snapshot tersebut sedang direplikasi?
Tidak. Snapshot sumber tersebut hanya dapat dihapus setelah replikasi selesai.

### Apakah snapshot baru yang dibuat dengan replikasi masih terkait dengan disk sumber snapshot?
Snapshot yang dibuat melalui replikasi lintas wilayah tidak lagi terkait dengan disk sumber snapshot sumber.Fitur pengembalian (rollback) tidak tersedia untuk snapshot yang direplikasi.

### Apakah snapshot terkait akan dihapus saat CVM dihentikan?
Tidak, snapshot terkait tidak akan dihapus secara otomatis.Anda dapat menghapusnya melalui konsol atau API.Untuk informasi selengkapnya, lihat [Menghapus Snapshot](https://intl.cloud.tencent.com/document/product/362/5758).

### Bagaimana cara menghapus snapshot?
- Untuk snapshot disk cloud, Anda dapat menghapusnya langsung melalui konsol atau API.Untuk informasi selengkapnya, lihat [Menghapus Snapshot](https://intl.cloud.tencent.com/document/product/362/5758).
- Untuk snapshot yang terkait dengan image khusus, Anda harus menghapus image khusus terlebih dahulu, lalu [menghapus snapshot](https://intl.cloud.tencent.com/document/product/362/5758).

### Dapatkah saya menggunakan snapshot yang dibuat dari disk sistem untuk membuat disk cloud?
Tidak. Anda hanya dapat menggunakan snapshot dari disk sistem untuk membuat image khusus.

### Apakah snapshot mendukung fitur replikasi lintas wilayah?
Ya.Anda dapat menggunakan fitur ini untuk memigrasikan data dan layanan ke wilayah lain dengan mudah, atau membangun sistem pemulihan bencana lintas wilayah Anda.Untuk informasi selengkapnya, lihat [Mereplikasi Snapshot Lintas Wilayah](https://intl.cloud.tencent.com/document/product/362/31623).

