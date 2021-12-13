Tencent Cloud menyediakan dua lingkungan jaringan: [Virtual Private Cloud](https://intl.cloud.tencent.com/product/vpc) (VPC) dan jaringan dasar.
Setelah 13 Juni 2017, akun yang baru didaftarkan tidak lagi mendukung jaringan dasar. Kami merekomendasikan Anda untuk menggunakan VPC dengan alasan berikut:
- Fitur lengkap: VPC mencakup semua fitur jaringan dasar, sekaligus menyediakan layanan jaringan yang lebih fleksibel seperti rentang IP kustom, perutean, Direct Connect, VPN, NAT, dll.
- Migrasi lancar: Tidak ada solusi migrasi yang sepenuhnya lancar di industri ini (kebutuhan untuk menonaktifkan, mengubah IP pribadi, dll). Jika nanti Anda perlu menggunakan VPC untuk pengembangan bisnis, proses migrasi dapat memengaruhi bisnis Anda.

## Jaringan dasar dan VPC

### VPC

Dengan [Virtual Private Cloud (VPC)] Tencent Cloud (https://intl.cloud.tencent.com/document/product/215), Anda dapat menyesuaikan jaringan virtual terisolasi logis di cloud. Meskipun di wilayah yang sama, VPC yang berbeda tidak dapat berkomunikasi satu sama lain secara default. Mirip dengan jaringan tradisional yang dijalankan di pusat data Anda, sumber daya Tencent Cloud Anda, termasuk [CVM](https://intl.cloud.tencent.com/document/product/213/495), [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214/524), dan [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/5147), dihosting di VPC Tencent Cloud untuk memberi Anda kontrol penuh atas lingkungan. Untuk mengetahui informasi selengkapnya tentang skenario aplikasi dan konfigurasi, lihat [VPC](https://intl.cloud.tencent.com/document/product/215/535). VPC membantu Anda membangun arsitektur jaringan yang lebih kompleks dan cocok untuk pengguna yang terbiasa menggunakan manajemen jaringan.

![](https://main.qcloudimg.com/raw/b86b2e3af8e21354d317bb2b4739b47d.jpg)

### Jaringan dasar

Jaringan dasar adalah kumpulan sumber daya jaringan publik untuk semua pengguna Tencent Cloud. Semua sumber daya Tencent Cloud Anda akan dikelola secara terpusat oleh Tencent Cloud.

### Perbedaan fitur

| **Fitur**| **Jaringan Dasar**| **VPC** |
|---------|---------|---------|
| Asosiasi penyewa | Asosiasi penyewa | Jaringan terisolasi logis didasarkan pada enkapsulasi GRE |
| Penyesuaian jaringan | Tidak Didukung | Didukung |
| Penyesuaian perutean | Tidak Didukung | Didukung |
| IP Kustom | Tidak Didukung | Didukung |
| Aturan interkoneksi | Interkoneksi diizinkan untuk penyewa yang sama di wilayah yang sama | Interkoneksi lintas wilayah dan lintas akun didukung |
| Kontrol keamanan　| [Grup keamanan](https://intl.cloud.tencent.com/document/product/213/12452)| [Grup keamanan](https://intl.cloud.tencent.com/document/product/213/12452) dan [ACL Jaringan](https://intl.cloud.tencent.com/document/product/215/5132) |

## Membagikan dan mengakses sumber daya antara jaringan dasar dan VPC

Beberapa sumber daya dan fitur Tencent Cloud mendukung jaringan dasar dan VPC, dan dapat dibagikan atau diakses melalui dua jaringan yang berbeda.

|**Sumber Daya**|**Deskripsi**|
|--|--|
|[Citra](https://intl.cloud.tencent.com/document/product/213/4940)|Citra dapat digunakan untuk meluncurkan instans CVM di lingkungan jaringan apa pun|
|[IP Publik Elastis](https://intl.cloud.tencent.com/document/product/213/5733)|IP Publik Elastis dapat terhubung ke instans CVM pada lingkungan jaringan apa pun|
|Instans|Instans di jaringan dasar dan VPC dapat berkomunikasi satu sama lain melalui [IP Publik](https://intl.cloud.tencent.com/document/product/213/5224) atau [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807)|
|[Kunci SSH](https://intl.cloud.tencent.com/document/product/213/6092)|Kunci SSH mendukung pemuatan instans CVM di lingkungan jaringan apa pun|
|[Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/12452)|Grup keamanan mendukung pengikatan instans CVM pada lingkungan jaringan apa pun|

> [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) tidak dapat dibagi antara jaringan dasar dan VPC. Meskipun VPC dan jaringan dasar saling terhubung, Cloud Load Balancer tidak mendukung pengikatan instans di VPC dan jaringan dasar secara bersamaan.

## Memigrasikan instans di jaringan dasar ke VPC

Lihat [Beralih ke VPC](https://intl.cloud.tencent.com/document/product/213/20278) untuk memigrasikan instans dalam jaringan dasar ke VPC.
