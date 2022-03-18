Saat Anda mematikan atau memulai ulang CVM, kegagalan mungkin terjadi. Meskipun ini adalah peristiwa yang jarang terjadi, Anda dapat memecahkan masalah sebagai berikut:

## Kemungkinan Penyebab

- Penggunaan CPU atau memori yang tinggi.
- ACPI belum terinstal di CVM Linux.
- Pembaruan sistem CVM Windows memakan waktu terlalu lama.
- CVM Windows belum menyelesaikan inisialisasi saat Anda membelinya untuk pertama kali.
- Sistem operasi rusak karena adanya perangkat lunak yang diinstal atau virus seperti Trojan.

## Pemecahan Masalah

### Periksa penggunaan CPU/memori

1. Periksa penggunaan CPU/memori berdasarkan sistem operasi CVM.
 - Untuk CVM Windows: Klik kanan "Taskbar" (Bilah tugas) dan pilih **Task Manager** (Pengelola Tugas) pada CVM.
 - Untuk CVM Linux: Jalankan perintah `top` untuk melihat informasi di kolom `%CPU` dan `%MEM`.
2. Hentikan proses dengan penggunaan CPU atau memori yang tinggi.
Jika Anda masih tidak dapat mematikan atau memulai ulang CVM, jalankan [pematian atau pemulaian ulang paksa](#ForcedShutdownOrRestart).

### Periksa apakah ACPI telah diinstal
> Operasi ini untuk CVM Linux.
>
Jalankan perintah berikut untuk melihat apakah ada proses ACPI.
```
ps -ef | grep -w "acpid" | grep -v "grep"
```
 - Jika ada proses ACPI, jalankan [pematian atau pemulaian ulang paksa](#ForcedShutdownOrRestart).
 - Jika tidak ada proses ACPI, instal ACPI. Untuk operasi tertentu, lihat [Konfigurasi Manajemen Daya Linux](https://intl.cloud.tencent.com/document/product/213/2129).


### Periksa apakah WindowsUpdate sedang berjalan
> Operasi ini untuk CVM Windows.
>
Pada antarmuka sistem operasi CVM Windows, klik **Start**(Mulai) > **Control Panel** (Panel Kontrol) > **Windows Update** (Pembaruan Windows) untuk melihat apakah ada patch atau program yang sedang diperbarui.
- Windows dapat melakukan patching saat sistem dimatikan. Pembaruan mungkin memakan waktu lama, menyebabkan pematian/pemulaian ulang CVM gagal. Sebaiknya Anda menunggu pembaruan Windows selesai lalu mencoba mematikan atau memulai ulang CVM.
- Jika tidak ada patch atau program yang diperbarui, jalankan [pematian atau pemulaian ulang paksa](#ForcedShutdownOrRestart).


### Periksa apakah CVM telah menyelesaikan inisialisasi
> Operasi ini untuk CVM Windows.
>
Saat Anda membeli CVM Windows untuk pertama kalinya, inisialisasi mungkin memakan waktu lebih lama karena Sysprep digunakan untuk mendistribusikan citra. Sebelum inisialisasi selesai, Windows akan mengabaikan operasi mematikan dan memulai ulang.
- Jika CVM Windows yang Anda beli sedang diinisialisasi, sebaiknya Anda menunggu inisialisasi selesai sebelum mematikan atau memulai ulang CVM lagi.
- Jika CVM sudah menyelesaikan inisialisasi, jalankan [pematian atau pemulaian ulang paksa](#ForcedShutdownOrRestart).

### Periksa apakah perangkat lunak yang diinstal normal
 
Gunakan alat pemeriksa atau perangkat lunak antivirus untuk melihat apakah perangkat lunak yang diinstal pada CVM normal atau diserang oleh virus seperti Trojan.
- Jika pengecualian ditemukan, sistem mungkin rusak, menyebabkan proses pematian dan pemulaian ulang gagal. Sebaiknya Anda menghapus instalan perangkat lunak, mencadangkan data, atau memindai dengan perangkat lunak keamanan, lalu menginstal ulang sistem.
- Jika tidak titemukan adanya pengecualian, jalankan [pematian atau pemulaian ulang paksa](#ForcedShutdownOrRestart).

<span id="MandatoryShutdownOrRestart"></span>
### Mematikan/memulai ulang paksa

> Mematikan/memulai ulang paksa yang disediakan oleh Tencent Cloud dapat digunakan jika Anda gagal mematikan atau memulai ulang CVM setelah beberapa kali mencoba. Fitur ini memungkinkan Anda untuk memaksa mematikan atau memulai ulang CVM, yang dapat menyebabkan kehilangan data atau merusak sistem file.
>
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Di halaman manajemen instans, pilih CVM yang ingin Anda matikan atau mulai ulang.
 - Matikan CVM: Klik **More** (Lainnya) > **Instance Status** (Status Instans) > **Shutdown** (Matikan).
 - Mulai ulang CVM: Klik **More** (Lainnya) > **Instance Status** (Status Instans) > **Restart** (Mulai Ulang).
3. Di jendela **Shutdown** (Matikan) atau **Restart Instance** (Mulai Ulang Instans) yang muncul, centang **Forced Shutdown** (Matikan Paksa) atau **Forced Restart** (Mulai Ulang Paksa), dan Klik **Ok** (Oke).
 - Centang **Forced Shutdown** (Matikan Paksa), seperti gambar di bawah ini:
 ![](https://main.qcloudimg.com/raw/22db326eebab11c60e6bbcf8baa23144.png)
 - Centang **Forced Restart** (Mulai ulang Paksa), seperti gambar di bawah ini:
 ![](https://main.qcloudimg.com/raw/61ae4a4185110b7ff86507e15047211f.png)
