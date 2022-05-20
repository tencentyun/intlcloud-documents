TencentDB for Redis memungkinkan Anda membuat grup replikasi di konsol dan menambahkan instans master atau baca saja ke dalamnya, untuk menerapkan sinkronisasi data yang konsisten dalam arsitektur satu master atau multi-master dalam grup replikasi. 

(>?Untuk menggunakan fitur replikasi global, [kirim tiket]https://console.cloud.tencent.com/workorder/category) untuk aplikasi.

## Konsep
- **Instance role:** (Peran instans:) Anda perlu menetapkan peran yang berbeda ke instan dalam grup replikasi, termasuk **master instance** (instans master) dan **read-only instance** (instans baca saja).
  - **Master instance:** (Instans master:) Instans ini menyediakan akses baca/tulis data dan digunakan untuk menulis data bisnis.
  - **Read-only instance:** (Instans baca saja:) Instans ini menyediakan akses baca saja ke data dan digunakan untuk operasi data baca saja atau pemulihan bencana.
- **IP address:**  (Alamat IP:) Setiap instans dalam grup replikasi memiliki alamat IP terpisah, yang dapat diakses secara independen.
- **Master/Replica switch:** (Pengalihan Master/Replika:) Failover otomatis antara node master dan replika di setiap instans dapat dilakukan. Namun, failover otomatis antara instans master dan baca saja tidak didukung.

## Deskripsi Versi
- Replikasi global hanya mendukung instans Arsitektur Standar 4.0, Arsitektur Klaster 4.0, Arsitektur Standar 5.0, dan Arsitektur Klaster 5.0.
- Versi fitur replikasi global saat ini hanya mendukung instans yang di-deploy di AZ yang sama. Instans multi-AZ akan didukung di masa mendatang.

## Catatan
### Batas spesifikasi
- Instans yang berjalan pada arsitektur klaster dapat memiliki hingga 64 shard dalam grup replikasi global.
- Saat membuat grup replikasi, Anda harus menentukan instans master dalam grup.
- Saat ini, Anda dapat menambahkan hingga empat instans ke dalam grup replikasi global dalam skema deployment berikut: satu instans master dan tiga instans baca saja, empat instans master, atau dua instans master dan dua instans baca saja.

### Batas wilayah
Fitur replikasi global dapat mereplikasi data di AZ yang sama atau di seluruh AZ di antara wilayah Tencent Cloud mana pun terlepas dari di mana instans dalam grup replikasi di-deploy.
Saat ini, hanya wilayah dan AZ berikut yang mendukung replikasi global:

| Wilayah | AZ |
|---------|---------|
| Virginia | Zona Virginia 2 |
| Beijing | Zona Beijing 5 |
| Shanghai | Zona Shanghai 5 |
| Hong Kong (China) | Zona Hong Kong 3 |
| Guangzhou | Zone Guangzhou 6 |
| Singapura | Zona Singapura 2 |
| Nanjing | Zona Nanjing 3 |

### Deskripsi perintah
- Perintah **FLUSHDB** (FLUSHDB) atau **FLUSHALL** (FLUSHALL) akan disinkronkan ke semua instans dalam grup replikasi. Karena itu, jalankan perintah tersebut dengan hati-hati.
- Grup perintah **Pub** (Pub) dan **Sub** (Sub) tidak akan disinkronkan. Sebaiknya gunakan struktur data `Stream` untuk mereplikasi pesan notifikasi di seluruh wilayah.
- Saat perintah **RESTORE** (PEMULIHAN) disinkronkan, jika subinstans target memiliki kunci yang sama, perintah tersebut tidak akan dijalankan.

## Deskripsi Penagihan
- Jika instans dalam grup replikasi berada di wilayah yang sama, biaya tambahan tidak akan dikenakan.
- Biaya bandwidth akan dikenakan untuk replikasi data lintas wilayah dalam grup replikasi. Untuk informasi selengkapnya, lihat [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/553/35174).

## Membuat Grup Replikasi Global
### Prasyarat
- Anda telah [membuat instans TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/37712), dan instans tersebut dalam status **Running** (Berjalan).
- Data dalam instans master TencentDB for Redis di grup replikasi telah dihapus. 

## Petunjuk
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis).
2. Pilih **Global Replication** (Replikasi Global) di bilah sisi kiri.
3. Pada halaman **Redis - Global Replication** (Redis - Replikasi Global) di sebelah kanan, klik **Create Replication Group** (Buat Grup Replikasi).
4. Di jendela pop-up **Create Replication Group** (Buat Grup Replikasi), konfigurasikan parameter berikut dan klik **OK** (OKE).
<table width="100">
<thead><tr><th width="15%">Deskripsi</th><th width="55%">Parameter</th><th width="15%">Membutuhkan</th><th width="15%">Nilai Sampel</th></tr></thead>
<tbody>
<tr>
<td>Nama</td>
<td>Nama grup replikasi yang akan dibuat. </td>Masukkan nama seperti yang diminta
<td>Ya</td>
<td>pengujian</td></tr>
<tr>
<td>Keterangan</td>    
<td>Deskripsi singkat tentang grup replikasi. Anda dapat memasukkan karakter apa pun untuk membedakan grup dari yang lain.</td>
<td>Tidak</td>
<td>Pengujian pembuatan grup replikasi</td></tr>
<tr>
<td>Wilayah Instans Master</td> 
<td>Pilih wilayah instans master di grup replikasi.</td>
<td>Ya</td>
<td>Guangzhou</td></tr>
<tr>
<td>Pilih Instans Master</td> 
<td>Pilih instans master dalam grup replikasi, yang tidak boleh memiliki data. Versi, arsitektur, dan kapasitas memori dari instans yang dipilih akan ditampilkan, dan Anda perlu mengonfirmasi apakah spesifikasi memenuhi persyaratan Anda.</td>
<td>Ya</td>
<td>pengujian-XXX</td></tr>
</tbody></table>
> !Kernel Redis dari instans master yang ditentukan selama pembuatan grup replikasi harus ditingkatkan ke Edisi Replikasi Global. Setelah peningkatan selesai, satu atau beberapa pemutusan sementara yang berlangsung selama 5 detik akan terjadi.
> 
5. Kembali ke halaman **Redis - Global Replication** (Redis - Replikasi Global), dan Anda dapat melihat grup replikasi yang baru dibuat dalam daftar grup replikasi.
Klik <img src="https://qcloudimg.tencent-cloud.cn/raw/3a815073e7ccf4206decf7b522a40ccd.png" style="zoom: 67%;" /> sebelum nama grup replikasi untuk menampilkan daftar instansnya, di mana Anda dapat melihat status instans master. Anda dapat menggunakan instans master setelah sistem meningkatkan kernelnya ke edisi Replikasi Global.
![](https://qcloudimg.tencent-cloud.cn/raw/9a49f26745b61d2ab3315e86631da150.png)

## Menambahkan Instans ke Grup Replikasi
Setelah membuat grup replikasi, Anda dapat menambahkan instans di region yang sama atau berbeda dan menetapkan peran instans master dan baca saja ke instans yang ditambahkan sesuai kebutuhan untuk menerapkan sinkronisasi data.

### Catatan
- Saat ini, Anda tidak dapat menambahkan instans multi-AZ ke grup replikasi. Fitur ini akan didukung di masa mendatang, jadi harap tunggu.
- Anda dapat menambahkan hingga **empat** instans ke grup replikasi. Instans tersebut tidak boleh memiliki data; jika tidak, instans tersebut tidak dapat ditambahkan. Menambahkan instans yang sudah memiliki data akan didukung di masa mendatang.
- Instans yang baru ditambahkan ke grup replikasi akan menyinkronkan data dari node instans master, dan instans tersebut tidak dapat dimanipulasi atau diakses sebelum data lengkap disinkronkan.
- Setelah instans ditambahkan ke grup replikasi, edisi kernelnya akan ditingkatkan, dan satu atau beberapa pemutusan sementara akan terjadi setelah peningkatan.

### Prasyarat
- Anda telah membuat grup replikasi global, dan grup tersebut dalam status **Running** (Berjalan).
- Anda telah membuat instans untuk ditambahkan ke grup replikasi. Versi dan arsitektur Redis yang kompatibel harus sama dengan instans master yang ditentukan selama pembuatan grup, kapasitas memorinya harus lebih besar atau sama dengan kapasitas instans master yang digunakan, dan harus dalam status **Running** (Berjalan).
- Jika Anda ingin menentukan instans yang akan ditambahkan sebagai instans master, instans tersebut harus memiliki setidaknya dua node replika.
- Anda harus menghapus data dalam instans yang akan ditambahkan ke grup replikasi terlepas dari apakah instans tersebut akan ditambahkan sebagai instans master atau baca saja.

## Petunjuk
1. Dalam [daftar instans](https://console.cloud.tencent.com/redis/replication) pada halaman **Redis - Global Replication** (Redis - Replikasi Global), pilih grup replikasi target.
2. Di kolom **Operation** (Operasi) grup replikasi, klik **Add Instance** (Tambahkan Instans).
3. Di jendela pop-up **Add Instance** (Tambahkan Instans), baca catatan dengan cermat, konfigurasikan parameter berikut, dan klik **OK** (OKE).
  - **Region** (Wilayah): Pilih wilayah instans target.
  - **Select Instance** (Pilih Instans): Pilih target instans.
  - **Instance Role** (Peran instans): Tetapkan peran (**master instance** (instans master) atau **read-only instance**(instans baca-saja)) ke instans target.
> ? Peran instans tidak dibatasi saat Anda menambahkan instans ke grup replikasi. Atur peran ke instans master atau baca saja sesuai kebutuhan.
> 
4. Kembali ke halaman **Redis - Global Replication** (Redis - Replikasi Global). Dalam daftar grup replikasi, klik <img src="https://qcloudimg.tencent-cloud.cn/raw/3a815073e7ccf4206decf7b522a40ccd.png" style="zoom: 67%;" /> sebelum nama grup replikasi target untuk menampilkan daftar instansnya, di mana Anda dapat melihat instans yang baru ditambahkan.
![](https://qcloudimg.tencent-cloud.cn/raw/9a49f26745b61d2ab3315e86631da150.png)
Anda dapat menambahkan beberapa instans ke grup replikasi sesuai kebutuhan, lalu menyinkronkan data di antara mereka.

## Catatan tentang Ketersediaan
### Pemulihan bencana lintas wilayah
Instans master dan instans baca saja dapat ditambahkan ke grup replikasi untuk menyiapkan sistem pemulihan bencana lintas wilayah. Namun, sistem tidak akan secara otomatis melakukan failover, yang hanya dapat dilakukan secara manual di konsol atau melalui TencentCloud API. Untuk petunjuk mendetail, lihat [Mengalihkan Peran Instans](https://intl.cloud.tencent.com/document/product/239/45604).

### Pengecualian replikasi
Terlepas dari apakah grup replikasi memiliki satu atau beberapa instans master, saat replikasi terganggu, sistem tidak akan menetapkannya sebagai instans baca saja atau melakukan operasi lain; sebagai gantinya, sistem akan secara otomatis melanjutkan pemutaran ulang log inkremental setelah pemulihan instans. Sebaiknya konfigurasi alarm untuk pengecualian replikasi dan atur instans master sebagai instans baca saja ketika pengecualian replikasi seperti gangguan replikasi terjadi, untuk menjamin konsistensi data.

