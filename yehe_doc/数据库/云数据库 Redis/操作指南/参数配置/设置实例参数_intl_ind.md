
Anda dapat melihat dan mengubah parameter tertentu dan log modifikasi parameter kueri di konsol TencentDB for SQL Server.

## Catatan
- Untuk memastikan stabilitas instans, hanya beberapa parameter yang dapat dimodifikasi di konsol. Parameter ini ditampilkan di halaman **Parameter Settings** (Pengaturan Parameter).
- Jika parameter yang dimodifikasi memerlukan mulai ulang instans untuk diterapkan, sistem akan menanyakan apakah Anda ingin memulai ulang. Sebaiknya Anda melakukannya selama jam normal dan memastikan bahwa aplikasi Anda memiliki mekanisme koneksi ulang.

## Memodifikasi Parameter Secara Massal
1. Masuk ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Parameter Configuration** (Konfigurasi Parameter) > **Parameter Settings** (Pengaturan Parameter) dan klik **Batch Modify Parameters** (Modifikasi Parameter Secara Massal).
![](https://main.qcloudimg.com/raw/eb99fc02ef937bcf284cde55c65defc7.png)
3. Temukan parameter target dan modifikasi nilainya di kolom **Current Value** (Nilai Saat Ini). Setelah mengonfirmasi bahwa semuanya sudah benar, klik **OK** (OKE).
![](https://main.qcloudimg.com/raw/56e48d579e473235848479d9c0bfd809.png)
4. Di jendela pop-up, pilih **Execution Mode** (Mode Eksekusi) dan klik **OK** (OKE).
>?
>- Jika Anda memilih **Immediate execution** (Eksekusi langsung), tugas modifikasi parameter akan dijalankan dan segera berlaku.
>- Jika Anda memilih **During maintenance time** (Selama waktu pemeliharaan), tugas modifikasi parameter akan dijalankan dan berlaku selama [waktu pemeliharaan instans](https://intl.cloud.tencent.com/document/product/238/35785).
> 
![](https://main.qcloudimg.com/raw/09cd7df6181f175a265a3c0c29a71b25.png)

## Memodifikasi Satu Parameter
1. Masuk ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans untuk mengakses halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Parameter Configuration** (Konfigurasi Parameter)  > **Parameter Settings** (Pengaturan Parameter), pilih baris parameter target, dan klik ![img](https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png) di kolom **Current Value** (Nilai Saat Ini) untuk mengubah nilainya.
![](https://main.qcloudimg.com/raw/840cd20adf065b0fa30adefed997a640.png)
3. Masukkan nilai parameter target seperti yang diminta di kolom **Current Value** (Nilai Saat Ini) dan klik ![img](https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png) untuk menyimpan perubahan. Anda dapat mengeklik ![img](https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png) untuk membatalkan operasi.
![](https://main.qcloudimg.com/raw/896f3db37107b9e3c69d7b3cd1164f55.png)
4. Di jendela pop-up, pilih **Execution Mode** (Mode Eksekusi) dan klik **OK** (OKE).
>?
>- Jika Anda memilih **Immediate execution** (Eksekusi langsung), tugas modifikasi parameter akan dijalankan dan segera berlaku.
>- Jika Anda memilih **During maintenance time** (Selama waktu pemeliharaan), tugas modifikasi parameter akan dijalankan dan berlaku selama [waktu pemeliharaan instans](https://intl.cloud.tencent.com/document/product/238/35785).
>
![](https://main.qcloudimg.com/raw/f31ea4d1b771972dbde10e5fab9eb763.png)
