TencentDB for Redis menyediakan fitur auto-failback untuk instans yang di-deploy di seluruh AZ. Setelah fitur diaktifkan, jika node master dialihkan dari AZ master atau grup node master (arsitektur klaster) ke AZ atau grup lain setelah failover terjadi, node tersebut akan secara otomatis dialihkan kembali, sehingga menyederhanakan operasi OPS berikutnya. Anda dapat mengaktifkan atau menonaktifkan fitur ini dengan mengatur parameter database.

## AZ Master

Anda dapat men-deploy node instans TencentDB for Redis di AZ master dan replika. Auto-failback diaktifkan secara default. Jika node master dialihkan dari AZ master atau grup node master (arsitektur klaster) ke AZ atau grup lain setelah failover terjadi, node tersebut akan secara otomatis dialihkan kembali setelah semua node yang gagal diganti.

Anda dapat menentukan AZ master saat membuat instans. Atau, Anda dapat secara manual mempromosikan AZ replika menjadi master setelah instans dibuat (setelah node replika/grup node dipromosikan menjadi master, AZ-nya akan menjadi AZ master).

## Mengaktifkan/Menonaktifkan Auto-Failback

Anda dapat mengelola fitur auto-failback dengan parameter database. Fitur ini diaktifkan secara default. Mengaktifkan/menonaktifkan fitur ini tidak memengaruhi akses Anda ke Redis.

1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pada halaman **Parameter Settings** (Pengaturan Parameter), atur `auto-failback` ke `yes` atau `no` untuk mengaktifkan atau menonaktifkan fitur auto-failback.
   ![](https://main.qcloudimg.com/raw/254792ffab482fd3c092ea63b001a7c1.png)

