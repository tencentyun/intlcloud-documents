### Bagaimana cara menggunakan algoritma hash TencentDB for Redis Edisi Klaster?
Algoritme hash Redis Edisi Klaster sama dengan yang ada di klaster Redis Edisi Komunitas, misalnya, `HASH_SLOT = CRC16(key) mod 16384`. Untuk informasi selengkapnya, lihat [Spesifikasi Klaster Redis](https://redis.io/topics/cluster-spec).

### Berapa kapasitas maksimum satu instans?

| Edisi | Rentang Spesifikasi |
|--|--|
| Edisi Memori (Arsitektur Standar) | 0,25–64GB |
| Edisi Memori (Arsitektur Klaster) | 2GB–8TB |
| Edisi CKV (Arsitektur Standar) | 4–384 GB |
| Edisi CKV (Arsitektur Klaster) | 12GB–48TB |

### Apakah data yang disimpan di TencentDB for Redis dapat diandalkan?
Arsitektur Standar Redis (tanpa replika) tidak menyediakan ketersediaan tinggi. Edisi Redis lainnya mengadopsi struktur replikasi master/replika, di mana keandalan data dipastikan dengan pencadangan hot ditambah pencadangan cold data setiap hari.

### Metode persistensi mana yang digunakan TencentDB for Redis?
Pada backend TencentDB for Redis, klaster pencadangan melakukan pencadangan data penuh dan tambahan, dan persistensi dilakukan pada replika yang hampir tidak terlihat oleh bisnis online.

### Mengapa kapasitas penyimpanan sebesar 2 MB digunakan segera setelah instans dibeli?
Kapasitas penyimpanan tersebut digunakan oleh instans TencentDB for Redis untuk mempertahankan struktur datanya.

### Dapatkah TencentDB for Redis dikelola dengan alat visual seperti Redis Desktop Manager?
Anda dapat melakukan operasi manajemen dan OPS di konsol TencentDB for Redis. Jika Anda perlu menggunakan alat visual, gunakan instans CVM sebagai server lompat untuk memberikan alamat akses Redis Desktop Manager.

### Apakah bisnis saya akan terganggu selama penskalaan?
Pemutusan sementara selama penskalaan berbagai edisi TencentDB for Redis adalah seperti yang dijelaskan di bawah ini:
- Selama peningkatan skala, jika kapasitas yang diperluas melebihi kapasitas yang tersisa dari satu server, klaster akan melakukan sharding atau memigrasi node, dan pemutusan bisnis sesaat akan terjadi; jika tidak, tidak akan terjadi pemutusan.
- Selama penskalaan ke luar, jumlah node dalam klaster akan bertambah, dan pemutusan bisnis sesaat akan terjadi.
- Selama penskalaan ke dalam, pengambilalihan node akan menyebabkan migrasi node di klaster, dan pemutusan bisnis sesaat akan terjadi.
- Selama penurunan skala, tidak ada pemutusan bisnis sesaat yang akan terjadi.

### Bagaimana cara menambahkan alarm pemantauan?
Alarm dapat diimplementasikan melalui pemantauan dan alarm kustom. Untuk informasi selengkapnya, silakan lihat [Pemantauan dan Alarm](https://intl.cloud.tencent.com/document/product/239/34589).

### Apakah saya perlu membeli instans yang berbeda untuk memilih database 0-15?
Tidak. Beberapa database dapat diatur pada satu instans Arsitektur Standar atau Arsitektur Klaster.

### Apakah TencentDB for Redis mendukung Lua?
- Untuk instans Redis Edisi Memori (Arsitektur Standar) yang dibeli sebelum 1 September 2018, Lua tidak diaktifkan secara default. Anda dapat [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk aplikasi.
Lua diaktifkan secara default untuk instans yang dibeli setelah tanggal tersebut.
- Lua aktif secara default untuk instans Redis Edisi Memori (Arsitektur Klaster), Edisi CKV (Arsitektur Standar), dan Edisi CKV (Arsitektur Klaster).

### Apakah TencentDB for Redis mendukung caching acara langganan yang tidak valid?
Ya.

### Apa yang harus saya lakukan jika saya tidak sengaja menghapus akun atau lupa kata sandi?
- Jika Anda tidak sengaja menghapus akun, Anda dapat login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans untuk masuk ke halaman pengelolaan instans, dan pilih **Manage Account** (Kelola Akun) > **Create Account** (Buat Akun) untuk membuat akun baru.s
- Jika Anda lupa kata sandi akun default, Anda dapat mengatur ulang kata sandi tersebut dengan mencari akun yang sesuai di halaman **Manage Account** (Kelola Akun).

### Apa yang harus saya lakukan jika data pada node replika tidak sinkron dengan data pada node master di TencentDB for Redis?
Pembaruan node master TencentDB for Redis akan secara otomatis direplikasi ke node replika yang terkait. Karena mekanisme replikasi asinkron Redis, pembaruan node replika mungkin tertinggal dari pembaruan node master. Kemungkinan penyebabnya adalah sebagai berikut:
-Volume tulis I/O node master melebihi kecepatan sinkronisasi node replika.
- Ada penundaan jaringan antara node master dan node replika.

### Bagaimana cara memeriksa konektivitas port TencentDB for Redis?
Anda dapat menggunakan perintah `telnet` untuk memeriksa konektivitas port.

### Bagaimana cara menetapkan kebijakan caching di TencentDB for Redis?
Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans dalam daftar instans untuk masuk ke halaman konfigurasi parameter, dan konfigurasikan kebijakan caching melalui parameter `maxmemory-policy`, yang nilai defaultnya adalah `noeviction`.

### Bagaimana cara mengunduh klien untuk TencentDB for Redis?
Klien yang kompatibel dengan protokol Redis dapat mengakses TencentDB for Redis. Anda dapat memilih klien yang tepat sesuai kebutuhan. Untuk alamat unduhan, lihat [Klien](http://redis.io/clients?spm=a2c4g.11186623.2.5.c3a25c83nYgvqS).

### Bagaimana cara meningkatkan versi TencentDB for Redis?
Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis) dan klik ID instans di daftar instans untuk masuk ke halaman **Instance Details** (Detail Instans), di mana Anda dapat meningkatkan versi instans. Untuk informasi selengkapnya, lihat [Meningkatkan Versi Instans](https://intl.cloud.tencent.com/document/product/239/37710).

### Bagaimana cara meningkatkan arsitektur TencentDB for Redis?
Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis) dan klik ID instans di daftar instans untuk masuk ke halaman **Instance Details** (Detail Instans), di mana Anda dapat meningkatkan infrastruktur instans. Untuk informasi selengkapnya, lihat [Meningkatkan Versi Arsitektur](https://intl.cloud.tencent.com/document/product/239/37860).
