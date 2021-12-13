### Apakah snapshot tersedia di semua zona ketersediaan?
Ya.

### Apakah membuat snapshot akan memengaruhi performa disk?
Membuat snapshot akan menempati I/O disk cloud dalam jumlah kecil. Kami sarankan untuk membuat snapshot saat bisnis sedang lambat.

### Berapa lama waktu yang dibutuhkan untuk membuat snapshot?
Waktu yang diperlukan untuk membuat snapshot dipengaruhi oleh faktor-faktor seperti jumlah penulisan disk dan operasi baca-tulis yang mendasarinya. Membuat snapshot tidak akan memengaruhi penggunaan disk Anda.

### Apakah saya perlu mematikan CVM untuk memutar kembali snapshot?
- Untuk disk cloud yang sudah dipasang ke CVM, Anda harus mematikan CVM agar bisa memutar kembali snapshot.
- Untuk disk cloud yang belum dipasang, Anda bisa langsung memutar kembali snapshot.

### Bagaimana cara menghitung ukuran snapshot lengkap pertama dari disk cloud?
Snapshot pertama yang dibuat di disk cloud adalah snapshot lengkap yang menyalin semua data dari disk cloud pada satu titik waktu. Ukuran snapshot sama dengan kapasitas disk cloud yang digunakan. Misalnya, jika total kapasitas disk cloud adalah 200 GB dan telah digunakan 122 GB, ukuran snapshot lengkap pertama adalah 122 GB.

### Bisakah saya mengunduh atau mengekspor snapshot instans CVM ke perangkat lokal?
Tidak. Snapshot tidak bisa diunduh atau diekspor ke perangkat lokal. Anda perlu membuat citra kustom dari snapshot lalu mengekspor citranya.

### Apakah snapshot otomatis berbeda atau bertentangan dengan snapshot manual?
Tidak. Anda bisa menggunakan keduanya secara bersamaan. Namun, Anda tidak bisa membuat snapshot manual saat snapshot otomatis sedang dibuat.
- Anda tidak bisa membuat snapshot disk kustom sampai snapshot disk otomatis selesai dibuat, dan sebaliknya.
- Jika satu snapshot yang dibuat dari disk besar bertahan lebih lama dari interval antara dua snapshot otomatis, maka snapshot otomatis berikutnya akan dilewati. Misalnya, jika Anda mengonfigurasi snapshot otomatis yang akan dibuat pada 9:00, 10:00, dan 11:00, serta snapshot otomatis yang dibuat pada 9:00 berlangsung selama 70 menit dan berakhir pada 10:10, maka snapshot otomatis berikutnya akan dibuat pada pukul 11:00 dan bukan pada pukul 10:00.

### Bisakah saya membuat snapshot untuk disk lokal?
Tidak. Kami sarankan agar Anda menggunakan redundansi data di lapisan aplikasi atau membuat serangkaian deployment untuk kluster guna meningkatkan ketersediaan aplikasi.

### Setelah saya merilis cloud disk, apakah snapshot lokal akan dihapus?
Tidak. Anda perlu menghapus snapshot melalui Konsol atau API. Untuk informasi selengkapnya, lihat [Menghapus Snapshot](https://intl.cloud.tencent.com/document/product/362/5758).

### Mengapa kapasitas disk yang digunakan dan ditampilkan di sistem file berbeda dari ukuran snapshot?
Snapshot disk cloud adalah kloning atau cadangan tingkat blok. Secara umum, kapasitas snapshot akan lebih besar daripada kapasitas data yang ditampilkan dalam sistem file karena:
- Blok data yang mendasarinya menyimpan metadata dari sistem file.
- Beberapa data dihapus. Menghapus data akan mengubah blok data tertulis, yang akan dicadangkan ke snapshot.

### Bagaimana cara mencegah snapshot dihapus oleh Tencent Cloud?
- Snapshot manual: Tencent Cloud tidak akan pernah menghapusnya, terlepas dari apakah disk atau instans terkait sudah dirilis.
- Snapshot terjadwal: Anda bisa mengatur periode penyimpanan snapshot terjadwal ke retensi jangka panjang untuk mencegahnya agar tidak dihapus. Dengan cara ini, hanya snapshot yang dibuat paling awal yang akan dihapus ketika sudah mencapai kuota snapshot. Untuk petunjuk terperinci, lihat [Snapshot Terjadwal](https://intl.cloud.tencent.com/document/product/362/35238) dan [Batas Penggunaan](https://intl.cloud.tencent.com/document/product/362/32406).

### Bagaimana cara menghapus snapshot untuk mengurangi biaya pencadangan?
- Untuk snapshot disk cloud, Anda bisa menghapusnya langsung melalui Konsol atau API. Untuk informasi selengkapnya, lihat [Menghapus Snapshot](https://intl.cloud.tencent.com/document/product/362/5758).
- Untuk snapshot yang terkait dengan citra kustom, Anda harus menghapus citra kustom terlebih dahulu, lalu [menghapus snapshot](https://intl.cloud.tencent.com/document/product/362/5758).

### Apakah snapshot otomatis akan dihapus setelah instans kedaluwarsa atau disk cloud dilepaskan?
Tidak. Snapshot otomatis tidak akan dihapus setelah instans kedaluwarsa atau disk cloud dilepaskan karena disimpan berdasarkan kebijakan periode penyimpanan snapshot terjadwal. Untuk mengubah kebijakan snapshot terjadwal, lihat [Snapshot Terjadwal](https://intl.cloud.tencent.com/document/product/362/35238).

### Bagaimana cara menghapus snapshot dari tempat citra atau disk cloud dibuat?
- Snapshot dari tempat cloud disk dibuat: Anda bisa menghapus snapshot secara terpisah. Setelah menghapus snapshot, Anda tidak akan bisa mengoperasikan bisnis yang bergantung pada data snapshot asli.
- Snapshot dari tempat citra kustom dibuat: Anda harus menghapus citra terlebih dahulu, kemudian menghapus snapshot.
- Snapshot dari tempat instans dibuat: Anda bisa menghapus snapshot secara terpisah. Setelah menghapus snapshot, Anda tidak akan bisa mengoperasikan bisnis yang bergantung pada data snapshot asli.

### Apakah kebijakan snapshot akan gagal dijalankan jika saya membuat citra kustom atau disk cloud berdasarkan snapshot terjadwal?
Tidak.


### Bisakah disk cloud memiliki beberapa kebijakan snapshot otomatis?
Tidak.

### Bagaimana cara mencegah kehilangan data yang disebabkan oleh operasi yang salah?
Anda bisa membuat snapshot untuk mencadangkan data sebelum melakukan tindakan berisiko. Misalnya, Anda bisa membuat snapshot sebelum mengubah file sistem penting, memigrasikan instans dari jaringan klasik ke VPC, mencadangkan data, memulihkan instans yang dirilis secara tidak sengaja, mencegah serangan jaringan, mengubah sistem operasi, atau memberikan dukungan data untuk lingkungan produksi. Untuk informasi selengkapnya, lihat [Membuat Snapshot](https://intl.cloud.tencent.com/document/product/362/5755). Jika terjadi kesalahan, Anda bisa [memutar kembali snapshot](https://intl.cloud.tencent.com/document/product/362/5756) untuk mengurangi risiko.

### Saya membuat instans di wilayah Guangzhou dan membuat snapshot untuk disk data instans. Setelah instans kedaluwarsa dan dirilis, saya membeli instans lain di wilayah Guangzhou. Bisakah saya memutar kembali snapshot di instans baru untuk memulihkan instans yang asli?
Tidak. Snapshot hanya bisa dikembalikan ke disk cloud tempatnya dibuat. Anda bisa menggunakan snapshot dari disk data sebelumnya untuk membuat disk cloud dan memasang disk cloud tersebut ke instans baru. Untuk informasi selengkapnya, lihat [Membuat Disk Cloud Menggunakan Snapshot](https://intl.cloud.tencent.com/document/product/362/5757) dan [Memasang Disk Cloud](https://intl.cloud.tencent.com/document/product/362/32401).

### Apa perbedaan antara snapshot dan citra?
Jika tidak ada disk data yang dipasang ke instans dan semua data ditulis pada disk sistem, maka data pada disk sistem tidak bisa dilindungi dengan cara membuat citra. Citra tidak bisa dijadwalkan untuk pencadangan berkelanjutan. Setelah data disk sistem rusak, Anda hanya bisa memulihkan data ke status saat citra pertama kali dibuat. Oleh karena itu, citra tidak cocok untuk perlindungan data. Perbedaannya secara khusus adalah sebagai berikut:
<table>
		<tr>
		<th width="10%">Nama</th>
		<td width="45%">Snapshot</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/213/4940">Citra</a></td>
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

### Bagaimana cara memigrasikan data snapshot dari akun A ke akun B?
Snapshot tidak bisa dimigrasikan. Sebagai gantinya, Anda bisa membuat citra dari snapshot yang ingin dimigrasikan dan berbagi citra dengan akun lain.

### Bisakah saya membuat citra kustom dari data snapshot disk?
Tidak. Anda hanya bisa membuat citra kustom dari snapshot disk sistem.



