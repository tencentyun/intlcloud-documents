
Spesifikasi
### Edisi Memori
>?
>- Sebagai versi percobaan, spesifikasi 256 MB pada v4.0 atau v5.0 hanya cocok untuk verifikasi produk di lingkungan pengujian, tetapi tidak disarankan untuk digunakan di lingkungan produksi. Versi ini hanya tersedia di Zona Shanghai 5, Zona Beijing 6, dan Zona Guangzhou 6. Spesifikasi 1 GB dan lebih besar tidak dapat diturunkan ke spesifikasi 256 MB.
>- v2.8 saat ini tidak tersedia, dan disarankan v4.0 atau yang lebih baru. Untuk pembelian v2.8, [kirim tiket](https://console.cloud.tencent.com/workorder/category).
<table>
<thead><tr>
<th width=15%>Fitur</th><th colspan="2" width=60%>Arsitektur Standar</th><th width=25%>Arsitektur Kluster</th></tr></thead>
<tbody><tr>
<td>Versi Redis yang kompatibel</td><td width=30%>2.8</td><td width=30%>4.0 dan 5.0</td><td>4.0 dan 5.0</td></tr>
<tr>
<td>Memori</td><td>256 MB hingga 64 GB</td><td>256 MB hingga 64 GB
</td><td>2 GB hingga 8 TB</td></tr>
<tr>
<td>Jumlah pecahan</td><td>N/A</td><td>N/A</td><td>1 hingga 128</td></tr>
<tr>
<td>QPS</td><td>80.000 hingga 100,000</td><td>80.000 hingga 100.000</td><td>80.000 hingga 100.000 per pecahan</td></tr>
<tr>
<td>Koneksi maksimal</td><td>10.000 secara default dan hingga 40.000</td><td>10.000 secara default dan hingga 40.000</td><td>10.000/pecahan secara default dan hingga 40.000</td></tr>
<tr>
<td>Batas lalu lintas</td><td>10 MB/s hingga 64 MB/s</td><td>528 MB/s hingga 608 MB/s</td><td>288 MB/s hingga 72 GB/s</td></tr>
<tr>
<td>Multi-Database</td><td>Didukung</td><td>Didukung</td><td>Didukung</td></tr>
<tr>
<td>Mget, Mset</td><td>Didukung</td><td>Didukung</td><td>Didukung</td></tr>
<tr>
<td>Lua</td><td>Didukung</td><td>Didukung</td><td>Didukung (akses cross-slot tidak didukung))</td></tr>
<tr>
<td>Penskalaan horizontal</td><td>Tidak Didukung</td><td>Tidak Didukung</td><td>Didukung</td></tr>
<tr>
<td>Penskalaan replika</td><td>Tidak Didukung</td><td>Didukung</td><td>Didukung</td></tr>
<tr>
<td>Pemisahan Baca/Tulis</td><td>Tidak Didukung</td><td>Didukung</td><td>Didukung</td></tr>
<tr>
<td>GEO</td><td>Tidak Didukung Didukung</td><td>Didukung</td><td>Didukung</td></tr>
<tr>
<td>Kuantitas replika</td><td>0 hingga 1</td><td>1 hingga 5</td><td>1 hingga 5</td></tr>
</tbody></table>


### Edisi CKV
<table>
<thead>
<tr><th width=20%>Fitur</th><th width=30%>Arsitektur Standar</th><th width=50%>Arsitektur Kluster</th></tr></thead>
<tbody><tr>
<td>Versi Redis yang kompatibel</td><td>3.2</td><td>3.2</td></tr>
<tr>
<td>Memori</td><td>4 GB hingga 384 GB</td><td>12 GB hingga 48 TB</td></tr>
<tr>
<td>Kuantitas pecahan</td><td>N/A</td><td>3 hingga 128</td></tr>
<tr>
<td>QPS</td><td>80.000 hingga 120.000</td><td>Puluhan juta</td></tr>
<tr>
<td>Koneksi maksimal</td><td>12.000 hingga 24.000</td><td>12.000 hingga 24.000 per pecahan</td></tr>
<tr>
<td>Batas lalu lintas</td><td>16 MB/s hingga 256 MB/s</td><td>72 MB/s hingga 32 GB/s</td></tr>
<tr>
<td>Multi-Database</td><td>Didukung</td><td>Didukung</td></tr>
<tr>
<td>Mget, Mset</td><td>Didukung</td><td>Didukung</td></tr>
<tr>
<td>lua</td>
<td>Didukung</td><td>Dukungan terbatas (untuk menggunakan Lua dalam edisi kluster, Anda perlu memastikan bahwa kunci yang diakses dalam skrip Lua berada di slot yang sama, dan bidang `key` harus disertakan dalam parameter perintah)</td></tr>
<tr>
<td>Penskalaan horizontal</td><td>Didukung</td><td>Didukung</td></tr>
<tr>
<td>Pensjalaan replika</td><td>Tidak Didukung</td><td>Tidak Didukung</td></tr>
<tr>
<td>Pemasihan Baca/Tulis</td><td>Tidak Didukung</td><td>Tidak Didukung</td></tr>
<tr>
<td>GEO</td><td>Tidak Didukung</td><td>Tidak Didukung</td></tr>
</tbody></table>

### Lalu lintas dan koneksi
#### Edisi Memori
| Spesifikasi (GB) | Koneksi Maks | Throughput Maks (MB/s) |
|  :----------: |  :----------: |  :-------------------: |
| 0.25          | 3,000       | 10                  |
| 1          | 40.000       | 16                  |
| 2          | 40.000       | 24                  | 
| 4          | 40.000       | 24                  |
| 8          | 40.000       | 24                  |
| 12         | 40.000       | 32                  | 
| 16         | 40.000       | 32                  | 
| 20         | 40.000       | 48                  |
| 24         | 40.000       | 48                  | 
| 32         | 40.000       | 48                  | 
| 40         | 40.000       | 64                  | 
| 48         | 40.000       | 64                  | 
| 60         | 40.000       | 64                  | 

#### Edisi CKV
| Spesifikasi (GB) | Koneksi Maks | Throughput Maks (MB/s) | 
|  :----------: |  :----------: |  :-------------------: |
| 4          | 10.000       | 24                  |
| 8          | 10.000       | 24                  |
| 16         | 10.000       | 32                  | 
| 24         | 10.000       | 32                  | 
| 32         | 10.000       | 32                  | 
| 48         | 18.000      | 64                  | 
| 64         | 18.000      | 64                  | 
| 80         | 18.000      | 64                  |
| 96         | 18.000      | 64                  | 
| 128        | 24.000      | 128                 | 
| 160        | 24.000      | 128                 | 
| 192        | 24.000      | 128                 | 
| 256        | 24.000      | 256                 | 
| 320        | 24.000      | 256                 | 
| 384        | 24.000      | 256                 | 

Koneksi edisi kluster = jumlah koneksi per pecahan * jumlah pecahan;
Throughput edisi kluster = throughput pecahan * jumlah pecahan
>!Setelah penskalaan, instans lama yang mampu hingga 9.000 koneksi akan mampu 10.000 koneksi.

## Data Kinerja
### Referensi Kinerja
Waktu yang dibutuhkan untuk menjalankan perintah Redis berbeda-beda. Bisnis menggunakan perintah database yang berbeda di lingkungan produksi mereka; oleh karena itu, nilai kinerja yang sesuai juga akan berbeda-beda. Hasil pengujian yang tercantum di sini diperoleh dengan parameter tertentu dan hanya untuk referensi Anda. Lakukan pengujian di lingkungan bisnis aktual Anda untuk hasil yang lebih akurat.

#### Kinerja uji node tunggal
| Spesifikasi Instans Redis | Koneksi | QPS |
|:---------:|:---------:|:--------:|
| Edisi Memori (Arsitektur Standar), 8 GB | 10.000 | 80.000-100.000 |
| Edisi Memori (Arsitektur Kluster), 8 GB (per pecahan) | 10.000 | 80.000-100.000 |
| Edisi CKV (Arsitektur Standar), 8 GB|  12.000    |   80.000-120.000  |

#### Kinerja pengujian arsitektur kluster
Performa Edisi Memori (Arsitektur Kluster) = Performa Edisi Memori (Arsitektur Standar) * jumlah pecahan
Performa Edisi CKV (Arsitektur Kluster) = Performa Edisi CKV (Arsitektur Standar) * jumlah pecahan

### Metode Pengujian
#### Lingkungan Pengujian
| Jumlah CVM tempat Klien Uji Tekanan Diinstal | Inti CVM | CVM MEM | Wilayah | Spesifikasi Instans Redis |
|:---------:|:---------:|:---------:|:---------:|:---------:|
| 3 | 2 |8 GB | Zona Guangzhou 2 | Edisi Memori (Arsitektur Standar), 8 GB | 
| 3 | 2 |8 GB | Zona Guangzhou 2 | Edisi CKV (Arsitektur Standar), 8 GB |

#### Parameter Pengujian
 ```
redis-benchmark -h 10.66.187.x -p 6379 -a crs-1znib6aw:chen2016 -t set -c 3500 -d 128 -n 25000000 -r 5000000
redis-benchmark -h 10.66.187.x -p 6379 -a crs-1z5536aw:chen2016 -t set -c 3500 -d 128 -n 25000000 -r 5000000
redis-benchmark -h 10.66.187.x -p 6379 -a crs-090rjlih:1234567 -t set -c 3500 -d 128 -n 25000000 -r 5000000
```

#### Perhitungan QPS
Jumlah nilai QPS dari tiga klien uji tekanan (diuji dengan redis-benchmark).

