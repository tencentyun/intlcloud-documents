## IP Publik

### Bagaimana cara CVM tanpa IP publik dapat mengakses jaringan publik?
Jika Anda tidak membeli IP publik saat membeli CVM atau telah menampilkan PI publik, Anda dapat mengajukan EIP di [Konsol EIP](https://console.cloud.tencent.com/cvm/eip) dan mengikatnya ke CVM Anda guna mengizinkan akses jaringan publik.

### Apakah saya bisa mengubah IP publik saya?

Anda bisa mengubah IP publik CVM. Untuk informasi selengkapnya tentang operasi tertentu, lihat [Mengubah IP Publik Instans](https://intl.cloud.tencent.com/document/product/213/16642).

### Bagaimana cara menjaga agar IP publik tidak berubah?

Jika perlu mempertahankan IP publik tertentu pada akun Anda, Anda bisa mengubahnya menjadi EIP, yang bisa diikat ke perangkat dan digunakan untuk mengakses jaringan publik. EIP ini akan dipertahankan pada akun Anda sampai Anda **release** (melepaskannya).
Untuk informasi selengkapnya tentang operasi terkait, lihat [EIP](https://intl.cloud.tencent.com/document/product/213/16586).

### Apa yang dimaksud dengan alamat IP publik?
Alamat IP publik adalah alamat IP tanpa syarat yang ada di Internet. CVM dengan alamat IP publik dapat diakses untuk dan oleh komputer lain di Internet.
Untuk informasi selengkapnya, lihat [Akses Internet](https://intl.cloud.tencent.com/document/product/213/5224).

### Bagaimana cara mendapatkan alamat IP publik dari sebuah instans?
Untuk mengetahui detailnya, lihat [Mendapatkan Alamat IP Publik](https://intl.cloud.tencent.com/document/product/213/17940).

### Bagaimana cara mengubah alamat IP publik sebuah instans?
Untuk mengetahui detailnya, lihat [Mengubah IP Publik Instans](https://intl.cloud.tencent.com/document/product/213/16642).

### Apa perbedaan antara gateway publik dan CVM dengan alamat IP publik?
Gateway publik mengaktifkan fitur penerusan lalu lintas jaringan publik dalam citra. Namun, CVM dengan alamat IP publik tidak memiliki fitur ini secara default. Oleh karena itu, CVM yang dibuat di citra publik Windows tidak dapat berfungsi sebagai gateway publik karena citra Windows tidak memiliki fitur penerusan lalu lintas.

### Mengapa saya tidak dapat mengubah IP publik CVM saya?
Kemungkinan alasannya meliputi:
- Instans CVM dimatikan dan tidak dikenakan biaya saat dimatikan.
- IP publik CVM telah diubah.


### Bagaimana cara mendapatkan alamat IP publik dari instans yang tidak memiliki IP publik (IPv4) yang ditetapkan selama pembuatan instans?
- Anda dapat memperoleh IP publik dari sebuah instans dengan menerapkan dan mengikat EIP ke instans tersebut. Untuk operasi langkah demi langkah, lihat [EIP](https://intl.cloud.tencent.com/document/product/213/16586).

## IP Pribadi

### Apa yang dimaksud dengan alamat IP pribadi?
Alamat IP pribadi yang tidak dapat diakses melalui Internet. Begitulah cara Tencent Cloud menyediakan layanan jaringan pribadi.
Untuk informasi selengkapnya, lihat [Akses Jaringan Pribadi](https://intl.cloud.tencent.com/document/product/213/5225).

### Bagaimana cara mendapatkan alamat IP pribadi dari sebuah instans?
Untuk detailnya, lihat [Mendapatkan Alamat IP Pribadi dan Mengatur DNS](https://intl.cloud.tencent.com/document/product/213/17941).

### Apakah saya bisa mengubah alamat IP pribadi pada instans selain alamat IP publiknya?
Ya, Anda bisa mengubah IP pribadi pada instans. Untuk mengetahui operasinya, lihat [Memodifikasi Alamat IP Pribadi](https://intl.cloud.tencent.com/document/product/213/16561)

