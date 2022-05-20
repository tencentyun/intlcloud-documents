
## Ikhtisar
TencentDB for Redis mendukung pencadangan dan pemulihan data. Layanan backend dapat secara otomatis mencadangkan data instans secara teratur pada titik waktu yang dikonfigurasi di konsol. Pencadangan manual juga dapat dilakukan kapan saja. Data cadangan disimpan dalam format RDB yang sesuai dengan Redis Engine Edition dan disimpan dalam COS untuk keandalan data yang tinggi. TencentDB for Redis mendukung pemulihan data instans melalui pengembalian dan kloning, yang mengimplementasikan pemulihan dan kloning data dalam skenario tertentu.

## Data Cadangan
TencentDB for Redis mendukung pencadangan otomatis dan manual. Untuk pencadangan otomatis, periode waktu pencadangan dapat disesuaikan.

### Pencadangan Otomatis
Layanan backend TencentDB mencadangkan data instans secara berkala. Siklus pencadangan dapat dilihat dan dikonfigurasi di **Backup and Restore** (Pencadangan dan Pemulihan) > **Auto Backup** (Pencadangan Otomatis) di konsol.
Secara default, pencadangan data lengkap akan dilakukan setiap hari antara pukul 02.00 dan 08.00, di mana file cadangan disimpan di COS. Anda dapat melihat file cadangan harian di **Backup and Restore** (Pencadangan dan Pemulihan) di Konsol TencentDB for Redis.
Daftar cadangan menampilkan semua file cadangan dan informasinya tentang instans. TencentDB for Redis menyediakan dua alamat unduhan cadangan. Alamat unduhan jaringan publik memungkinkan Anda untuk mengunduh data cadangan di mana pun Anda dapat mengakses internet. Alamat unduhan jaringan pribadi memungkinkan untuk Anda melakukan pengunduhan melalui jaringan pribadi Tencent Cloud, yang tidak mendukung unduhan lintas wilayah, sehingga Anda hanya dapat mengunduh data di wilayah tempat instans Redis Anda berada.

### Pencadangan Manual
Selain pencadangan otomatis yang dilakukan oleh backend sistem secara teratur, Anda dapat mencadangkan instans secara manual di Konsol TencentDB for Redis untuk memenuhi beragam kebutuhan Anda. File cadangan manual juga ditampilkan dalam daftar cadangan di konsol, yang dapat dibedakan dari file cadangan otomatis dengan jenis cadangan **Manual Backup** (Pencadangan Manual) dalam daftar.

## Pemulihan Data
TencentDB for Redis mendukung pemulihan data berdasarkan file cadangan. Ada dua cara untuk melakukannya: memulihkan ke instans asli atau memulihkan ke instan baru melalui kloning.

## Memulihkan Instans
TencentDB for Redis Edisi Standar (Komunitas) mendukung pemulihan instans, yang menghapus data yang ada pada instans dan memulihkan data cadangan yang ditentukan ke dalamnya. Instans tidak dapat diakses selama pemulihan. Anda dapat memilih file cadangan yang ingin dipulihkan dalam daftar cadangan pada tab **Backup and Restore** (Pencadangan dan Pemulihan) di Konsol TencentDB for Redis.

### Mengkloning Instans
TencentDB for Redis Edisi Klaster (Komunitas) mendukung kloning instans, yaitu membuat instans lengkap berdasarkan file cadangan. Data instans sama dengan yang ada di file cadangan. Anda dapat menggunakan fitur kloning untuk menganalisis data sebelumnya. Anda juga dapat mengembalikan instans dengan menukar IP instans baru dan instans asli.


