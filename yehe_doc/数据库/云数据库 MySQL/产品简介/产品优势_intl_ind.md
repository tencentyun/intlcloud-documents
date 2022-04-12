
>?Keunggulan yang dijelaskan dalam dokumen ini eksklusif untuk instans TencentDB for MySQL dual-node dan tiga node.

## Efektivitas Biaya dan Kemudahan Penggunaan
- **Read/write separation is supported** (Mendukung pemisahan baca/tulis)
Replika baca saja dapat dipasang ke TencentDB for MySQL. Arsitektur satu sumber dengan banyak replika memungkinkan Anda untuk menanggapi permintaan besar-besaran. Grup RO dengan fitur penyeimbangan beban didukung untuk mengoptimalkan distribusi tekanan di antara replika baca saja.

- **Powerful hardware ensures high performance** (Perangkat keras yang canggih memastikan performa tinggi)
NVMe SSD menampilkan performa IO tinggi, memastikan pembacaan dan penulisan yang lancar.
Maksimum 240.000 QPS dan ruang penyimpanan maksimum 6 TB didukung untuk instans.

## Keamanan Tinggi
- **Anti-DDoS protection** (Perlindungan Anti-DDoS)
Saat Anda mengalami serangan DDoS, fitur ini dapat membantu Anda menahan berbagai lalu lintas serangan, memastikan operasi bisnis yang normal.

- **Protection against database attacks** (Perlindungan terhadap serangan database)
Pertahanan yang efektif terhadap serangan database seperti injeksi SQL dan serangan brute force.

## Keandalan Tinggi
Data disimpan secara online dalam arsitektur sumber/replika, memastikan keamanan data yang tinggi. Selain itu, data cadangan dapat disimpan untuk jangka waktu yang lama, memungkinkan pemulihan data jika terjadi bencana database.

- **Data encryption** (Enkripsi data)
Fitur enkripsi data transparan (TDE) menjamin keamanan data real-time dan data cadangan.

- **Database audit** (Audit database)
Fitur audit data tingkat keuangan membantu mencegah pencurian data inti, melacak operasi yang tidak sesuai, dan menemukan penarikan berbahaya.

## Ketersediaan Tinggi
- **Real-time hot backup** (Pencadangan terbaru secara real-time)
Mekanisme pencadangan terkini server ganda mendukung pemulihan data tanpa kehilangan dari 7-732 hari terakhir berdasarkan pencadangan data dan pencadangan log (binlog). Pencadangan tersebut dapat disimpan selama 7-732 hari.

- **Automatic disaster recovery** (Pemulihan bencana otomatis)
Deteksi kegagalan otomatis dan failover otomatis didukung. Prosedur peralihan sumber/replika dan failover tidak terlihat oleh pengguna.

## Keuntungan dibandingkan Database Buatan Sendiri
- **Easy management of massive databases** (Pengelolaan database besar yang mudah)
Database dapat dikelola melalui baris perintah atau konsol. Manajemen database batch, pengaturan izin, dan impor SQL didukung. 

- **Data import and backup rollback** (Impor data dan pengembalian pencadangan)
Beberapa metode impor data disediakan untuk inisialisasi. Data dicadangkan secara otomatis setiap hari. TencentDB memungkinkan data untuk dikembalikan ke titik waktu mana pun dalam periode penyimpanan berdasarkan file cadangan.

- **Professional monitoring and alarm** (Pemantauan dan alarm profesional)
Pemantauan multidimensi dan alarm berdasarkan ambang batas sumber daya khusus didukung. Anda juga dapat mengunduh laporan analisis kueri lambat dan menyelesaikan laporan menjalankan SQL.

- **A variety of access methods** (Berbagai metode akses)
Akses ke jaringan publik dan VPC didukung. Anda dapat menghubungkan instans TencentDB ke IDC, cloud pribadi, atau sumber daya komputasi lainnya untuk di-deploy di cloud hibrida dengan mudah.
