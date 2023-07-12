Mulai Januari 2021, satu kinerja disk Enhanced SSD terdiri dari **kinerja dasar** dan **kinerja ekstra**:
- kinerja dasar bervariasi secara linier dengan kapasitas disk cloud dan mencapai nilai maksimum pada titik kritis.
- Jika Anda memiliki persyaratan kinerja yang lebih tinggi, Anda dapat mengaktifkan dan mengonfigurasi kinerja ekstra.

Dokumen ini memperkenalkan kinerja dasar dan kinerja ekstra.

## Kinerja Keseluruhan

Untuk satu disk Enhanced SSD, kinerjanya terdiri dari dua bagian: **kinerja dasar** dan **kinerja ekstra**. Tabel berikut menentukan kinerja maksimum, terlepas dari proporsi kinerjanya.

| Metrik Kinerja | Nilai Maksimum |
| --------------------- | ------ |
| IOPS Acak             | 100000 |
| Throughput maks (MB/dtk)    | 1000   |



## Kinerja Dasar

Untuk Enhanced SSD, kinerja dasarnya bervariasi secara linier dengan kapasitas disk. Kinerja dasar tidak dapat disesuaikan secara terpisah, yang dihitung dengan rumus berikut.

| Metrik Kinerja Dasar | Rumus Perhitungan | Nilai Maksimum |
| ---------------------------- | --------------------------- | -------------- |
| IOPS acak | min {1800 + kapasitas (GB) × 50, 50000} | 50000 |
| Throughput maksimum (MB/dtk) | min {120 + kapasitas (GB) × 0,5, 350} | 350 |

Menurut rumus,

- Jika kapasitas disk 460 GB, throughput mencapai nilai maksimum dan kinerja dasarnya adalah: IOPS acak: 24.800; throughput maksimum: 350 MB/dtk.
- Jika kapasitas disk 964 GB, IOPS acak mencapai nilai maksimum dan kinerja dasarnya adalah: IOPS acak: 50.000; throughput maksimum: 350 MB/dtk.



## Kinerja Ekstra

Jika Anda memiliki persyaratan kinerja yang lebih tinggi, Anda dapat mengaktifkan kinerja ekstra.

### Prasyarat

Persyaratan berikut harus dipenuhi untuk memungkinkan kinerja ekstra:

- Saat ini, fitur ini hanya tersedia untuk disk **Enhanced SSD** dan **Tremendous SSD**.
- Kinerja ekstra hanya dapat dikonfigurasi setelah metrik kinerja dasar mencapai nilai maksimumnya. Dengan kata lain, kapasitas disk harus lebih besar dari 460 GB sesuai dengan rumus kinerja dasar.

### Rumus kinerja ekstra

Lihat rumus berikut untuk mengonfigurasi kinerja ekstra.

| Metrik kinerja Ekstra | Rumus Perhitungan | Nilai Maksimum |
| ---------------------------- | --------------------- | -------------- |
| IOPS acak | min {nilai yang dikonfigurasi × ​​128, 50000} | 50000 |
| Throughput maksimum (MB/dtk) | min {nilai yang dikonfigurasi × ​​1, 650} | 650 |

### Harga kinerja ekstra
Untuk informasi selengkapnya tentang harga kinerja ekstra, lihat [Ikhtisar Harga](https://intl.cloud.tencent.com/document/product/362/2413).

## Contoh

**Contoh 1: disk Enhanced SSD memerlukan kapasitas 2.000 GB dan throughput 500 MB/dtk**

Konfigurasi kapasitas ini mencapai batas throughput kinerja dasar dan perlu mengonfigurasi kinerja throughput ekstra: (500-350)/1 = 150. Oleh karena itu, Anda perlu membeli disk Enhanced SSD dengan kapasitas 2.000 GB dan kinerja throughput ekstra 150 MB/dtk.

**Contoh 2: disk Enhanced SSD membutuhkan kapasitas 1.000 GB dan IOPS 50.000**
Konfigurasi kapasitas ini mencapai batas IOPS acak dari kinerja dasar, dan IOPS yang diperlukan terpenuhi. Oleh karena itu, Anda hanya perlu membeli disk Enhanced SSD dengan kapasitas 1.000 GB.
