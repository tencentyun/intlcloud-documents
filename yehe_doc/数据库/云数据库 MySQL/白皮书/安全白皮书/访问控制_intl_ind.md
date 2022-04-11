TencentDB for MySQL mengimplementasikan kontrol akses melalui manajemen akun database, manajemen akses, grup keamanan, dan cara lain untuk memastikan keamanan data MySQL.

### Manajemen Akun Database
Anda dapat [membuat akun database](https://intl.cloud.tencent.com/document/product/236/31900) di Konsol TencentDB for MySQL atau melalui API. Anda juga dapat memberikan izin manajemen pada tingkat yang berbeda untuk akun tersebut. Sebaiknya berikan izin pada akun berdasarkan prinsip hak istimewa paling rendah untuk memastikan keamanan data.

### Cloud Access Management
[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) adalah layanan Tencent Cloud berbasis web yang membantu Anda mengelola dan mengontrol izin akses ke sumber daya Tencent Cloud dengan aman. Menggunakan CAM, Anda dapat membuat, mengelola, dan menghentikan pengguna (grup), dan mengontrol sumber daya Tencent Cloud yang dapat digunakan oleh pengguna tertentu melalui pengelolaan identitas dan kebijakan.

### Grup Keamanan
[Grup keamanan](https://intl.cloud.tencent.com/document/product/236/14470) terutama membantu Anda mengimplementasikan kontrol akses jaringan untuk instans TencentDB for MySQL Anda. Grup keamanan adalah firewall virtual stateful yang mampu memfilter. Sebagai sarana penting untuk isolasi keamanan jaringan yang disediakan oleh Tencent Cloud, solusi ini dapat digunakan untuk mengatur kontrol akses jaringan untuk satu atau beberapa instans TencentDB.

Anda dapat menambahkan CVM, ENI, TencentDB, dan instans lainnya di wilayah yang sama dengan persyaratan isolasi keamanan jaringan yang sama ke grup keamanan yang sama. Instans dalam grup keamanan dicocokkan berdasarkan aturan. Memodifikasi aturan grup keamanan tidak memerlukan restart instans TencentDB for MySQL, dan perubahan akan segera berlaku.


