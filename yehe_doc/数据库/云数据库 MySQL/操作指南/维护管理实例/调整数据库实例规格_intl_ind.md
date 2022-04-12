TencentDB for MySQL mendukung penyesuaian cepat dari spesifikasi instans dan memungkinkan operasi penskalaan yang fleksibel di konsol. Anda dapat menyesuaikan spesifikasi instans MySQL secara elastis sesuai dengan kondisi bisnis Anda yang sebenarnya (pada tahap awal, pada tahap pengembangan yang cepat, selama jam sibuk, atau selama jam normal), untuk memenuhi kebutuhan Anda dengan lebih baik seperti penggunaan penuh sumber daya dan optimalisasi biaya real time. Untuk detail tentang biaya penyesuaian instans, lihat [Biaya Penyesuaian Instans](https://intl.cloud.tencent.com/document/product/236/32345).

## Deskripsi Ruang Disk Instans
- Untuk memastikan kelangsungan bisnis, tingkatkan spesifikasi instans Anda atau beli kapasitas disk tambahan tepat waktu sebelum kapasitas disk habis.
>?Anda dapat melihat ruang disk pada halaman detail instans di [konsol MySQL](https://console.cloud.tencent.com/cdb), atau menerima alarm disk sesuai dengan [Kebijakan Alarm (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
- Ketika ukuran data yang disimpan pada instans melebihi batas kapasitasnya, instans akan dikunci dan menjadi baca saja. Anda tidak akan dapat menulis data pada instans tersebut. Anda perlu memperluas kapasitasnya atau menghapus beberapa tabel database di konsol untuk membukanya.
- Untuk menghindari database memicu status kunci berulang kali, instans terkunci akan dibuka kuncinya dan diizinkan untuk membaca dan menulis hanya ketika kapasitas yang tersedia tersisa menyumbang lebih dari 20% dari total kapasitasnya atau lebih dari 50 GB.

## Deskripsi Penyesuaian Konfigurasi
Secara default, konfigurasi instans disesuaikan dalam mode normal, yang memerlukan migrasi data agar penyesuaian selesai setelah Anda menyesuaikan konfigurasi instans di konsol. Namun, jika mesin fisik tempat instans berada memiliki sumber daya yang tersisa (alias sumber daya lokal), Anda dapat memilih mode QuickChange. Proses penyesuaiannya adalah sebagai berikut:
![](https://qcloudimg.tencent-cloud.cn/raw/8e7702c81886573a459dbf73b2846701.png)

- **Normal mode** (Mode normal): untuk menyesuaikan konfigurasi instans, data instans perlu dimigrasikan dari mesin fisik asli ke mesin baru. Karena penyesuaian dalam mode ini memerlukan migrasi, perbandingan, dan verifikasi data, proses penyesuaian secara keseluruhan akan memakan waktu lama jika datanya sangat banyak. Selain itu, peralihan instans dapat terjadi setelah penyesuaian selesai.
- **QuickChange mode** (Mode QuickChange): konfigurasi instans dapat disesuaikan tanpa memigrasikan data atau beralih ke mesin fisik lain. Karena tidak diperlukan persiapan migrasi, proses penyesuaian keseluruhan jauh lebih singkat.
>!
>- Jika sumber daya lokal mencukupi dan memenuhi kondisi mode QuickChange, mode ini akan digunakan secara default. Jika Anda tidak perlu menggunakannya, Anda dapat menonaktifkannya dengan menonaktifkannya di halaman penyesuaian konfigurasi.
>- Dalam mode QuickChange, instans dapat dimulai ulang dan tidak tersedia untuk waktu yang singkat selama penyesuaian konfigurasi.

## Catatan
- Instans baca saja dengan VIP eksklusif yang diaktifkan tidak mendukung QuickChange.
- Jika grup instans baca saja (grup RO) mengaktifkan fitur "Remove Delayed RO Instances" (Hapus Instans RO Tertunda), instans baca saja yang penundaannya melebihi ambang batas yang ditentukan akan dihapus dari grup RO hingga jumlah yang tersisa mencapai jumlah minimum yang diizinkan. Jika jumlah instans baca saja yang tersisa dalam grup RO kurang dari atau sama dengan jumlah minimum yang diizinkan, tidak ada instans tersebut yang akan mendukung QuickChange.
- Jika grup RO hanya memiliki satu instans baca saja, instans tersebut tidak mendukung QuickChange.

## [Aturan Penyesuaian Konfigurasi](id:guize)
- Anda dapat menyesuaikan konfigurasi instans TencentDB for MySQL serta instans baca saja dan pemulihan bencananya yang terkait hanya ketika berada dalam status normal (berjalan) dan tidak menjalankan tugas apa pun.
- Anda tidak dapat membatalkan operasi penyesuaian konfigurasi yang sedang berlangsung.
- Nama, IP akses, dan port akses instans tetap tidak berubah setelah penyesuaian konfigurasi.
- Selama penyesuaian konfigurasi, Anda harus menghindari operasi seperti memodifikasi parameter global MySQL dan kata sandi pengguna.
- Migrasi data mungkin terlibat dalam penyesuaian konfigurasi. Selama migrasi data, instans TencentDB for MySQL dapat diakses secara normal dan bisnis tidak akan terpengaruh.
- Peralihan instans mungkin diperlukan setelah penyesuaian konfigurasi selesai (yaitu, instans MySQL mungkin terputus selama beberapa detik). Sebaiknya aplikasi dikonfigurasi dengan fitur koneksi ulang otomatis dan peralihan instans dilakukan selama periode pemeliharaan instans. Untuk informasi selengkapnya, lihat [Mengatur Periode Pemeliharaan Instans](https://intl.cloud.tencent.com/document/product/236/10929).
- Instans TencentDB for MySQL node tunggal dasar tidak tersedia selama sekitar 15 menit dalam proses penyesuaian konfigurasi. Sebaiknya sesuaikan konfigurasi instans selama jam normal.

## Menyesuaikan Konfigurasi Instans di Konsol
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), cari instans yang diinginkan dalam daftar instans, dan pilih **More** (Lainnya) > **Adjust Configurations** (Sesuaikan Konfigurasi) di kolom **Operation** (Operasi).
2. Di jendela pop-up, pilih konfigurasi yang diinginkan dan klik **Submit** (Kirim).
>?
>- Jika sumber daya lokal memadai, Anda dapat mengaktifkan mode QuickChange dengan mengaktifkan tombol **QuickChange** (QuickChange) pada halaman penyesuaian konfigurasi di konsol.
>![](https://main.qcloudimg.com/raw/c37bb99f0a2db0a9108c7068ad72ba7c.png)
>- Dalam beberapa kasus, mulai ulang instans tidak diperlukan dalam mode QuickChange dan penyesuaian konfigurasi akan segera berlaku setelah Anda mengirimkan permintaan, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/6f5e9ab54f270c0833f5545cccbc8c6d.png)
>
![](https://main.qcloudimg.com/raw/ef2bf519dabe88cb23b9c73993602b9b.png)

## Menyesuaikan Konfigurasi Instans Melalui API
Anda dapat menyesuaikan konfigurasi instans menggunakan API `UpgradeDBInstance`. Untuk informasi selengkapnya, lihat [UpgradeDBInstance](https://intl.cloud.tencent.com/document/product/236/15876).

## Pertanyaan Umum
#### Apakah penyesuaian konfigurasi instans akan memengaruhi instans?
- Dalam proses penyesuaian konfigurasi TencentDB for MySQL, migrasi data dapat terjadi, dan instans masih dapat diakses selama proses tersebut. Setelah migrasi selesai, ada peralihan yang menyebabkan pemutusan singkat yang berlangsung hanya beberapa detik, pastikan bisnis Anda memiliki mekanisme koneksi ulang.
- Instans TencentDB for MySQL node tunggal dasar tidak tersedia selama sekitar 15 menit dalam proses penyesuaian konfigurasi. Sebaiknya sesuaikan konfigurasi instans selama jam normal.

#### Mengapa instans saya tidak dapat diturunkan versinya?
Bisa jadi karena kapasitas penyimpanan yang digunakan sudah mencapai kapasitas maksimal hard disk. Untuk menurunkan versi instans, Anda harus membersihkan data terlebih dahulu dan memastikan sisa kapasitas yang tersedia lebih dari 20% dari total kapasitas atau lebih dari 50 GB.

#### Mengapa instans saya dalam status "Waiting for switch" (Menunggu peralihan) untuk waktu yang lama setelah saya menyesuaikan konfigurasi instans di konsol?
Mungkin karena Anda memilih **During maintenance time** (Selama waktu pemeliharaan) sebagai **Switch Time** (Waktu Peralihan) saat Anda menyesuaikan konfigurasi instans di [konsol](https://console.cloud.tencent.com/cdb), sehingga instans tidak akan langsung dialihkan setelah penyesuaian.
Untuk segera beralih, Anda dapat menemukan instans yang diinginkan dalam daftar instans dan klik **Switch Now** (Beralih Sekarang) di kolom **Operation** (Operasi). Peralihan menyebabkan pemutusan singkat yang berlangsung hanya beberapa detik. Pastikan bisnis Anda memiliki mekanisme koneksi ulang.

#### Berapa lama waktu yang dibutuhkan untuk meningkatkan konfigurasi instans?
Waktu yang diperlukan bergantung pada volume data instans dan permintaan baca untuk mereplikasi data.
Instans masih dapat diakses selama peningkatan, tetapi peralihan VIP menyebabkan pemutusan hubungan singkat yang berlangsung hanya beberapa detik setelah peningkatan selesai.

#### Bagaimana cara melihat kemajuan penyesuaian konfigurasi instans?
Anda dapat melihat kemajuan di [Daftar Tugas](https://console.cloud.tencent.com/mysql/task) di konsol.

#### Apa yang harus saya lakukan jika ruang disk habis?
Jika lebih dari 85% ruang disk yang digunakan, sebaiknya hapus data yang tidak lagi digunakan atau perluas ruang disk di [konsol](https://console.cloud.tencent.com/cdb) dengan memilih **More** (Lainnya) > **Adjust Configurations** (Sesuaikan Konfigurasi) di kolom **Operation** (Operasi) di sebelah kanan daftar instans.

#### Bagaimana cara mengetahui apakah mode QuickChange didukung saat saya menyesuaikan memori instans atau kapasitas disk?
Pada halaman penyesuaian konfigurasi, jika mode QuickChange didukung, tombol **QuickChange** (QuickChange) dapat diaktifkan atau dinonaktifkan sesuai kebutuhan; jika tidak, sakelar tidak dapat digunakan.
![](https://main.qcloudimg.com/raw/0ecdc6d86e3727e7a688a559ce217d7d.png)

#### Apakah perluasan memori atau kapasitas disk memengaruhi versi minor kernel dari instans?
Jika versi minor kernel dari instans bukan yang terbaru saat memori atau kapasitas disk diperluas, versi tersebut akan ditingkatkan ke versi terbaru. Dalam hal ini, mengaktifkan mode QuickChange akan menyebabkan database dimulai ulang.

#### Apakah mengaktifkan mode QuickChange akan menyebabkan instans dimulai ulang?
Instans perlu dimulai ulang dalam beberapa kasus. Perintah apakah akan memulai ulang instans atau tidak akan ditampilkan pada halaman penyesuaian konfigurasi seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/d97d2daa7cb8e5aa0924355c59bc4fc8.png)

>?Jika versi minor kernel dari instans adalah yang terbaru, hanya menyesuaikan kapasitas disk dalam mode QuickChange tidak akan menyebabkan instans dimulai ulang.

#### Bagaimana cara mengetahui apakah mode QuickChange diaktifkan saat saya meningkatkan konfigurasi instans di konsol?
Anda dapat memeriksa peralihan **QuickChange** (QuickChange) di halaman penyesuaian konfigurasi: jika peralihan diaktifkan, mode QuickChange diaktifkan; jika tidak, mode dinonaktifkan.
![](https://main.qcloudimg.com/raw/0ecdc6d86e3727e7a688a559ce217d7d.png)

#### Bagaimana cara mengetahui apakah mode QuickChange diaktifkan saat saya menggunakan API untuk menyesuaikan konfigurasi instans?
API tidak mendukung QuickChange untuk saat ini, jadi konfigurasi instans hanya dapat disesuaikan dengan memigrasikan data jika Anda menggunakan API. API akan mendukung QuickChange di masa mendatang.

#### Apakah parameter database akan diubah selama penyesuaian konfigurasi database?
Parameter `innodb_buffer_pool_size` akan dimodifikasi sesuai dengan perubahan konfigurasi.

#### Apakah parameter database akan diubah selama penyesuaian konfigurasi database dalam mode QuickChange?
Parameter ini sama dengan mode normal. Dalam mode QuickChange, beberapa parameter akan dimodifikasi sesuai dengan perubahan konfigurasi.

#### Apa perbedaan antara mode QuickChange dan mode normal?
Mode QuickChange tidak memerlukan migrasi data, sehingga memerlukan lebih sedikit waktu untuk menyesuaikan konfigurasi instans.
