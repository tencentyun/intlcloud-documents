

## Instans TencentDB Bayar Sesuai Pemakaian
> !Jika Anda tidak lagi menggunakan sumber daya bayar sesuai pemakaian, **terminate them as soon as possible** (segera hentikan sumber daya tersebut) untuk menghindari biaya tambahan.
> Karena konsumsi sumber daya Anda yang sebenarnya terus berubah, beberapa perbedaan kecil mungkin ada untuk saldo yang Anda nyatakan.

### Peringatan
- Sumber daya bayar sesuai pemakaian ditagih pada jam tersebut. Saat saldo akun Anda menjadi negatif, sistem akan mengirimkan peringatan kepada pembuat akun Tencent Cloud Anda, kolaborator sumber daya global, dan kolaborator keuangan melalui email, SMS, dan metode lain yang dikonfigurasi dalam langganan pesan di [Pusat Pesan](https://console.cloud.tencent.com/message).


### Pemrosesan Pembayaran Jatuh Tempo
1. **From the moment your account balance becomes negative:** (Sejak saat saldo akun Anda menjadi negatif:)
 - Anda dapat terus menggunakan instans TencentDB Anda selama 24 jam sejak saldo akun Anda menjadi negatif. Kami akan terus menagih Anda untuk periode ini.
 - Jika akun Anda telah jatuh tempo selama 24 jam, **your TencentDB instance will automatically shut down** (instans TencentDB Anda akan dimatikan secara otomatis), dan penagihan akan dihentikan.

2. **After automatic shutdown:** (Setelah pematian otomatis:)
 - Dalam 3 hari setelah pematian otomatis, jika akun Anda tidak diisi ulang hingga saldo positif, Anda tidak akan dapat memulai instans TencentDB Anda; jika saldo Anda positif, penagihan berlanjut, dan Anda dapat memulai instans.
 - Jika saldo tetap negatif selama 3 hari setelah dimatikan, instans TencentDB akan diambil alih. Semua data akan dihapus dan tidak dapat dipulihkan. Pembuat akun Tencent Cloud, kolaborator sumber daya global, dan kolaborator keuangan akan diberi tahu melalui email, SMS, dll.
 
![](https://main.qcloudimg.com/raw/2a4084a3304cd60ede9a2675feda9e97.png)
