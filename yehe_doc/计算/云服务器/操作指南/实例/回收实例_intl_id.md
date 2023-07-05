Dokumen ini menjelaskan cara memulihkan instans Cloud Virtual Machine (CVM) dari keranjang sampah. Untuk informasi selengkapnya, lihat [Pembayaran Jatuh Tempo](https://intl.cloud.tencent.com/document/product/213/2181). 

## Keranjang Sampah
Keranjang sampah Tencent Cloud menyediakan mekanisme kepemilikan kembali instans CVM sebagai berikut:
- **Pay-as-you-go instances** (Instans bayar sesuai pemakaian): instans bayar sesuai pemakaian akan memasuki keranjang sampah setelah dihentikan oleh pengguna atau pada waktu yang dijadwalkan. Jika akun lewat jatuh tempo, instans bayar sesuai pemakaian tidak akan masuk ke keranjang sampah. Ini akan dirilis setelah akun telah jatuh tempo selama 2 jam dan 15 hari.

### Instans bayar sesuai pemakaian di keranjang sampah

 - **Retention period** (Periode retensi): instans yang dihentikan oleh pengguna akan disimpan di keranjang sampah selama 2 jam.
 - **Expiry processing** (Pemrosesan kedaluwarsa): jika instans tidak diperpanjang sebelum periode retensi berakhir, sistem akan melepaskan sumber daya instans dan secara otomatis [mengakhiri instans](https://intl.cloud.tencent.com/document/product/213/4930), yang tidak dapat dipulihkan. IP elastis yang terikat pada instans ini juga dirilis.
 - **Mounting relationship** (Hubungan pemasangan): setelah instans memasuki keranjang sampah, hubungan pemasangannya dengan Cloud Load Balancer, Cloud Block Storage, dan Classiclink **not be automatically terminated** (tidak akan dihentikan secara otomatis).
 - **Operation restriction** (Pembatasan operasi): instans di keranjang sampah hanya dapat [dipulihkan setelah pembaruan](https://intl.cloud.tencent.com/document/product/213/6143) atau [dihentikan](https://intl.cloud.tencent.com/document/product/213/4930). Beberapa jenis instans mendukung [membuat citra kustom](https://intl.cloud.tencent.com/document/product/213/4942)
 
>! 
> - Anda tidak dapat memulihkan instans bayar sesuai pemakaian dari keranjang sampah jika akun Anda lewat jatuh tempo. Harap perbarui pembayaran terlebih dahulu.
> - Instans bayar sesuai pemakaian disimpan di keranjang sampah selama maksimal 2 jam. Harap perhatikan waktu rilis dan perbarui pembayaran tepat waktu untuk memulihkan instans.
> - Instans bayar sesuai pemakaian tidak dapat masuk ke keranjang sampah jika akun Anda jatuh tempo. Anda dapat melihatnya di halaman daftar instans CVM. Instans akan dirilis setelah akun Anda jatuh tempo selama 2 jam dan 15 hari.

## Memulihkan Instans
 1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/).
 2. Di bilah sisi kiri, klik **Recycle Bin** (Keranjang Sampah) -> **Instance Recycle Bin** (Keranjang Sampah Instans) untuk masuk ke daftar daur ulang CVM.
 3. Pulihkan satu instans: temukan instans yang akan dipulihkan dalam daftar, klik **Recover** (Pulihkan) di kolom **Operation** (Operasi), dan selesaikan pembayaran perpanjangan.
 4. Pulihkan instans dalam kumpulan: pilih semua instans yang akan dipulihkan, klik **Recover Selected** (Pulihkan Instans yang Dipilih) di bagian atas, dan selesaikan pembayaran perpanjangan.

