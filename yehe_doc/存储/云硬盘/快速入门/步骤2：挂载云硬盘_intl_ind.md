## Overview (Ikhtisar)
Dokumen ini menggunakan disk cloud `cbs-test` yang akan dipasang di Zona 2 Beijing sebagai contoh untuk menggambarkan cara memasangkan disk tersebut ke CVM melalui konsol.
>?
>- Disk cloud hanya dapat dipasang ke CVM yang berada di zona ketersediaan yang sama.
>- Untuk informasi selengkapnya tentang cara memasang disk cloud, silakan lihat [Memasang Disk Cloud](https://intl.cloud.tencent.com/document/product/362/32401).
>

## Prerequisites (Prasyarat)
- Anda sudah [membuat disk cloud `cbs-test`](https://intl.cloud.tencent.com/document/product/362/31647).
- Anda memiliki CVM yang berjalan di zona ketersediaan yang sama (yaitu Zona 2 Beijing dalam contoh ini) dengan disk cloud. Untuk informasi selengkapnya tentang cara membeli dan memulai CVM, silakan lihat [Menyesuaikan Konfigurasi CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517) dan [Menyesuaikan Konfigurasi CVM Windows](https://intl.cloud.tencent.com/document/product/213/10516).

## Directions (Petunjuk)
1. Login ke konsol CVM dan klik [**Cloud Block Storage**](https://console.cloud.tencent.com/cvm/cbs) di bilah sisi kiri.
2. Pilih **Beijing** di bagian atas halaman, cari disk cloud `cbs-test`, dan pilih **More** > **Mount** (Lainnya > Pasang) di bawah kolom **Operation** (Operasi).

3. Di jendela pop-up, pilih instans CVM tempat disk cloud akan dipasang, kemudian klik **Next** > **Mount Now** (Berikutnya > Pasang Sekarang).
>?Anda dapat mencentang **Release upon instance termination** (Rilis saat penghentian instans) sesuai dengan keadaan yang sebenarnya.
>
Kembali ke halaman daftar disk cloud. Disk cloud yang berstatus **Mounting** (Dipasang) menunjukkan bahwa disk tersebut sedang dipasang ke CVM. Setelah statusnya berubah menjadi **Mounted** (Terpasang), itu artinya pemasangan berhasil dilakukan.


## Subsequent Operations (Operasi Berikutnya)
Setelah disk cloud dipasang ke CVM, disk cloud akan bertindak sebagai disk data, yang secara default berfungsi secara offline. Anda harus menginisialisasi disk cloud terlebih dahulu dengan memformat, mempartisi, dan membuat sistem file. Untuk informasi selengkapnya, silakan lihat [Menginisialisasi Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31645).






