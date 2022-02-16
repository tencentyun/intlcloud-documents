### Biaya rendah
Layanan penyimpanan NoSQL key-table, yang menggunakan penyimpanan memori yang dilengkapi dengan penyimpanan disk, memberikan kemampuan untuk mengalihkan data dalam proses antara memori dan disk, dan kemampuan memperluas kapasitas secara dinamis di berbagai proses untuk memastikan bahwa data aktif disimpan dalam memori dan data tidak aktif pada disk. Layanan ini menghemat biaya sekitar 70% dibandingkan dengan penyimpanan hanya memori, dan sekitar 40% dibandingkan dengan Redis+MySQL.

### Performa Tinggi
Fitur termasuk pertukaran hot data dan cold data antara memori dan disk berdasarkan algoritme Least Recent Used (LRU), penyimpanan data pada disk SSD dan distribusi data multi-server memastikan performa tinggi hingga 100.000 QPS per server dengan latensi lebih sedikit dari 10 milidetik.

### Ketersediaan tinggi
Mekanisme hot backup master/slave yang memastikan pemulihan cepat jika terjadi kegagalan sistem.

### Dukungan untuk kebutuhan khusus game
Kebutuhan khusus game seperti model multi-server/multi-wilayah, pengaktifan server yang cepat, akses lintas wilayah, konsolidasi data lintas wilayah, kompresi data, dan lainnya terpenuhi, dan terus dioptimalkan sesuai dengan kebutuhan game.

### Perluasan dinamis
Ruang penyimpanan tidak dibatasi, dan kapasitasnya dapat diperluas atau dikurangi secara dinamis sesuai dengan kebutuhan game aktual tanpa memengaruhi operasi game. Fitur ini memudahkan untuk mengatasi perubahan mendadak dalam skala bisnis.

### Kemudahan pembelajaran
Layanan ini mewarisi teknologi pengembangan platform PC dan memanfaatkan pengalaman pengembangan tim game PC. API layanan menyediakan API operasi sinkron dan asinkron yang mudah.

### Operasi berbasis layanan
Dengan mode aplikasi sumber daya yang nyaman, tidak perlu lagi menerapkan lingkungan layanan penyimpanan secara manual.

### Pengoptimalan pemanfaatan sumber daya untuk meningkatkan efisiensi operasional
Alarm dan sistem dasar lainnya terintegrasi untuk menyediakan kemampuan pemantauan tingkat proses. API Layanan menyediakan akses mudah ke perluasan kapasitas server, penyeimbangan beban, dan pemulihan bencana.
