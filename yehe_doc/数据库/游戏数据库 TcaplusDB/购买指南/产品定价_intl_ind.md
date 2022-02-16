## Mode Penagihan
TencentDB untuk TcaplusDB mendukung dua mode penagihan berikut:

| Jenis Instans | Mode Penagihan | Kasus Penggunaan |
|----|----|----|
|Edisi Kluster Standar |Bayar Sesuai Pemakaian|Mode penagihan ini cocok untuk pengujian, pengauditan, dan lingkungan pengembangan. Anda akan dikenakan biaya sesuai dengan lalu lintas puncak harian. Jika tidak ada permintaan yang dibuat untuk mengakses database, Anda hanya membayar biaya sumber daya minimum yang dipesan.|
|Edisi Kluster yang Di-deploy Mandiri|Bayar Sesuai Pemakaian|Mode penagihan ini cocok untuk lingkungan produksi. Anda akan dikenakan biaya harian sesuai dengan jumlah lapisan akses dan lapisan penyimpanan. Anda dapat mengurangi biaya dengan penskalaan otomatis. Misalnya, Anda dapat memperluas kapasitas kluster sebelum kampanye berdasarkan perkiraan puncak bisnis, dan mengurangi kapasitas kluster setelah kampanye.|

## Siklus Pembayaran
Biaya yang timbul pada hari ini akan ditagihkan pada hari berikutnya.

## Aturan Penagihan untuk Edisi Kluster Standar

Edisi Kluster Standar mengadopsi mode penagihan bayar sesuai pemakaian. Biaya harian dihitung berdasarkan permintaan baca/tulis database puncak dan kapasitas disk puncak yang digunakan dalam sehari.

**Daily fees = Fees of the peak disk capacity used on a day + Fees of the peak RCUs on a day + Fees of the peak WCUs on a day** (Biaya harian = Biaya kapasitas puncak disk yang digunakan dalam sehari + Biaya RCU puncak dalam sehari + Biaya puncak WCU dalam sehari)

**Concepts** (Konsep)
-**Capacity** (Kapasitas): nama kolom kunci utama dan kolom atribut dihitung ke dalam ukuran setiap baris data.
- **Read CU** (Baca CU): satu operasi baca baris tunggal 4 KB per detik dihitung sebagai satu [unit kapasitas baca (RCU)] yang dicadangkan (https://intl.cloud.tencent.com/document/product/1016/36557).
- **Write CU** (Tulis CU): satu operasi tulis baris tunggal 4 KB per detik dihitung sebagai satu [unit kapasitas tulis (WCU)] yang dicadangkan (https://intl.cloud.tencent.com/document/product/1016/36557).
- **CU calculation rule** (Aturan penghitungan CU): CU dihitung secara terpisah di akhir setiap proses permintaan dan respons. CU diakumulasikan dan dihitung berdasarkan permintaan atau tanggapan (mana pun yang lebih besar). Data yang lebih kecil dari 4 KB dibulatkan ke 4 KB terdekat, dan data yang lebih besar dari 4 KB dihitung kelipatan 4 KB. Misalnya, jika respons 9 KB dikembalikan untuk permintaan 1 KB dalam satu detik, karena ukuran respons lebih besar dari ukuran permintaan, jumlah CU akan dihitung berdasarkan nilai respons. 9 KB adalah sekitar dua set 4 KB, dan 1 KB yang tersisa dihitung sebagai 4 KB, sehingga jumlah total CU adalah 2 + 1 = 3.
- **CU statistics rule** (Aturan statistik CU): biaya harian dihitung berdasarkan puncak akses harian ke database. Jika pembacaan database mencapai nilai tertinggi pada pukul 12.00.00 pada suatu hari, RCU saat ini akan digunakan untuk menghitung biaya hari ini. Demikian pula, jika penulisan database mencapai nilai tertinggi pada pukul 15.01.00 pada suatu hari, WCU pada saat ini akan digunakan untuk menghitung biaya hari ini.

### Harga

| Wilayah | Kapasitas (USD/GB/hari) | RCU (USD/CU/hari) | WCU (USD/CU/hari) |
|---------|---------|---------|---------|
| Tiongkok Daratan | 0,0052 | 0,0019 | 0,0048 |
| Silicon Valley (AS Barat) | 0,006289 | 0,002 | 0,0055 |
| Virginia (AS Timur) | 0,006289 | 0,002 | 0,0055 |
| Frankfurt (Jerman) | 0,006 | 0,0022 | 0,0057 |
| Singapura | 0,0061 |0,0025 | 0,0061 |
| Hong Kong (Tiongkok) | 0,0055 | 0,0019 | 0,0055 |
| Jepang | 0,0055 | 0,0019 |0,0055 |
| Seoul | 0,006289 | 0,002546 | 0,00599 |

>?
> - Biaya dikeluarkan setelah kluster dibuat. Konsumsi harian minimum kluster adalah kapasitas disk 1 GB, 80 RCU, dan 26 WCU. Meskipun tidak ada tabel yang dibuat, tetap ada biaya.
> - Setidaknya 1 GB kapasitas disk dicadangkan untuk kluster standar.
> - Setidaknya 80 RCU dicadangkan untuk kluster standar.
> - Setidaknya 26 WCU dicadangkan untuk kluster standar.
>- Edisi Kluster Standar mendukung hingga 100.000 QPS. Permintaan di luar rentang ini akan dibatasi. Jika bisnis Anda membutuhkan lebih dari 100.000 QPS, sebaiknya gunakan Edisi Kluster yang Di-deploy Sendiri yang memberikan performa yang lebih tinggi dan lebih stabil.
### Contoh penagihan
Misalnya Anda membuat kluster di wilayah Shanghai. Dalam sehari, permintaan baca puncak adalah 80 per detik, permintaan tulis puncak adalah 26 per detik, dan puncak kapasitas disk yang digunakan adalah 0,5 GB.
Biaya harian dihitung sebagai berikut:

| Kapasitas (GB) | Permintaan Baca (RCU) | Permintaan Tulis (WCU) | Biaya |
|---------|---------|---------|-------|
| 1 | 80 | 26 | 1 GB × 0,0052 USD/GB/hari + 80 RCU × 0,0019 USD/RCU/hari + 26 WCU × 0,0048 USD/WCU/hari = 0,282 USD/hari|

Asumsikan bahwa dengan promosi bisnis, aplikasi berinteraksi lebih banyak dengan kluster, menghasilkan akses baca/tulis yang lebih tinggi per detik. Jika pembacaan puncak harian mencapai 1.000 RCU/dtk, puncak harian menulis 300 WCU/dtk, dan data puncak harian berukuran 1,5 GB, biaya harian dihitung sebagai berikut:

| Kapasitas (GB) | Permintaan Baca (RCU) | Permintaan Tulis (WCU) | Biaya |
|---------|---------|---------|-------|
| 1,5 | 1.000 | 300 | 1,5 GB × 0,0052 USD/GB/hari + 1.000 RCU × 0,0019 USD/RCU/hari + 300 WCU × 0,0048 USD/WCU/hari = 3,3478 USD |


## Aturan Penagihan untuk Edisi Kluster yang Di-deploy Sendiri
Edisi Kluster yang Di-deploy Sendiri mengadopsi mode penagihan bayar sesuai pemakaian. Biaya harian dihitung berdasarkan sumber daya yang benar-benar digunakan di lapisan penyimpanan dan lapisan akses dalam sehari.

**Daily fees = Daily unit price of access layer × Access layer quantity + Daily unit price of storage layer (which varies with instance type) × Storage layer quantity** (Biaya harian = Harga satuan harian lapisan akses × Jumlah lapisan akses + Harga satuan harian lapisan penyimpanan (yang bervariasi menurut jenis instans) × Jumlah lapisan penyimpanan)

### Harga
| Wilayah| Lapisan Akses (USD/lapisan/hari) | Instans Standar T1 Satu-Utama-Satu-Sekunder di Lapisan Penyimpanan (USD/instans/hari) |
|---------|---------|---------|
| Tiongkok Daratan| 0,51 | 65,22 |
| Virginia (AS Timur) |1,52| 220.58 |
| Silicon Valley (AS Barat) |1,57| 224,49 |
| Frankfurt (Jerman) | 1,57 | 224,49 |
| Singapura | 1,89 | 224,49 |
| Hong Kong (Tiongkok) | 1,89 | 226,38 |
| Jepang | 1,76 | 226,38 |
| Seoul | 1,76 | 222,03 |

### Contoh penagihan
Misalnya Anda membuat kluster yang di-deploy sendiri di wilayah Shanghai. Kluster memiliki empat lapisan akses dan dua lapisan penyimpanan (yaitu, dua instans standar T1 satu-primer-satu-sekunder).
Biaya harian dihitung sebagai berikut:

Biaya lapisan akses harian = 0,5 × 4 = 2 USD/hari
Biaya lapisan penyimpanan harian = 64,28471429 × 2 = 128,56942858 USD/hari

Total biaya harian = 2 + 128,56942858 = 130,56942858 USD/hari
