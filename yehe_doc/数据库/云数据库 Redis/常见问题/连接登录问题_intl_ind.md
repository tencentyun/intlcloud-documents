### Bagaimana saya dapat terhubung ke instans TencentDB for Redis?
Anda dapat terhubung ke instans TencentDB for Redis menggunakan alat klien, pusat manajemen database (DMC), dan SDK yang mendukung berbagai bahasa pemrograman. Untuk informasi selengkapnya, lihat [Menghubungkan ke instans TencentDB for Redis (melalui Jaringan Pribadi)](https://intl.cloud.tencent.com/document/product/239/9897).

### Apa yang harus saya lakukan jika koneksi ke TencentDB for Redis gagal?
Penyebab umum kegagalan koneksi: masalah jaringan/grup keamanan, masalah kata sandi, dan masalah koneksi (misalnya jumlah koneksi maksimum telah tercapai). Untuk solusi terkait, lihat [Kegagalan Koneksi Instans Redis](https://cloud.tencent.com/document/product/239/58020).

### Bagaimana TencentDB for Redis dapat mendukung akses jaringan pribadi? Bagaimana cara melihat alamat jaringan pribadi instans saya?
Untuk mendukung akses jaringan pribadi, instans CVM dan TencentDB harus berada di bawah akun yang sama dan di VPC yang sama di wilayah yang sama, atau keduanya di jaringan klasik.

Untuk melihat alamat jaringan pribadi, login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), lihat alamat di daftar instans, atau klik ID instans dan lihat alamat di halaman detail instans yang ditampilkan.

### Dapatkah instans CVM saya terhubung ke TencentDB for Redis melalui jaringan pribadi?
1. Kondisi berikut harus dipenuhi untuk menggunakan koneksi jaringan pribadi:
Instans CVM dan TencentDB harus berada di bawah akun yang sama dan di VPC yang sama di wilayah yang sama, atau keduanya di jaringan klasik.
2. Anda dapat memeriksa apakah keduanya berada di VPC yang sama atau keduanya di jaringan klasik dengan cara berikut:
 - Anda dapat login ke [konsol CVM](https://console.cloud.tencent.com/cvm/instance), dan melihat informasi jaringan instans CVM di daftar instans atau di halaman detail instans.
 - Anda dapat login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), dan lihat informasi jaringan instans Redis di daftar instans atau di halaman detail instans.
 Untuk informasi lebih lanjut, lihat [Melihat jenis jaringan dan informasi VPC](https://cloud.tencent.com/document/product/239/58020#wllxvpdff).

### Apa yang harus saya lakukan jika instans CVM dan TencentDB for Redis saya berada di VPC yang berbeda?
Anda dapat terhubung ke instans melalui CCN.
Instans CVM dan TencentDB di VPC yang berbeda (dalam akun yang sama atau berbeda di wilayah yang sama atau berbeda) dapat saling terhubung melalui jaringan pribadi melalui [Cloud Connect Network](https://cloud.tencent.com/document/product/877).

### Instans CVM dan TencentDB untuk Redis saya berada di wilayah yang berbeda (masing-masing seperti Guangzhou dan Shanghai). Dapatkah saya menggunakan jaringan pribadi untuk koneksi?
Jika instans CVM dan Redis berada di [wilayah] yang berbeda(https://intl.cloud.tencent.com/document/product/239/4106), mereka berada di VPC yang berbeda, sehingga mereka tidak dapat saling terhubung langsung melalui jaringan pribadi. Sebaiknya Anda menggunakan [CCN](https://cloud.tencent.com/document/product/877)untuk menghubungkan VPC.

### Instans CVM dan TencentDB for Redis saya berada di AZ yang berbeda (masing-masing seperti Zona Shanghai 2 dan Zona Shanghai 1) di wilayah yang sama. Dapatkah saya menggunakan jaringan pribadi untuk koneksi?
Meskipun instans CVM dan TencentDB for Redis berada di wilayah yang sama, mereka mungkin berada di VPC yang berbeda.
- Jika mereka berada di AZ yang berbeda di VPC yang sama, mereka dapat saling terhubung melalui jaringan pribadi.
- Jika mereka berada di VPC yang berbeda (masing-masing seperti VPC 1 dan VPC 2), mereka tidak dapat saling terhubung melalui jaringan pribadi. Untuk solusi, lihat [Perubahan Jaringan Redis](https://intl.cloud.tencent.com/document/product/239/31944).

### Instans CVM dan TencentDB for Redis saya berada di AZ yang berbeda (masing-masing seperti Zona Shanghai 2 dan Zona Shanghai 1) di VPC yang sama. Dapatkah saya menggunakan jaringan pribadi untuk koneksi?
Ya. Instans di AZ yang berbeda tetapi dalam VPC yang sama saling terhubung melalui jaringan pribadi secara default.

### Instans CVM dan TencentDB for Redis saya berada di bawah akun yang berbeda. Dapatkah saya menggunakan jaringan pribadi untuk koneksi?
Tidak. Karena instans yang berada di bawah akun yang berbeda berada di VPC yang berbeda. Sebaiknya Anda menggunakan [CCN](https://cloud.tencent.com/document/product/877) untuk koneksi.

### Bagaimana cara mengaktifkan akses ke Redis melalui jaringan publik? 
Untuk informasi selengkapnya, lihat [Mengonfigurasi Alamat Jaringan Publik](https://cloud.tencent.com/document/product/239/63527).

