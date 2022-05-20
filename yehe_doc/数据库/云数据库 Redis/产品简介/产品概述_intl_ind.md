TencentDB for Redis adalah database cache yang disediakan oleh Tencent Cloud berdasarkan protokol Redis yang menampilkan ketersediaan, keandalan, dan fleksibilitas tinggi. Kompatibel dengan protokol Redis 2.8, 4.0, dan 5.0 dan tersedia dalam arsitektur standar dan kluster, mendukung hingga 8 TB kapasitas penyimpanan dan puluhan juta permintaan bersamaan, memenuhi kebutuhan skenario yang berbeda seperti caching, penyimpanan, dan komputasi.


## Fitur Produk
- Hot backup master/replika: hot backup master/replika, pemantauan kegagalan otomatis, dan pemulihan bencana otomatis didukung.
- Pencadangan data: arsitektur standar dan kluster mendukung persistensi data, cold backup harian, dan pengembalian manual.
- Penskalaan elastis: kapasitas instans, node, dan replika dapat diperluas atau dikurangi secara fleksibel.
- Perlindungan jaringan: VPC didukung untuk meningkatkan keamanan cache.
- Penyimpanan terdistribusi: data Anda didistribusikan di beberapa mesin fisik, membantu Anda menghilangkan kapasitas mandiri dan kendala sumber daya.

## Edisi Produk
TencentDB for Redis tersedia dalam arsitektur standar dan kluster untuk pilihan Anda berdasarkan persyaratan kinerja aktual Anda. Arsitektur standar memiliki kompatibilitas yang lebih tinggi, tetapi kinerjanya dibatasi pada satu node tunggal. Arsitektur kluster tidak sekompetibel yang standar, tetapi dapat ditingkatkan untuk mendukung hingga puluhan juta permintaan bersamaan.
<table>  
<tr><th>Jenis Instans</th><th>Kuantitas Replika</th><th>Pemisahan Baca/Tulis</th><th>Deskripsi</th>  </tr>  
<tr>  
<td>Edisi Memori (arsitektur standar)</td><td >0 hingga 5</td><td >Didukung</td><td >Edisi ini kompatibel dengan protokol Redis 2.8, 4.0, dan 5.0. v2.8 mendukung 0 replika dan hemat biaya jika hanya digunakan sebagai cache. v4.0 atau v5.0 mendukung 1 hingga 5 replika, dan kapasitas instans serta replika dapat diskalakan tanpa gangguan layanan.<br>Edisi ini mendukung hot backup master/replika, sinkronisasi data real-time, dan failover dalam hitungan detik.</td></tr>  
<tr>  
<td>Edisi Memori (arsitektur kluster)</td><td >1 hingga 5</td><td >Didukung</td><td >Edisi ini kompatibel dengan protokol Redis 4.0 dan 5.0. Arsitektur kluster mendukung 1 hingga 128 pecahan dengan kapasitas penyimpanan maksimum 8 TB dan puluhan juta QPS. <br>Edisi ini mendukung master/replika hot backup, sinkronisasi data real-time, dan failover dalam hitungan detik.</td></tr>  
</table>  
