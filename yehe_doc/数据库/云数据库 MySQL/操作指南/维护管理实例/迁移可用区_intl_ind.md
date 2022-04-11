
Anda dapat memigrasikan instans TencentDB for MySQL ke AZ lain di wilayah yang sama. Semua atribut, konfigurasi, alamat pribadi, dan subnet instans akan tetap tidak berubah setelah migrasi. Waktu yang diperlukan untuk memigrasikan instans bergantung pada volume data instans.

Misalnya, Anda dapat bermigrasi ke AZ baru dalam skenario berikut:
- Jika Anda ingin memodifikasi jenis instans, tetapi AZ saat ini tidak mendukung jenis instans baru, Anda dapat memigrasikan instans ke AZ yang mendukung jenis baru.
- Jika AZ saat ini tidak memiliki sumber daya yang tersisa untuk penskalaan, Anda juga dapat memigrasikan instans ke AZ lain di wilayah yang sama dengan sumber daya yang cukup untuk memenuhi kebutuhan bisnis Anda.

## Prasyarat
- Instans sedang berjalan.
- Wilayah tempat instans berada memiliki beberapa AZ untuk mendukung migrasi lintas-AZ.

## Deskripsi Penagihan
Fitur ini gratis. Tidak ada biaya bahkan untuk memigrasikan instans dari satu AZ ke beberapa AZ.

## Deskripsi Fitur
- Instans akan terpengaruh untuk sementara saat AZ-nya dialihkan; oleh karena itu, pastikan aplikasi Anda memiliki mekanisme koneksi ulang otomatis.
- Migrasi AZ tidak akan menghasilkan perubahan VIP.
- Instans sumber tidak dipisahkan dari instans baca saja setelah migrasi AZ dan masih dapat disinkronkan dengan instans tersebut.
- Anda dapat memilih AZ instans baca saja.
- Instans Baca Saja tidak mendukung migrasi lintas wilayah.
- Tidak ada akses melalui grup RO (penghapusan) yang dapat dilakukan selama peralihan migrasi.
- Jika instans target memiliki kunci tugas di platform cloud selama tugas DTS, migrasi lintas-AZ tidak dapat dilakukan.
- Jika ada tugas DTS yang sedang berlangsung, setelah migrasi AZ, Anda perlu memulai ulang tugas tersebut.
- Ekspor DTS akan gagal jika instans sumber mengalami peralihan migrasi lintas-AZ selama ekspor dumper.
- Untuk migrasi AZ di bawah arsitektur dua node atau tiga node, pemilihan sumber dan replika AZ tunduk pada sumber daya yang tersisa di AZ dan wilayah baru. Anda dapat memilih AZ baru selama migrasi di konsol, dan opsi AZ replika akan diperbarui secara otomatis.

## Jenis Migrasi

| Jenis Migrasi | Skenario yang Berlaku | Jenis Instans yang Didukung |
|---------|---------|---------|
| Migrasi dari satu AZ ke AZ lain | AZ tempat instans berada di bawah beban penuh atau kondisi lain yang memengaruhi performa instans. | Instans sumber, baca saja, dan DR |
| Migrasi dari satu AZ ke beberapa AZ | Anda dapat meningkatkan kemampuan pemulihan bencana instans dan menerapkan pemulihan bencana psat lintas-data. Instans sumber dan replika terletak di AZ yang berbeda. Instans multi-AZ dapat menahan tingkat bencana yang lebih tinggi daripada instans AZ tunggal. Misalnya, instans terakhir dapat mentolerir kegagalan tingkat server dan rak, sedangkan instans pertama dapat mentolerir kegagalan tingkat pusat data. | Instans sumber, baca saja, dan DR |
| Migrasi dari beberapa AZ ke satu AZ | Anda ingin memenuhi persyaratan fitur tertentu. | Instans sumber, baca saja, dan DR |

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik **instance ID** (ID instans) atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail instans.
2. Pada halaman **Instance Details** (Detail Instans), pilih **Basic Info** (Info Dasar) > **Region/AZ** (Wilayah/AZ) dan klik **Migrate to New AZ** (Migrasikan ke AZ Baru), atau pilih **Availability Info** (Info Ketersediaan) > **Deployment Mode** (Mode Deployment) dan klik **Modify Replica AZ** (Modifikasi AZ Replika).
![](https://qcloudimg.tencent-cloud.cn/raw/cd1bd1b09029548391ba986c61027907.png)
3. Di jendela pop-up, sesuaikan konfigurasi yang relevan dan klik **Submit** (Kirim) setelah mengonfirmasi bahwa semua konfigurasi sudah benar.
 - **New AZ** (AZ Baru): Anda dapat mengubah AZ sumber di daftar drop-down atau memilih **Yes** (Ya) untuk **Multi-AZ Deployment** (Deployment Multi-AZ) untuk memodifikasi replika AZ.
 - **Delay Threshold for Data Consistency Check** (Ambang Batas Penundaan untuk Pemeriksaan Konsistensi Data): opsi ini hanya tersedia jika Anda mengubah AZ sumber. Ambang batas dapat berupa bilangan bulat antara 1 dan 10 detik.
>! Mungkin ada penundaan selama pemeriksaan konsistensi data. Anda perlu menetapkan ambang batas penundaan data. Pemeriksaan konsistensi database akan dijeda saat penundaan melebihi nilai yang ditetapkan dan akan dilanjutkan saat penundaan turun di bawah ambang batas. Jika nilai ambang terlalu kecil, migrasi mungkin memakan waktu lebih lama.
 - **Switch Time** (Waktu Peralihan): Anda dapat memilih untuk beralih selama waktu pemeliharaan atau setelah migrasi selesai. Untuk informasi selengkapnya, lihat [Mengatur Periode Pemeliharaan Instans](https://intl.cloud.tencent.com/document/product/236/10929).
![](https://qcloudimg.tencent-cloud.cn/raw/33577bc75f50cb9805478f71b372e07f.png)

