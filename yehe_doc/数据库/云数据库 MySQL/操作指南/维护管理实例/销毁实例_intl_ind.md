## Skenario Operasi
Berdasarkan kebutuhan bisnis Anda, Anda dapat mengembalikan instans bayar sesuai pemakaian di konsol secara mandiri.
- Setelah instans bayar sesuai pemakaian dikembalikan, instans tersebut akan dipindahkan ke keranjang sampah TencentDB dan disimpan selama 24 jam. Selama periode retensi, instans tidak dapat diakses tetapi dapat dipulihkan.

Setelah instans dikembalikan, setelah statusnya berubah menjadi "terisolasi", tidak ada biaya terkait yang akan dikenakan.
>
>- Setelah instans dihentikan, datanya tidak dapat dipulihkan, dan file cadangannya juga akan dihentikan, sehingga data tidak dapat dipulihkan di cloud. Harap simpan file cadangan Anda dengan aman di tempat lain terlebih dahulu.
>- Saat instans dihentikan, sumber daya IP-nya akan dirilis secara bersamaan. Jika instans memiliki instans baca saja atau instans pemulihan bencana:
> - Instans baca saja akan dihentikan pada saat yang sama.
> - Instans pemulihan bencana akan memutuskan sambungan sinkronisasinya dan dipromosikan ke instans master secara otomatis.


## Petunjuk
1. Login ke [Konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), pilih instans target dalam daftar instans, dan pilih **More** (Lainnya) > **Terminate/Return** (Hentikan/Kembalikan) atau **Terminate/Return & Refund** (Hentikan/Kembalikan & Kembalikan Dananya) di kolom "Operasi".
![](https://main.qcloudimg.com/raw/ea0d80564ad54c6c9e3ea43070c71f20.png)
2. Di kotak dialog pop-up, pilih "Saya telah membaca dan menyetujui Aturan Penghentian" dan klik **Terminate Now** (Hentikan Sekarang).

>
![](https://main.qcloudimg.com/raw/6e376a4a726195aefee841930577a5b3.png)
