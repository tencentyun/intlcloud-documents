## Instans CVM Bayar Sesuai Pemakaian

![](https://main.qcloudimg.com/raw/463d6b815dcf2677ebe28f9683d14430.jpg)

### Catatan
- Setelah Anda berhenti menggunakan sumber daya bayar sesuai pemakaian, **hentikan sumber daya tersebut sesegera mungkin** untuk menghindari pengurangan biaya.
- Setelah instans CVM dihentikan atau diambil alih, datanya akan dihapus dan tidak dapat dipulihkan.
- Karena konsumsi sumber daya aktual terus berubah, mungkin ada beberapa perbedaan kecil untuk saldo yang tercantum di peringatan saldo hampir habis.

### Peringatan

<table>
	<tr><th>Jenis Peringatan</th><th>Deskripsi</th></tr>
	<tr><td><b>Pengingat pembayaran melewati jatuh tempo</b></td><td>Sumber daya bayar sesuai pemakaian ditagih pada jam tersebut. Saat saldo akun Anda minus, pembuat akun Tencent Cloud, kolaborator sumber daya global, dan kolaborator keuangan Anda akan menerima pemberitahuan melalui email dan SMS.</td></tr>
	<tr><td><b>Peringatan pembayaran melewati jatuh tempo</b></td><td>Fitur ini dinonaktifkan secara default.</td></tr>
</table>

### Kebijakan pembayaran lewat waktu
Saat saldo akun Anda di bawah nol, Anda dapat terus menggunakan instans CVM selama 2 jam ke depan. Kami juga akan terus menagih Anda untuk penggunaan ini. Setelah 2 jam, jika saldo akun Anda tetap negatif, instans CVM Anda akan dimatikan otomatis dan penagihan akan berhenti.
Setelah penonaktifan otomatis, instance CVM Anda melewati tahapan berikut:
<table>
	<tr><th>Waktu Sejak Pematian</th><th>Deskripsi</th></tr>
	<tr><td rowspan=2><b>≤ 15 hari</b></td><td>Jika akun diisi ulang hingga saldo plus, penagihan dilanjutkan dan Anda dapat terus menggunakan instans CVM.</td></tr>
	<tr><td>Jika saldo akun tetap minus, Anda tidak akan dapat memulai instans CVM.</td></tr>
	<tr><td><b>> 15 hari</b></td><td>Jika akun tidak diisi ulang hingga saldo plus, CVM bayar sesuai pemakaian akan diambil alih. Semua data akan dihapus dan tidak dapat dipulihkan. Saat CVM diambil alih, pembuat akun Tencent Cloud dan semua kolaborator akan menerima pemberitahuan melalui email dan SMS.</td></tr>
</table>

## Jaringan Tagihan per traffic
<table>
	<tr><th>Jenis Peringatan</th><th>Deskripsi</th></tr>
	<tr><td><b>Peringatan saldo</b></td><td>Konsumsi lalu lintas jaringan cenderung fluktuatif secara signifikan dan sulit diprediksi. Oleh karena itu, kami tidak menawarkan peringatan saldo.</td></tr>
	<tr><td><b>Peringatan pembayaran melewati jatuh tempo</b></td><td>Saat saldo minus, Anda dapat terus menggunakan jaringan tagihan per lalu lintas selama <b>2 jam ke depan</b>. Kami juga akan terus mengirimkan tagihan untuk penggunaan ini. Setelah 2 jam, jika saldo akun tetap minus, layanan jaringan tagihan per lalu lintas akan berhenti otomatis. </br>Setelah akun diisi ulang hingga saldo plus, layanan akan dilanjutkan. Periksa instans CVM dan instans CLB yang terdampak dan pastikan bahwa pengaturan sebelumnya telah dipulihkan.</td></tr>
</table>

>! Untuk informasi tentang biaya lalu lintas, lihat [Penagihan Jaringan Publik](https://intl.cloud.tencent.com/document/product/213/10578).
>
