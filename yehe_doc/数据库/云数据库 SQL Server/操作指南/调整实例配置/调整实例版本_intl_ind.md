Dokumen ini menjelaskan cara menyesuaikan versi instans di konsol TencentDB for SQL Server.

## Prasyarat
Anda dapat menyesuaikan konfigurasi instans TencentDB for SQL Server dan instansnya yang terkait hanya jika mereka dalam status normal (Berjalan) dan tidak menjalankan tugas apa pun.

## Catatan
Saat ini, versi database tidak dapat diturunkan kembali setelah ditingkatkan.

## Dampak Penyesuaian Konfigurasi
- Migrasi data akan terlibat selama penyesuaian konfigurasi instans, dan semakin tinggi volume data, semakin lama waktu migrasi data. Akses ke instans tidak akan terpengaruh selama periode ini.
>- Peralihan akan dilakukan setelah migrasi selesai, yang disertai dengan pemutusan dari database yang berlangsung hanya beberapa detik. Pastikan bisnis Anda memiliki mekanisme koneksi ulang.
- Selama pemutusan sementara, sebagian besar operasi yang terkait dengan database, akun, dan jaringan tidak dapat dijalankan. Dengan demikian, pastikan untuk melakukan peralihan selama jam normal.

## Petunjuk
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver), pilih wilayah dan instans target dalam daftar instans, dan klik **Adjust Configuration** (Sesuaikan Konfigurasi) di kolom **Operation** (Operasi).
![](https://qcloudimg.tencent-cloud.cn/raw/84f60eedd1e5492b31da602ef387b9f9.png)
2. Di jendela **Adjust Configuration** (Sesuaikan Konfigurasi) yang muncul, pilih **database version** (versi database) yang diinginkan dan klik **Confirm** (Konfirmasi).
>?Pilih **Time to Take Effect** (Waktu untuk Berlaku) dari penyesuaian konfigurasi dan klik catatan berwarna jingga.
> - Selama waktu pemeliharaan: Anda dapat mengubah waktu pemeliharaan di halaman detail instans.
>- Sesuaikan sekarang: penyesuaian konfigurasi akan segera dilakukan.
>
![](https://qcloudimg.tencent-cloud.cn/raw/f232f1ed96e136d859685b302d3061cf.png)
3. Pada halaman pembayaran tempat Anda diarahkan, konfirmasi informasi konfigurasi dan biaya dan klik **Submit Order** (Kirim Pesanan).
4. Anda akan diarahkan ke daftar instans. Saat status instans berubah dari **Switching (after configuration adjustment)** (Beralih (setelah penyesuaian konfigurasi)) menjadi **Running** (Berjalan), peningkatan versi selesai. Anda dapat mengkueri dan memeriksa versi baru di halaman **Instance List** (Daftar Instans) atau **Instance Details** (Detail Instans).

