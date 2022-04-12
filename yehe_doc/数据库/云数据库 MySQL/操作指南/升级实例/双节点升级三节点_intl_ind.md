
## Ikhtisar
Dokumen ini menjelaskan cara meningkatkan instans TencentDB for MySQL dari [dua node](https://intl.cloud.tencent.com/document/product/236/38329) ke [tiga node](https://intl.cloud.tencent.com/document/product/236/39783) di konsol.
>?
>- Hanya instans dua node TencentDB for MySQL yang dapat ditingkatkan ke tiga node.
>- Peningkatan tidak akan mengganggu layanan instans.
>- Anda juga dapat membeli instans tiga node di [halaman pembelian](https://buy.cloud.tencent.com/cdb).

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail instans.
2. Di bagian **Configuration Info** (Info Konfigurasi), klik **Upgrade to Three-node** (Tingkatkan ke Tiga node) di sebelah **Architecture** (Arsitektur).
![](https://main.qcloudimg.com/raw/cbc0ef63b4b4824a8eedf92898a039f6.png)
3. Di kotak dialog pop-up, tentukan mode replikasi data dan zona ketersediaan, lalu klik **OK** (OKE).
 - **Data Replication Mode** (Mode Replikasi Data): untuk informasi selengkapnya, lihat [Replikasi Instans Database](https://intl.cloud.tencent.com/document/product/236/7913).
 - **Multi-AZ Deployment** (Deployment Multi-AZ): Deployment multi-AZ melindungi layanan database agar tidak terganggu jika terjadi kegagalan database atau kegagalan zona ketersediaan.
    - Untuk instans tiga node, replikanya dapat digunakan di zona ketersediaan sumber atau zona ketersediaan yang berbeda. Kami sarankan Anda men-deploy satu replika di zona ketersediaan sumber dan replika lainnya di zona ketersediaan yang berbeda.
    - Saat ini, hanya beberapa zona ketersediaan sumber yang mendukung pemilihan zona ketersediaan yang berbeda sebagai zona ketersediaan replika. Anda dapat melihat zona ketersediaan sumber ini dan zona ketersediaan replika yang didukung di [halaman pembelian](https://buy.cloud.tencent.com/cdb).
![](https://main.qcloudimg.com/raw/6b1a4c2b43587cc99c7b01d544f53cd2.png)
4. Setelah pembayaran selesai, Anda akan diarahkan ke daftar instans. Setelah status instans berubah dari **Changing configuration** (Mengubah konfigurasi) menjadi **Running** (Berjalan), instans dapat digunakan secara normal.

## Pertanyaan Umum
#### Bagaimana cara melihat informasi arsitektur suatu instans?
Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, lihat informasi arsitektur di kolom **Configuration** (Konfigurasi); atau klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail instans, tempat Anda dapat melihat informasi arsitektur di bagian **Configuration Info** (Info Konfigurasi) > **Architecture** (Arsitektur).
![](https://main.qcloudimg.com/raw/e783ce5c7070b8084cf03b053d7e5077.png)

#### Bagaimana cara melihat zona ketersediaan sumber dan replika instans?
Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail instans, tempat Anda dapat melihat zona ketersediaan sumber dan replika di bagian **Availability Info** (Info Ketersediaan).
![](https://main.qcloudimg.com/raw/f022ef04a1db5bf566cc626990e534f5.png)

