TencentDB for MySQL mendukung peningkatan versi minor kernel otomatis atau manual. Peningkatan menambahkan fitur baru, meningkatkan kinerja, dan memperbaiki masalah.
Untuk detail tentang TencentDB untuk versi minor kernel MySQL, harap lihat [Pembaruan Versi Kernel](https://intl.cloud.tencent.com/document/product/236/35989).

>?Saat ini, instans node tunggal dasar tidak mendukung peningkatan versi kernel minor.

## Ikhtisar
- **Automatic upgrade** (Peningkatan otomatis):
 - Skenario 1: ketika bug parah atau kerentanan keamanan terjadi di TencentDB for MySQL, sistem akan melakukan peningkatan versi minor kernel database selama jendela pemeliharaan dan mengirimkan pemberitahuan peningkatan melalui Pusat Pesan konsol dan SMS.
 - Skenario 2: ketika instans TencentDB for MySQL dimigrasikan karena peningkatan/penurunan konfigurasi instans, perluasan/pengurangan kapasitas penyimpanan, atau peningkatan versi database, dll., sistem akan secara otomatis meningkatkan kernel instans ke versi minor terbaru.
- **Manual upgrade** (Peningkatan manual):
Anda juga dapat meningkatkan versi minor kernel secara manual di konsol.


## Aturan Peningkatan
- Jika instans yang akan ditingkatkan dikaitkan dengan instans lain (mis., instans sumber dan replika baca saja), instans ini akan ditingkatkan bersama untuk memastikan konsistensi data.
- Peningkatan TencentDB for MySQL melibatkan migrasi data. Waktu yang diperlukan untuk memigrasikan instans bergantung pada ukuran data instans. Bisnis Anda tidak akan terpengaruh selama peningkatan dan dapat diakses seperti biasa.

## Catatan
- Peralihan instans mungkin diperlukan setelah peningkatan versi selesai (yaitu, instans MySQL mungkin terputus selama beberapa detik). Sebaiknya aplikasi dikonfigurasi dengan fitur rekoneksi otomatis dan peralihan instans dilakukan selama jendela pemeliharaan instans. Untuk informasi selengkapnya, lihat [Mengatur Jendela Pemeliharaan Instans](https://intl.cloud.tencent.com/document/product/236/10929).
- Jika jumlah tabel dalam satu instans melebihi satu juta, peningkatan mungkin gagal dan pemantauan database mungkin terpengaruh. Harap pastikan jumlah tabel dalam satu instans tidak lebih dari satu juta.
- Versi minor kernel tidak dapat diturunkan setelah ditingkatkan.

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb) dan klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail instans.
2. Di bagian **Configuration Info** (Info Konfigurasi), klik **Upgrade Kernel Minor Version** (Tingkatkan Versi Minor Kernel).
![](https://main.qcloudimg.com/raw/3fda3cffc784b3cde619e698d728d486.png)
3. Di kotak dialog pop-up, pilih waktu peralihan dan klik **Upgrade** (Tingkatkan).
>! Karena peningkatan database melibatkan migrasi data, setelah peningkatan selesai, maka dapat terjadi pemutusan hubungan yang sangat singkat dari database MySQL yang berlangsung hanya beberapa detik. Kami menyarankan Anda memilih **During maintenance time** (Selama waktu pemeliharaan) sebagai waktu peralihan, sehingga sakelar akan dimulai dalam waktu pemeliharaan berikutnya setelah peningkatan instans selesai.
>
![](https://qcloudimg.tencent-cloud.cn/raw/c758e092bce297bbfeb553297bf9b266.png)

