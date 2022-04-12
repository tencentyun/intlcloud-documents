### Apa itu Classiclink?
Classiclink digunakan untuk mengaitkan CVM di jaringan klasik ke VPC tertentu, yang memungkinkan CVM berkomunikasi dengan layanan Tencent Cloud, termasuk CVM dan database di VPC. Untuk informasi selengkapnya, lihat [Mengelola Jaringan Klasik](https://intl.cloud.tencent.com/document/product/215/31807).

### Bagaimana cara membangun komunikasi antara CVM di jaringan klasik dan CVM di VPC?
Anda dapat menggunakan [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807) untuk membangun komunikasi antara jaringan klasik dan VPC.
Saat menggunakan Classiclink, perhatikan batasan berikut:
1. Jaringan klasik dan VPC yang perlu saling berkomunikasi harus berada di wilayah yang sama (tetapi dapat berada di zona ketersediaan yang berbeda, seperti Zona 1 Guangzhou dan Zona 2 Guangzhou).
2. CIDR (rentang IP) VPC harus `10.0.0.0/16 - 10.47.0.0/16` (termasuk subset), jika tidak, konflik akan terjadi.

Jika jaringan klasik dan VPC Anda memenuhi ketentuan ini, Anda dapat mengonfigurasi tab **Classiclink** (Classiclink) pada halaman detail VPC di Konsol untuk mengaitkan VPC dengan CVM di jaringan klasik untuk interkoneksi.

### Dapatkah sumber daya, termasuk penyeimbang beban awan dan database di jaringan klasik, berkomunikasi dengan VPC?
- Koneksi terminal membantu membangun komunikasi antara instans di VPC dan instans lain di jaringan klasik melalui jaringan pribadi. Prinsipnya adalah memetakan alamat IP instans di jaringan klasik ke alamat IP VPC, sehingga Anda dapat mengakses instans jaringan klasik dengan mengakses alamat IP VPC yang sesuai. Layanan yang mendukung jaringan klasik termasuk CLB klasik, TencentDB, CMEM, REDIS, MongoDB. Namun, komunikasi lintas wilayah atau lintas akun tidak didukung.
- Arah: satu arah (VPC mengakses jaringan klasik).
- Jika Anda memerlukan petunjuk selengkapnya, [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk menerapkan.

### Apakah instans jaringan dan VPC klasik yang berada di akun yang berbeda dapat saling berkomunikasi?
Tidak. Saat ini, sumber daya (CVM dan database) di jaringan klasik dan instans VPC di bawah akun yang berbeda tidak dapat saling berkomunikasi. VPC mendukung lebih banyak fitur dengan fleksibilitas yang lebih besar, jadi sebaiknya Anda memigrasi dari jaringan klasik ke VPC.
