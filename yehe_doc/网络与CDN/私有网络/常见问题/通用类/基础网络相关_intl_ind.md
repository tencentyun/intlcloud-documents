### Apa perbedaan antara jaringan klasik dan VPC?
VPC adalah ruang jaringan virtual yang terisolasi secara logis di Tencent Cloud.
- VPC menyediakan lebih banyak fitur daripada jaringan klasik. Untuk informasi tentang cara mengoperasikan Classiclink, lihat [Mengelola Jaringan Klasik](https://intl.cloud.tencent.com/document/product/215/31807).

### Dapatkah saya mengalihkan CVM dari jaringan klasik ke VPC? 
Ya. Tencent Cloud memungkinkan Anda memigrasikan satu atau beberapa instans CVM dari jaringan klasik ke VPC sekaligus. Untuk langkah dan petunjuk selengkapnya, lihat [Beralih ke VPC](https://intl.cloud.tencent.com/document/product/213/20278).
>!Operasi ini tidak dapat dibatalkan. Pastikan Anda membaca dokumen dengan cermat sebelum melakukan operasi ini.

### Dapatkah saya mengalihkan CVM dari VPC ke jaringan klasik?
Tidak. VPC mendukung lebih banyak fitur dengan fleksibilitas yang lebih besar, oleh karena itu kami menyarankan Anda untuk memigrasikan CVM dari jaringan klasik ke VPC.

### Bagaimana cara membangun komunikasi antara CVM jaringan klasik dan CVM berbasis VPC?
Anda dapat menggunakan [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807) untuk menjalin komunikasi antara jaringan klasik dan VPC.
Penggunaan Classiclink tunduk pada batasan berikut:
1. Jaringan klasik dan VPC yang akan dikomunikasikan terletak di wilayah yang sama (dapat berada di zona ketersediaan yang berbeda, seperti Zona 1 Guangzhou dan Zona 2 Guangzhou).
2. Rentang alamat IP VPC (CIDR) harus 10.0.0.0/16 - 10.0.47.0/16 (termasuk subset). Jika tidak, akan ada konflik.

Jika jaringan klasik dan VPC Anda memenuhi ketentuan ini, Anda dapat mengonfigurasi Classiclink pada halaman detail VPC di konsol, untuk mengaitkan VPC dengan CVM jaringan klasik untuk interkoneksi.

### Dapatkah sumber daya seperti penyeimbang beban cloud dan database di jaringan klasik berkomunikasi dengan VPC?
+ Koneksi terminal membantu membangun komunikasi antara instans di VPC dan instans lain di jaringan klasik melalui jaringan pribadi. Ini memetakan alamat IP instans jaringan klasik ke IP VPC, yang memungkinkan Anda mengakses instans jaringan klasik melalui IP VPC. Produk jaringan klasik termasuk CLB klasik, TencentDB, CMEM, REDIS, dan MongoDB dapat berkomunikasi dengan VPC dengan cara ini. Komunikasi lintas wilayah atau lintas akun tidak didukung.
- Arah: Satu arah (VPC mengakses jaringan klasik).
- Jika diperlukan, [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk menerapkan.

### Dapatkah jaringan klasik dan instans VPC di bawah akun yang berbeda saling berkomunikasi?
Tidak. VPC mendukung lebih banyak fitur dengan fleksibilitas yang lebih besar, oleh karena itu kami sarankan Anda untuk memigrasikan sumber daya dari jaringan klasik ke VPC.

### Bagaimana cara membatalkan pengaitan CVM dari VPC atau jaringan klasik?
Lakukan langkah-langkah berikut untuk membatalkan pengaitan CVM.
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/vpc).
2. Klik ID VPC yang saling terhubung dengan jaringan klasik untuk masuk ke halaman detail VPC.
3. Klik **Classiclink** (Classiclink). Dalam daftar CVM jaringan klasik, pilih CVM yang akan dibatalkan pengaitannya dan klik **Disassociate** (Batalkan Pengaitan).
4. Klik **OK** (Oke).

Untuk petunjuk langkah demi langkah, lihat bagian “Membatalkan pengaitan VPC dan CVM Jaringan Klasik” di [Mengelola Jaringan Klasik](https://intl.cloud.tencent.com/document/product/215/31807).
