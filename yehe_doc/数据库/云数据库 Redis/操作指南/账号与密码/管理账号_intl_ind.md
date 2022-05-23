## Skenario Operasi
TencentDB for Redis menyediakan kontrol izin baca/tulis dan kontrol kebijakan perutean melalui mekanisme akun, yang membantu memenuhi kebutuhan manajemen izin bisnis dalam skenario yang kompleks. Saat ini, hanya Edisi Memori TencentDB for Redis (tidak termasuk v2.8) yang mendukung pengaturan akun.
- **Kategori akun**
  - Akun default: akun dengan kata sandi saja.
  - Akun kustom: akun dengan nama akun. Metode autentikasi akun kustom adalah `account name@password`, yang digunakan sebagai parameter kata sandi untuk mengakses Redis, seperti `redis-cli -h 1.1.1.1 -p 6379 -a readonlyuser@password`.
- **Prioritas kecocokan akun**
  - Jika ada akun default dengan pemisah @, akan dicocokkan terlebih dahulu sebelum akun kustom. Akun kustom akan dicocokkan dengan simbol @ pertama sebagai pemisah.
  - TencentDB for Redis menggunakan metode autentikasi bebas kata sandi yang berbeda dari Edisi Komunitas Redis. Secara khusus, setelah akses bebas kata sandi diaktifkan untuk sebuah instans, jika kata sandi dalam parameter akses tidak kosong, autentikasi akan gagal di yang sebelumnya tetapi akan berhasil di yang terakhir.
- **Pengaturan izin**
  - Izin baca saja: akun memiliki izin untuk membaca tetapi tidak mengubah data.
  - Izin baca/tulis: akun memiliki izin untuk membaca dan menulis data.
- **Kebijakan perutean baca saja**
  - Dengan mengonfigurasi kebijakan perutean baca saja, Anda dapat mendistribusikan **permintaan baca** dari akun yang ditentukan ke node (master atau replika) yang ditentukan.
  - Jika **replika baca saja** tidak diaktifkan untuk sebuah instans, instans tersebut tidak akan mendukung perutean ke node replika. Fitur ini dapat diaktifkan di halaman **Kelola Node**.
  - Jika sebuah instans memiliki akun yang mengakses node replika, fitur **replika baca saja** tidak dapat dinonaktifkan. Untuk menonaktifkannya, Anda harus menghapus akun terlebih dahulu.
  
## Petunjuk
1. Login ke [Konsol Redis](https://console.cloud.tencent.com/redis) dan klik ID instans di daftar instans untuk masuk ke halaman manajemen instans.
2. Pilih tab **Manage Account** (Kelola Akun) untuk membuat akun, mengubah izin, mengatur ulang kata sandi, dan menghapus akun.
![](https://main.qcloudimg.com/raw/276fb5f3092f46c57d675b19d1a14962.png)
