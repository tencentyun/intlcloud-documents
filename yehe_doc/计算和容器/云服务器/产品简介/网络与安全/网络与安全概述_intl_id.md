Tencent Cloud menawarkan infrastruktur jaringan dan layanan keamanan untuk memastikan bisnis Anda tetap aman, efisien, dan fleksibel.

## Login Terenkripsi
Tencent Cloud menyediakan dua metode login terenkripsi menggunakan [Kata Sandi Login](https://intl.cloud.tencent.com/document/product/213/6093) dan [Kunci SSH](https://intl.cloud.tencent.com/document/product/213/6092). Anda dapat menggunakan salah satu dari metode ini untuk terhubung ke instans CVM Anda. CVM Windows tidak mendukung login menggunakan kunci SSH.

## Akses jaringan
Produk Tencent Cloud dapat berkomunikasi satu sama lain menggunakan [Akses Internet](https://intl.cloud.tencent.com/document/product/213/5224) atau [Akses Jaringan Pribadi](https://intl.cloud.tencent.com/document/product/213/5225).
 - Akses internet: Instans CMV dan produk Tencent Cloud lainnya menggunakan akses Internet untuk menyediakan layanan yang dapat diakses publik. Layanan tersebut mendapatkan alamat IP publik untuk berkomunikasi dengan komputer lain di Internet.
 - Akses Jaringan Pribadi: Tencent Cloud menetapkan alamat IP pribadi ke sumber daya di wilayah yang sama sehingga dapat berkomunikasi satu sama lain di LAN yang sama secara gratis. 

## Lingkungan Jaringan
Tencent Cloud menyediakan dua jenis [Lingkungan Jaringan](https://intl.cloud.tencent.com/document/product/213/5227): jaringan dasar dan jaringan pribadi (VPC).
 - Jaringan dasar adalah kumpulan sumber daya jaringan bersama untuk semua pengguna. Kami merekomendasikan jaringan dasar untuk pemula.
 - VPC adalah ruang jaringan kustom yang terisolasi secara logis. Anda dapat meluncurkan instans CVM pada rentang IP yang telah ditentukan dan disesuaikan untuk mengisolasi sumber daya Anda dari pengguna lain. Kami merekomendasikan VPC bagi pengguna yang terbiasa menggunakan administrasi jaringan.

## Grup Keamanan
[Grup keamanan](https://intl.cloud.tencent.com/document/product/213/12452) adalah firewall virtual stateful yang mampu memfilter. Sebagai sarana penting untuk isolasi keamanan jaringan yang disediakan oleh Tencent Cloud, solusi ini dapat digunakan untuk mengatur kontrol akses jaringan untuk satu atau beberapa instans TencentDB.
Berikut adalah daftar kasus penggunaan grup keamanan umum:
 - Buat beberapa grup keamanan dan isi dengan aturan yang berbeda.
 - Kaitkan satu atau beberapa grup keamanan dengan setiap instans CVM Anda. Sistem menggunakan grup keamanan ini untuk mengontrol lalu lintas ke instans Anda dan sumber daya yang dapat diakses oleh instans Anda.
 - Konfigurasikan grup keamanan Anda sehingga hanya alamat IP atau grup keamanan tertentu yang dapat mengakses instans Anda.

## Elastic Public IP
[Elastic Public IP](https://intl.cloud.tencent.com/document/product/213/5733), atau EIP, adalah alamat IP statis yang didesain khusus untuk komputasi cloud.
Kami merekomendasikan penggunaan EIP dalam kasus berikut:
 - Instans dapat tidak berfungsi karena alasan yang tidak terduga, dan instans pengalihan perlu menggunakan alamat IP yang sama untuk menyediakan layanan tanpa gangguan. 
 - Instans tidak memiliki alamat IP publik tetapi masih memerlukan alamat IP statis.

## ENI
[Elastic Network Interface (ENI)](https://intl.cloud.tencent.com/document/product/213/6514) adalah antarmuka jaringan elastis yang dapat terhubung ke instans CVM pada VPC untuk menyediakan koneksi jaringan. ENI dapat dimigrasikan secara bebas di antara instans. Tindakan ini penting saat mengonfigurasi dan mengelola jaringan serta menerapkan deployment dengan ketersediaan tinggi.
