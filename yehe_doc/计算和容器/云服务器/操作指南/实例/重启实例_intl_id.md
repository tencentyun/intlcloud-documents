## Skenario Operasi

Memulai ulang instans CVM adalah metode umum untuk memeliharanya. Langkah ini sama dengan memulai ulang sistem operasi komputer lokal. Dokumen ini menjelaskan cara memulai ulang instans.

## Catatan
 - **Preparing to restart instances:** (Mempersiapkan untuk memulai ulang instans:) Instans tidak dapat menyediakan layanan selama proses mulai ulang. Pastikan sebelum memulai ulang CVM bahwa instans telah berhenti menerima permintaan layanan.
 - **How to restart instances:** (Cara memulai ulang instans:) Sebaiknya mulai ulang instans menggunakan operasi mulai ulang yang disediakan oleh Tencent Cloud, bukan menjalankan perintah mulai ulang di instans (seperti perintah luncurkan ulang di Windows dan perintah boot ulang di Linux).
 - **Restart time:** (Waktu mulai ulang:) Umumnya, dibutuhkan hanya beberapa menit untuk memulai ulang instans.
 - **Physical features of instances:** (Fitur fisik instans:) Memulai ulang instans tidak mengubah fitur fisiknya. Alamat IP publik dan pribadinya serta data yang disimpan tidak akan diubah.
 - **Billing:** (Penagihan:) Memulai ulang instans tidak akan memulai periode penagihan instans baru.

## Petunjuk

Anda dapat memulai ulang instans melalui metode berikut:
- [Gunakan konsol untuk memulai ulang instans](#consoleRestart)
- [Gunakan API untuk memulai ulang instans](#apiRestart)

<span id="consoleRestart"></span>
### Menggunakan konsol untuk memulai ulang instans

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/).
2. Pada halaman manajemen instans, pilih metode mulai ulang instans berdasarkan jumlah aktual instans yang akan dimulai ulang.
 - Memulai ulang satu instans: Pada baris instans yang ingin Anda mulai ulang, klik **More** (Lainnya) > **Instance Status** (Status Instans) > **Restart** (Mulai Ulang), seperti yang ditunjukkan di bawah ini:
 ![Memulai ulang satu instans](https://main.qcloudimg.com/raw/56eb6421097130f3f424f582ff3d9f14.png)
 - Memulai ulang beberapa instans: Centang semua instans yang ingin Anda mulai ulang, lalu klik **Restart** (Mulai Ulang) di bagian atas daftar untuk memulai ulang instans secara massal. Jika tidak dapat dimulai ulang, alasannya akan ditampilkan, seperti yang ditunjukkan di bawah ini:
![Memulai ulang beberapa instans](https://main.qcloudimg.com/raw/c6eb646bd8d19e5484d43be3b9cac9bf.png)
> Satu instans juga dapat dimulai ulang menggunakan metode ini.

<span id="apiRestart"></span>
### Menggunakan API untuk memulai ulang instans
Lihat [RebootInstances API](https://intl.cloud.tencent.com/document/product/213/33243).
