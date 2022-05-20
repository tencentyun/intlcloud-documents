
Dokumen ini menjelaskan cara menyesuaikan arsitektur instans di konsol TencentDB for SQL Server.

## Latar Belakang Arsitektur
TencentDB for SQL Server mendukung arsitektur deployment berikut:

| Jenis | Deskripsi |
|---------|---------|
| Edisi Dasar | a. Ini memisahkan komputasi dan penyimpanan berdasarkan Penyimpanan Cloud Premium dan di-deploy pada satu node. <br>b. Ini menawarkan efektivitas biaya yang sangat tinggi. |
| Edisi Ketersediaan Tinggi Server Ganda | a. Ini terdiri dari satu database utama dan satu database cermin yang di-deploy di seluruh rak/AZ. <br>b. Setiap database sesuai dengan agen pemantau yang memantau database melalui detak jantung secara real-time. |
| Edisi Kluster | a. Ini mengadopsi arsitektur deployment kluster Always On, termasuk satu primer dan satu replika yang di-deploy di seluruh rak/AZ secara default. <br>b. Setiap database sesuai dengan agen pemantau yang memantau database melalui detak jantung secara real-time. |

Untuk informasi selengkapnya, lihat [Arsitektur](https://intl.cloud.tencent.com/document/product/238/3254).

## Prasyarat
- Anda dapat menyesuaikan konfigurasi instans TencentDB for SQL Server dan instans terkait hanya saat instans tersebut dalam status normal (Berjalan) dan tidak menjalankan tugas apa pun.
- Hanya Edisi Ketersediaan Tinggi (SQL Server 2017 Enterprise dan yang lebih tinggi) yang dapat disesuaikan dengan Edisi Kluster.

## Catatan
Saat ini, arsitektur tidak dapat diturunkan kembali setelah ditingkatkan.

## Dampak Penyesuaian Konfigurasi
- Migrasi data akan terlibat selama penyesuaian konfigurasi instans, dan semakin tinggi volume data, semakin lama waktu migrasi data. Akses ke instans tidak akan terpengaruh selama periode ini.
>- Peralihan akan dilakukan setelah migrasi selesai, yang disertai dengan pemutusan dari database yang berlangsung hanya beberapa detik. Pastikan bisnis Anda memiliki mekanisme koneksi ulang.
- Selama pemutusan sementara, sebagian besar operasi yang terkait dengan database, akun, dan jaringan tidak dapat dijalankan. Dengan demikian, pastikan untuk melakukan peralihan selama jam normal.

## Petunjuk
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver), pilih wilayah dan instans target dalam daftar instans, dan klik **Adjust Configuration** (Sesuaikan Konfigurasi) di kolom **Operation** (Operasi).
![](https://qcloudimg.tencent-cloud.cn/raw/84f60eedd1e5492b31da602ef387b9f9.png)
2. Di jendela **Adjust Configuration** (Sesuaikan Konfigurasi) yang muncul, pilih arsitektur yang diinginkan dan klik **Confirm** (Konfirmasi).
>?Jika migrasi data terlibat selama perubahan, Anda harus memilih waktu efektif dan klik catatan berwarna jingga; jika tidak, Anda tidak perlu memilih waktu efektif.
>- Selama waktu pemeliharaan: Anda dapat mengubah waktu pemeliharaan pada halaman detail instans.
>- Sesuaikan sekarang: penyesuaian konfigurasi akan segera dilakukan.
>
![](https://qcloudimg.tencent-cloud.cn/raw/a84d518ad3526ffd1958cca11061f0a3.png)
3. Pada halaman pembayaran tempat Anda diarahkan, konfirmasi informasi konfigurasi dan biaya dan klik **Submit Order** (Kirim Pesanan).
4. Anda akan diarahkan ke daftar instans. Saat status instans berubah dari **Beralih (setelah penyesuaian konfigurasi** menjadi **Berjalan**, peningkatan arsitektur selesai. Anda dapat mengkueri dan memeriksa arsitektur baru di halaman **Daftar Instans** atau **Detail Instans**.


