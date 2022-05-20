Untuk mengurangi latensi akses instans multi-AZ yang di-deploy, TencentDB for Redis memungkinkan Anda untuk membaca node lokal saja. Prinsinya adalah sebagai berikut:
- Aktifkan fitur "replika baca-saja". (Sebelum Anda mengaktifkan fitur tersebut, konfirmasikan bahwa penundaan data replika diperbolehkan.)
- Aktifkan fitur "Baca node lokal saja" dengan mengatur parameter database.
- Jika ada node proksi yang tersedia di AZ yang sama dengan klaster penyeimbang beban, klaster hanya dapat melihat dan mengakses node proksi tersebut.
- Node proksi dapat mengakses informasi AZ yang disimpan di node Redis dan merutekan permintaan baca ke node Redis di AZ yang sama.

## Mengaktifkan Fitur "Baca Node Lokal Saja"
Fitur "baca node lokal saja" dinonaktifkan secara default. Anda dapat mengaktifkan/menonaktifkan fitur ini untuk instans yang ada dengan mengatur parameter database pada halaman **Parameter Settings** (Pengaturan Parameter) di konsol. Anda dapat membuat templat parameter di mana parameter ditentukan dan menerapkan templat ketika membuat instans.

1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pada halaman **Parameter Settings** (Pengaturan Parameter), setel `read-local-node-only` ke `yes` atau `no` untuk mengaktifkan atau menonaktifkan fitur.
![](https://main.qcloudimg.com/raw/07556436ee1853d0ba0db190921a812d.png)

## Kebijakan Perutean Baca Saja
Untuk informasi selengkapnya, lihat [Kebijakan perutean baca-saja](https://intl.cloud.tencent.com/document/product/239/34590).

Saat fitur "replika baca saja" diaktifkan, kebijakan perutean baca-saja dapat digunakan untuk mengontrol apakah permintaan baca dirutekan ke node master. Namun, ketika fitur "baca node lokal saja" diaktifkan, prioritasnya lebih tinggi daripada kebijakan perutean baca saja: permintaan baca dirutekan ke node lokal terlebih dahulu, dan jika tidak ada node lokal yang tersedia, permintaan baca dirutekan ke node lain sesuai dengan kebijakan perutean baca saja. Berikut ini adalah contohnya:
1. Aktifkan fitur "replika baca saja" dan pilih kebijakan perutean baca saja (menurut kebijakan tersebut, permintaan baca tidak akan dirutekan ke node master).
2. Aktifkan fitur "Baca node lokal saja" (`read-local-node-only` = `yes`).
3. Hanya satu master node di AZ master.
4. Saat bisnis di AZ master mengakses node proksi di AZ master, proksi akan mengabaikan kebijakan perutean baca saja dan merutekan permintaan baca ke node master di AZ master untuk menghindari pembacaan di seluruh AZ.

