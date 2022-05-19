## Pengingat Pembayaran Jatuh Tempo untuk Instans TencentDB Bayar Sesuai Pemakaian
![](https://main.qcloudimg.com/raw/047e69df69e97cdfca9517a597b44370.png)
### Pengingat Saldo
Kami akan memperkirakan jumlah hari yang dibutuhkan saldo akun Anda menjadi negatif berdasarkan penggunaan 24 jam terakhir dan saldo saat ini. Jika kurang dari 5 hari, kami akan mengirimkan pesan pengingat. Pesan pengingat akan dikirim ke pembuat akun Tencent Cloud dan semua kolaborator melalui email dan SMS.

## Pengingat Pembayaran Jatuh Tempo
 Untuk sumber daya bayar sesuai pemakaian, biaya dipotong per jam. Ketika saldo akun Anda negatif (Poin 1 pada gambar di atas), kami akan memberi tahu pembuat akun Tencent Cloud dan semua kolaborator melalui email dan SMS.

### Pemrosesan Pembayaran Jatuh Tempo
Anda dapat terus menggunakan instans TencentDB selama 2 jam sejak akun Anda menjadi negatif.
Kami juga akan terus mengirimkan tagihan ke Anda untuk periode ini.
Ketika akun Anda telah jatuh tempo selama 2 jam, (Poin 2 pada gambar di atas), instans akan diisolasi dan menjadi tidak dapat diakses. Kami juga akan berhenti mengirimkan tagihan ke Anda untuk layanan.

Dalam waktu 24 jam setelah pematian otomatis, 
jika akun Anda tidak diisi ulang hingga saldo positif, Anda tidak akan dapat memulai instans TencentDB Anda; jika saldo Anda positif, penagihan berlanjut, dan Anda dapat memulai instans. 
Jika akun Anda tetap negatif selama 24 jam setelah dimatikan, (Poin 3 pada gambar di atas), database bayar sesuai pemakaian akan diambil alih, dan semua data akan dihapus dan tidak dapat dipulihkan.

Kami akan memberi tahu pembuat akun Tencent Cloud dan semua kolaborator melalui email dan SMS saat database diambil alih.


>- Bila Anda tidak lagi menggunakan sumber daya bayar sesuai pemakaian, hentikan sumber daya tersebut sesegera mungkin untuk menghindari pemotongan biaya lebih lanjut.
>- Setelah database dihentikan atau diambil alih, data akan dihapus dan tidak dapat dipulihkan.
>- Karena konsumsi sumber daya aktual Anda berubah dari waktu ke waktu, mungkin ada beberapa perbedaan untuk saldo yang disebutkan.

