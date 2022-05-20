## Skenario Operasi
Sesuai dengan kebutuhan bisnis Anda, Anda dapat mengembalikan instans bayar sesuai pemakaian di konsol secara mandiri.
- Setelah instans bayar sesuai pemakaian dikembalikan, instans tersebut akan dipindahkan ke keranjang sampah TencentDB dan disimpan selama 24 jam. Selama periode penyimpanan, instans tidak dapat diakses tetapi dapat dipulihkan.

Setelah instans dikembalikan, maka statusnya berubah menjadi "Terisolasi", tidak ada biaya terkait yang akan dikenakan.
>!
>- Setelah instans dihentikan, datanya tidak dapat dipulihkan, dan file cadangannya juga akan dihentikan, sehingga data tidak dapat dipulihkan di cloud. Harap simpan file cadangan Anda dengan aman di tempat lain terlebih dahulu.
>- Saat instans dihentikan, sumber daya IP-nya akan dirilis secara bersamaan. Jika instans memiliki instans baca saja atau konfigurasi pub/sub:
> - Instans baca saja akan dihentikan pada saat yang sama.
> - Setelah instans dihentikan, konfigurasi pub/sub yang ada pada instans akan dihapus.


## Petunjuk
1. Login ke [Konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver), pilih instans target dalam daftar instans, dan pilih **More** (Lainnya) > **Terminate/Return** (Hentikan/Kembalikan) di kolom "Operasi".
![](https://main.qcloudimg.com/raw/be837273695eb17b86447852317fb45f.png)
2. Di kotak dialog pop-up, berikan persetujuan Anda dan klik **Terminate** (Hentikan).
![](https://main.qcloudimg.com/raw/eed621d2fb6827d94ab5b2875a42fc84.png)


