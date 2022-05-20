
Edisi Memori TencentDB for Redis (Arsitektur Standar) adalah edisi yang mendukung nol atau lebih replika (replika adalah node yang bukan node master), yang merupakan edisi Redis yang paling umum. Edisi ini kompatibel dengan protokol dan perintah Redis v2.8, v4.0, dan v5.0 dan menampilkan persistensi dan pencadangan data, sehingga cocok untuk skenario di mana keandalan dan ketersediaan data yang tinggi diperlukan. Node master menyediakan akses layanan harian, sedangkan node replika memastikan ketersediaan tinggi (HA). Jika node master gagal, sistem akan secara otomatis beralih ke node replika untuk menjamin kelangsungan bisnis.

Edisi Memori (Arsitektur Standar) - satu replika:
![](https://main.qcloudimg.com/raw/0bb5f79eea8c50f2817050211a0ed77f.jpg)

## Deskripsi Replika
Edisi Memori (Arsitektur Standar) mendukung 0–5 replika untuk memenuhi persyaratan yang berbeda untuk ketersediaan dan kinerja bisnis Anda dalam skenario yang berbeda. Semua replika Edisi Memori (Arsitektur Standar) berperan dalam mendukung ketersediaan tinggi sistem, sehingga makin banyak replika, makin tinggi ketersediaannya. Jika jumlah replika lebih besar dari 1, pemisahan baca/tulis dapat diaktifkan untuk memperluas kinerja baca melalui node replika.
>? Edisi Memori TencentDB for Redis 4.0 (Arsitektur Standar) mendukung 0–9 replika di wilayah Beijing dan Guangzhou atau 0–5 replika di wilayah lain. Versi lain hanya mendukung 0–5 replika.
>

**Definisi**:
- Node master: node Redis yang menyediakan kemampuan baca dan tulis.
- Node replika: node Redis yang menyediakan ketersediaan tinggi atau kemampuan baca saja. Node master tidak bisa menjadi node replika.

**Dukungan replika**:
<table>
<tr><th >Versi Instans</th><th >Replika yang Didukung</th><th >Pemisahan Baca/Tulis</th>  </tr>
<tr>      
<td>Edisi Memori TencentDB for Redis 2.8 (Arsitektur Standar)</td><td>0–1</td><td>Tidak didukung</td></tr> 
<tr>
<td>Edisi Memori TencentDB for Redis 4.0 (Arsitektur Standar)</td><td>0–5</td><td>Didukung</td></tr> 
<tr>
<td>Edisi Memori TencentDB for Redis 5.0 (Arsitektur Standar)</td><td>0–5</td><td>Didukung</td></tr> 
</table>

**Instans Nol Replika**:
- Data mungkin hilang ketika sebuah node gagal; oleh karena itu, jangan gunakan instans nol replika dalam skenario penyimpanan data.
- Instans nol-replika hanya cocok untuk skenario cache murni. Sistem aplikasi dapat terus berjalan meskipun terjadi kegagalan Redis, tetapi sebagai instans nol-replika hanya memiliki satu node database, ketika node gagal, sistem akan memulai proses Redis baru (yang tidak memiliki data), dan setelah node failover selesai, aplikasi perlu melakukan pemanasan data lagi untuk menghindari tekanan akses pada database backend.

**Replika Baca Saja (pemisahan baca/tulis)**:
- Edisi yang didukung: Edisi Memori TencentDB for Redis 4.0 (Arsitektur Standar) dan instans di atasnya. Ketika jumlah replika lebih besar dari 1, pemisahan baca/tulis otomatis dapat diaktifkan untuk memperluas kinerja baca secara vertikal. Hingga 5 node replika dapat didukung.
- Cara kerjanya: setelah replika baca saja diaktifkan, permintaan tulis akan dirutekan ke node master, sedangkan permintaan baca akan dirutekan ke semua node replika melalui algoritme penyeimbangan beban dan tidak lagi diproses oleh node master. Fitur pemisahan baca/tulis ini disediakan oleh komponen Proksi yang dibangun di TencentDB for Redis.
- Mengaktifkan/Menonaktifkan: Anda dapat mengaktifkan atau menonaktifkan replika baca saja pada halaman pembuatan instans di konsol TencentDB for Redis atau melalui TencentCloud API.

## Fitur
- **Keandalan layanan (1-5 replika)**
Dengan arsitektur master/replika server ganda, node master dan replika berada pada mesin fisik yang berbeda dengan node master menyediakan akses eksternal. Anda dapat melakukan CRUD data menggunakan baris perintah atau klien Redis. Jika node master gagal, sistem ketersediaan tinggi (HA) yang dipatenkan akan secara otomatis menjalankan peralihan master/replika untuk memastikan kelancaran operasi bisnis. 
- **Keandalan data (1-5 replika)**
Fitur persistensi data diaktifkan secara default. Edisi Memori (Arsitektur Standar) mendukung pencadangan data. Anda dapat memutar kembali atau mengkloning instans untuk set cadangan guna mengatasi maloperasi data dan masalah lainnya secara efektif.

## Batasan Penggunaan
- Edisi Memori (Arsitektur Standar) mendukung kapasitas penyimpanan 0,25–64 GB. Untuk spesifikasi yang lebih tinggi, gunakan Edisi Kluster yang mendukung kapasitas hingga 8 TB.
- Edisi Memori (Arsitektur Standar) mendukung hingga 100.000 QPS (konkurensi perintah SET). Jika Anda membutuhkan QPS yang lebih tinggi, Anda dapat memilih pemisahan baca/tulis multi-replika atau menggunakan Edisi Kluster Redis yang mendukung puluhan juta QPS.
- Karena instans nol-replika tidak dapat memastikan keandalan data, dan data bisnis perlu dipanaskan setelah kegagalan node, jika bisnis Anda memerlukan ketersediaan data yang tinggi, Anda tidak disarankan untuk menggunakan instans nol-replika; karenanya, Anda dapat memilih instans replika tunggal atau multi-replika.

## Kompatibilitas Perintah
Untuk informasi selengkapnya tentang perintah yang didukung, lihat [Kompatibilitas Perintah](https://intl.cloud.tencent.com/document/product/239/31958).

​    
