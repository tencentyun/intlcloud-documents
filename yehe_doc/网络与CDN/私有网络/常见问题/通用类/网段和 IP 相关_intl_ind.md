### Berapa batasan rentang IP VPC dan subnet?
Blok CIDR Tencent Cloud VPC mendukung penggunaan salah satu dari rentang IP pribadi berikut:
- `10.0.0.0` - `10.255.255.255` (rentang mask antara 12 hingga 28)
- `172.16.0.0` - `172.31.255.255` (rentang mask antara 12 hingga 28)
- `192.168.0.0` - `192.168.255.255` (rentang mask antara 16 hingga 28)

- Blok CIDR subnet harus berada di dalam atau sama dengan blok CIDR VPC.

### Dapatkah rentang IP VPC dan subnet diubah?
- Saat membuat VPC dan subnet, Anda perlu menentukan blok CIDR-nya, dan blok tersebut tidak dapat diubah setelah dibuat.
- Jika Anda tidak dapat membuat koneksi peering karena tumpang tindihnya rentang IP VPC, Anda dapat mencoba [Cloud Connect Network](https://intl.cloud.tencent.com/product/ccn), yang memiliki detail batas yang lebih kecil (hanya rentang IP subnet yang tidak dapat tumpang tindih) atau memigrasikan instans ke VPC lain. Untuk detailnya, lihat [Beralih dari Jaringan Klasik ke VPC](https://intl.cloud.tencent.com/document/product/213/20278).

### Apa yang harus dilakukan ketika koneksi peering gagal dibuat karena konflik rentang IP VPC?
Saat membuat koneksi peering, blok CIDR dari dua VPC tidak boleh tumpang tindih, atau akan menyebabkan koneksi peering gagal dibuat.
- Jika rentang IP subnet dari dua VPC yang perlu berkomunikasi tidak tumpang tindih, maka Anda dapat menggunakan [CCN](https://intl.cloud.tencent.com/product/ccn) untuk membangun komunikasi. CCN menurunkan batas rentang IP ke tingkat subnet saat VPC berkomunikasi.
Misalnya, jika rentang IP dari dua VPC yang perlu saling berkomunikasi adalah `10.0.0.0/16`, tetapi subnetnya masing-masing adalah `10.0.1.0/24` dan `10.0.2.0/24`, maka Anda dapat membangun komunikasi menggunakan CCN. Lihat [Dokumentasi Produk CCN](https://intl.cloud.tencent.com/document/product/1003).
- Jika kebutuhan Anda tidak terpenuhi dengan menggunakan CCN, maka Anda perlu memigrasikan sumber daya di dalam subnet yang tumpang tindih tersebut.
    Untuk detail tentang mengubah subnet CVM, lihat [Mengubah Subnet Instans](http://intl.cloud.tencent.com/document/product/213/16565).
    - Migrasikan instans dalam VPC seperti yang diinstruksikan di [Beralih ke VPC](https://intl.cloud.tencent.com/document/product/213/20278).

### Dapatkah saya mengubah IP pribadi sumber daya di VPC (CVM dan database)?
- Anda dapat mengubah IP pribadi utama dari ENI utama CVM, tetapi IP pribadi utama ENI sekunder tidak dapat diubah. Untuk detailnya, lihat [Memodifikasi Alamat IP Pribadi](https://intl.cloud.tencent.com/document/product/213/16561).
- Anda dapat memodifikasi IP pribadi instans TencentDB (seperti instans MySQL). Lihat [Menyesuaikan IP dan Port](https://intl.cloud.tencent.com/document/product/236/31915).
- IP pribadi CLB tidak dapat diubah.

### Dapatkah saya memigrasikan CVM atau database dari satu VPC ke VPC lainnya?
- Untuk saat ini, Anda dapat memigrasikan instans CVM dan instans TencentDB for MySQL ke VPC lain di bawah akun yang sama. Instans TencentDB lainnya tidak didukung.
Lihat [Beralih ke VPC](https://intl.cloud.tencent.com/document/product/213/20278) untuk memigrasikan instans dalam jaringan dasar ke VPC.
- Untuk memigrasikan TencentDB untuk instans MySQL, lihat [Beralih Jaringan](https://intl.cloud.tencent.com/document/product/236/31915).

### Apa yang dilakukan oleh EIP?
ElP berlaku untuk skenario berikut:
1. **Disaster recovery** (Pemulihan bencana)
Kami sangat menyarankan Anda menggunakan EIP untuk pemulihan bencana. Ketika salah satu CVM Anda gagal menyediakan layanan secara normal, Anda dapat melepaskan ikatan EIP dari CVM ini dan mengikatnya kembali ke CVM yang sehat untuk melanjutkan layanan dengan cepat.
2. **Retaining a specific public IP** (Mempertahankan IP publik tertentu)
Jika perlu mempertahankan IP publik tertentu pada akun Anda, Anda bisa mengubahnya menjadi EIP, yang selanjutnya bisa digunakan untuk mengakses jaringan publik setelah diikat dengan perangkat. EIP ini akan dipertahankan pada akun Anda sampai Anda "melepasnya"
3. **Other special scenarios** (Skenario khusus lainnya)
Saat Anda perlu mengubah IP dalam kasus khusus lainnya, Anda dapat mengonversi IP publik biasa menjadi EIP, kemudian mengikat/melepas ikatan EIP. Namun, dengan sumber daya EIP terbatas yang tersedia, kuota dikenakan pada jumlah EIP untuk setiap wilayah dalam satu akun. Oleh karena itu, perencanaan yang wajar dan penggunaan EIP sangat penting.

### Bagaimana cara menjaga agar IP publik tidak berubah?
Jika perlu mempertahankan IP publik tertentu pada akun Anda, Anda bisa mengubahnya menjadi EIP, yang selanjutnya bisa digunakan untuk mengakses jaringan publik setelah diikat dengan perangkat. EIP ini akan dipertahankan pada akun Anda sampai Anda "melepasnya"
Untuk petunjuk, lihat [Mengonversi UP publik umum ke EIP](https://intl.cloud.tencent.com/document/product/213/16586#convert-a-public-ip-to-an-eip).

### Apakah EIP bisa dikonversi kembali menjadi IP publik?
EIP tidak bisa dikonversi kembali ke IP publik.



