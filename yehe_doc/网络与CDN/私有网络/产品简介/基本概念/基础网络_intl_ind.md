Jaringan dasar adalah kumpulan sumber daya jaringan publik untuk semua pengguna Tencent Cloud. IP pribadi dari semua CVM ditetapkan oleh Tencent Cloud. Anda tidak dapat menyesuaikan rentang IP atau alamat IP. VPC dengan akses yang independen, dapat dikontrol, dan lebih aman dikembangkan dari jaringan klasik untuk memenuhi kebutuhan semakin banyaknya pengguna akan layanan yang lebih kompleks.
>?Karena sumber daya jaringan klasik menjadi semakin langka dan tidak dapat diperluas, akun Tencent Cloud yang terdaftar setelah 13 Juni 2017 00:00:00  dapat membuat instans (termasuk CVM dan TencentDB) hanya di VPC, bukan di jaringan klasik.  Jika Anda perlu menggunakan layanan jaringan klasik, kirimkan permohonan.


## Batasan Penggunaan
+ CVM berbasis jaringan klasik tidak mendukung ENI.
+ Migrasi dari jaringan klasik ke VPC tidak dapat dikembalikan.

## Jaringan Klasik vs. VPC
Baik jaringan klasik maupun VPC adalah ruang jaringan di cloud.  
+ Jaringan klasik adalah kumpulan sumber informasi jaringan publik untuk semua pengguna Tencent Cloud (seperti yang ditampilkan di sisi kanan gambar di bawah). IP pribadi dari semua CVM ditetapkan oleh Tencent Cloud. Anda tidak dapat menyesuaikan rentang IP atau alamat IP.
+ Sebaliknya, VPC adalah ruang jaringan yang terisolasi secara logis di Tencent Cloud (seperti yang ditampilkan di sisi kiri gambar di bawah). Di VPC, Anda dapat menyesuaikan rentang IP, alamat IP, dan kebijakan perutean. VPC lebih cocok untuk kasus penggunaan yang memerlukan konfigurasi kustom.
![](https://main.qcloudimg.com/raw/5fe7730ac2f302d960cf20443f976b6f.png)

>?Anda dapat menggunakan [`DescribeAccountAttributes`](https://intl.cloud.tencent.com/document/product/215/17875) API untuk mengkueri atribut jaringan sebuah akun.  Jika nilai `supportedPlatforms` adalah `only-vpc`, akun tersebut adalah pengguna VPC default, yang memiliki semua sumber daya cloud di bawah VPC. Jika nilai `supportedPlatforms` adalah `classic`, akun tersebut adalah pengguna jaringan klasik default, yang memiliki semua sumber daya cloud di bawah jaringan klasik.

## Referensi
+ Untuk informasi selengkapnya tentang rencana komunikasi antara VPC dan jaringan klasik, lihat [Berkomunikasi dengan Jaringan Klasik](https://intl.cloud.tencent.com/document/product/215/35505).
+ Untuk informasi selengkapnya tentang konfigurasi Classiclink, lihat [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807).
+ Anda dapat memigrasikan instans Anda dari jaringan klasik ke VPC untuk memfasilitasi penggunaan VPC Anda. Untuk petunjuk mendetail, lihat [Beralih dari Jaringan Klasik ke VPC](https://intl.cloud.tencent.com/document/product/215/41414).

