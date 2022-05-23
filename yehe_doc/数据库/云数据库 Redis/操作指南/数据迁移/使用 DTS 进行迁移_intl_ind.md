## Ikhtisar DTS
Layanan Transmisi Data (DTS) Tencent Cloud adalah layanan transfer data yang mengintegrasikan fitur-fitur seperti migrasi data, sinkronisasi, dan langganan, yang membantu Anda memigrasikan database tanpa mengganggu bisnis Anda dan membangun arsitektur database dengan ketersediaan tinggi untuk pemulihan bencana jarak jauh melalui saluran sinkronisasi real-time. Fitur langganan datanya memberi Anda akses real-time ke data yang diperbarui secara bertahap di instans TencentDB Anda, sehingga Anda dapat menggunakan data tersebut berdasarkan kebutuhan bisnis Anda. Saat ini, DTS for Redis mendukung migrasi data pada berbagai versi Redis dan dalam berbagai skenario jaringan.

| Jangka Waktu | Deskripsi |
|---------|---------|
| Instans sumber | Instans sumber migrasi. |
| Instans target | Instans target yang akan dimigrasikan, yaitu TencentDB for Redis yang dibeli pengguna. |
| Instans yang dibuat sendiri di CVM | Layanan Redis yang di-deploy pada instans CVM. |
| Instans yang dibuat sendiri di jaringan publik | Layanan Redis di-deploy di jaringan publik. |

## Deskripsi Dukungan Migrasi
>?Untuk masalah kompatibilitas dengan migrasi dari arsitektur standar ke arsitektur kluster, lihat [Catatan tentang Migrasi dari Arsitektur Standar ke Arsitektur Kluster](https://intl.cloud.tencent.com/document/product/239/37594).

#### Fitur yang didukung
- Migrasi data: DTS mendukung migrasi satu kali semua data ke cloud.
- Sinkronisasi data: DTS mendukung sinkronisasi data real-time dengan cloud, dengan menggabungkan migrasi penuh dan sinkronisasi inkremental.

#### Versi yang didukung
- DTS mendukung Redis 2.8, 3.0, 3.2, 4.0, dan 5.0.
- DTS mendukung arsitektur node tunggal, kluster Redis, Codis, dan twemproxy.
- Persyaratan izin migrasi: untuk memigrasikan data melalui DTS, instans sumber harus mendukung perintah SYNC atau PSYNC.

#### Jaringan yang didukung
DTS mendukung migrasi data dan sinkronisasi data di seluruh jaringan publik, instans yang dibuat oleh CVM, gateway Direct Connect, gateway VPN, dan CCN.

#### Skenario yang didukung
- Migrasi ke cloud: DTS mendukung migrasi instans Redis Anda dalam IDC tradisional ke TencentDB for Redis, memindahkan bisnis Anda ke cloud dengan cara yang efisien dan nyaman.
- Migrasi layanan yang dibuat sendiri: DTS mendukung migrasi layanan Redis Anda yang dibuat dengan mesin virtual di Tencent Cloud atau cloud lainnya ke TencentDB for Redis.
- Migrasi data Redis dari vendor cloud lainnya: DTS mendukung migrasi data Redis dari vendor cloud lain ke Tencent Cloud dengan syarat bahwa izin perintah SYNC atau PSYNC telah diberikan.
- Migrasi antar instans di Tencent Cloud: DTS mendukung migrasi data atau sinkronisasi real-time antar instans di Tencent Cloud. Versi yang didukung adalah sebagai berikut:
  
<table>
<caption></caption>
<tr>
<th style="width:130px;position:relative;text-align:left;padding:5px px;font-weight:00;" valign="top">
<div style="position:absolute;width:1px;height:140px;top:0;left:0;background-color: #d9d9d9;display:block;transform:rotate(-66deg);transform-origin:top;valign=top;"></div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Instans Target<br>Instans Sumber
</th>
</div>
</th>
<th style="background-color:#f2f2f2;">Edisi Memori 2.8 (arsitektur standar)</th>
<th style="background-color:#f2f2f2;">Edisi Memori 4.0 (arsitektur standar)</th>
<th style="background-color:#f2f2f2;">Edisi Memori 4.0 (arsitektur kluster)</th>
<th style="background-color:#f2f2f2;">Edisi Memori 5.0 (arsitektur standar)</th>
<th style="background-color:#f2f2f2;">Edisi Memori 5.0 (arsitektur kluster)</th>
</tr>
<tr>
<td style="background-color:#f2f2f2;">Edisi Memori 2.8 (arsitektur standar)</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td style="background-color:#f2f2f2;">Edisi Memori 4.0 (arsitektur standar)</td>
<td>x</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td style="background-color:#f2f2f2;">Edisi Memori 4.0 (arsitektur kluster)</td>
<td>x</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td style="background-color:#f2f2f2;">Edisi Memori 5.0 (arsitektur standar)</td>
<td>x</td>
<td>x</td>
<td>x</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td style="background-color:#f2f2f2;">Edisi Memori 5.0 (arsitektur kluster)</td>
<td>x</td>
<td>x</td>
<td>x</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
</table>

#### Batasan migrasi
- Untuk memastikan efisiensi migrasi, migrasi lintas wilayah tidak didukung untuk instans yang dibuat sendiri di CVM.
- Untuk memigrasikan instans melalui jaringan publik, pastikan bahwa instans sumber dapat diakses dari jaringan publik.
- Hanya instans yang berjalan normal yang dapat dimigrasikan, sedangkan instans tanpa sandi yang diinisialisasi atau dengan tugas yang sedang berlangsung tidak dapat dimigrasikan.
- Instans target harus kosong tanpa data. Selama proses migrasi, instans target akan menjadi baca saja dan tidak dapat ditulisi.
- Setelah data yang berhasil dimigrasikan diverifikasi oleh bisnis Anda, koneksi ke instans sumber dapat ditutup, dan selanjutnya dialihkan ke instans target.

## Proses Migrasi
### 1. Buat tugas migrasi
1) Login ke [konsol DTS](https://console.cloud.tencent.com/dts) dan klik **Create Migration Task** (Buat Tugas Migrasi) di halaman migrasi data.
2) Pilih wilayah yang sesuai di **Linkage Region** (Kawasan Tautan) dan klik **Buy at 0 USD** (Beli dengan harga 0 USD).

### 2. Konfigurasikan tugas
- Nama tugas: tentukan nama untuk tugas ini.
- Eksekusi terjadwal: tentukan waktu mulai tugas migrasi.
>?
> - Untuk mengubah tugas terjadwal, Anda harus mengeklik **Scheduled start** (Mulai terjadwal) lagi setelah verifikasi berhasil, sehingga tugas dapat dimulai pada waktu yang ditentukan.
> - Jika waktu yang ditentukan telah berlalu, tugas akan segera dimulai. Anda juga dapat mengeklik **Immediate start** (Mulai segera) untuk segera memulai tugas.

### 3. Atur instans sumber dan instans target
Instans Redis pada CVM digunakan di sini sebagai contoh, dan hal yang sama berlaku untuk migrasi instans melalui jaringan publik.

| Bidang | Deskripsi | Keterangan | Diperlukan |
|---------|---------|---------|---------|
| Nama tugas | Nama tugas migrasi | Digunakan oleh pengguna untuk pengelolaan tugas mereka | Ya |
| Instans CVM (ID/IP pribadi) | ID dan IP pribadi dari instans CVM tempat instance Redis sumber berada | Tugas migrasi memeriksa kondisi berjalan CVM dan IP pribadi berdasarkan ID instans CVM | Ya |
| Port | Nomor port instans sumber | Tugas migrasi akan mengakses layanan instans sumber | Ya |
| Kata sandi | Kata sandi instans sumber | Kata sandi digunakan untuk autentikasi untuk mengakses instans sumber | Tidak |
| ID instans TencentDB | ID instans target | Data disinkronkan ke instans target | Ya |

**Catatan tentang migrasi dalam edisi kluster**
DTS mendukung migrasi di Edisi Kluster Redis. Untuk skema kluster dengan arsitektur Kluster Redis, Codis, atau twemproxy, cukup masukkan alamat dan kata sandi semua node pecahan dari kluster sumber sebagai informasi node saat membuat tugas. Sangat disarankan untuk melakukan migrasi data dari node replika instans sumber guna menghindari dampak apa pun terhadap akses bisnis ke instans sumber. DTS mendukung migrasi bebas kata sandi. Berikut ini adalah contoh memasukkan informasi yang relevan untuk migrasi:
![](https://main.qcloudimg.com/raw/513d89660769db2dfd155514bcb38dfc.png)

### 4. Mulai tugas migrasi
1) Setelah pengujian konektivitas jaringan berhasil, klik **Save** (Simpan).
2) DTS mulai memverifikasi tugas migrasi, dan setelah persyaratan migrasi terpenuhi, tugas migrasi akan dimulai.
3) Saat tugas dimulai, status tugas akan berubah menjadi **Memverifikasi**, yang menunjukkan bahwa putaran verifikasi parameter lainnya sedang berlangsung. Selama proses ini berlangsung, Anda hanya dapat membatalkan atau melihat tugas atau memeriksa kemajuan verifikasinya.
4) Setelah verifikasi parameter berhasil, migrasi data akan dimulai.
Selama sinkronisasi data berlangsung, perubahan offset data, instans sumber, dan kunci instans target akan ditampilkan.

### 5. Konfigurasikan alarm migrasi
DTS mendukung gangguan migrasi yang mengkhawatirkan untuk memberi Anda informasi tentang pengecualian. Alarm migrasi dapat dikonfigurasi sebagai berikut:
1) Login ke [konsol Cloud Monitor](https://console.cloud.tencent.com/monitor/policylist) dan pilih **Alarm Configuration** (Konfigurasi Alarm) > **Alarm Policy** (Kebijakan Alarm) di bilah sisi kiri.
2) Klik **Create** (Buat) untuk membuat kebijakan alarm.
 - Jenis kebijakan: pilih **Data Transmission Service** (Layanan Transmisi Data) > **Self-built Migration** (Migrasi yang Dibuat Sendiri).
 - Objek alarm: pilih tugas DTS yang akan dipantau dan konfigurasikan **Trigger Condition** (Kondisi Pemicu) dan **Alarm Object** (Objek Alarm) untuk menyelesaikan konfigurasi alarm.
![](https://main.qcloudimg.com/raw/120d51cd7bc4b66e3722ae6adcbf9469.png)

### 6. Selesaikan tugas migrasi 
Sebelum menonaktifkan sinkronisasi data, data dapat diverifikasi pada instans target, dan jika semuanya sudah benar, tugas migrasi dapat diselesaikan.
Jika kunci instans sumber dan instans target identik, klik **Complete** (Selesai) untuk menyelesaikan sinkronisasi data.

