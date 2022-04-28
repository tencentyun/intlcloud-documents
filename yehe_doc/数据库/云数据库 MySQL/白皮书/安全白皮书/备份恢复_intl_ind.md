### Cadangan
TencentDB for MySQL mendukung pencadangan otomatis dan manual untuk memastikan pemulihan data yang menjamin integritas dan keandalan data. Layanan ini menyediakan fitur pencadangan data dan pencadangan log secara default, dengan frekuensi pencadangan otomatis yang harus diatur lebih dari dua kali seminggu. Jika Anda memiliki kebutuhan pencadangan lain, Anda dapat memulai pencadangan manual melalui [konsol](https://console.cloud.tencent.com/cdb) atau API kapan saja.

Selain itu, Anda dapat secara fleksibel mengonfigurasi periode penyimpanan file cadangan sesuai kebutuhan, yaitu 7 hari secara default dan dapat hingga 1830 hari. File cadangan yang melebihi periode penyimpanan akan dihapus secara otomatis.

Untuk informasi selengkapnya tentang cara menggunakan fitur ini, harap lihat [Mencadangkan Database](https://intl.cloud.tencent.com/document/product/236/32340).

### Pemulihan
TencentDB for MySQL dapat memulihkan data. Anda dapat menggunakan fitur pengembalian untuk memulihkan data ke titik waktu mana pun dalam periode penyimpanan sesuai kebutuhan. Karena titik waktu yang tersedia untuk pemulihan data tunduk pada periode penyimpanan, Anda harus mengonfigurasi kebijakan penyimpanan cadangan yang wajar berdasarkan kebutuhan bisnis Anda untuk memastikan pemulihan data.

Untuk informasi selengkapnya tentang cara menggunakan fitur ini, harap lihat [Pengembalian Database](https://intl.cloud.tencent.com/document/product/236/7276).
