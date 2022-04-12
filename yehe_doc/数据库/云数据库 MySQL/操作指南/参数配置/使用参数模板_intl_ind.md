Selain templat parameter sistem yang disediakan oleh TencentDB for MySQL, Anda dapat membuat templat parameter kustom untuk mengonfigurasi parameter dalam batch.

Anda dapat menggunakan templat parameter untuk mengonfigurasi dan mengelola parameter mesin database. Templat seperti kontainer nilai parameter mesin database, yang dapat diterapkan ke satu atau beberapa instans TencentDB.
Anda dapat login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb) dan klik **Parameter Templates** (Templat Parameter) di bilah sisi kiri untuk membuat, melihat, dan mengelola templat parameter yang mendukung fitur berikut:
- Mendukung templat parameter default.
- Membuat templat dengan memodifikasi parameter default untuk menghasilkan skema pengoptimalan parameter kustom.
- Mengimpor file konfigurasi MySQL `my.conf` untuk menghasilkan templat.
- Menyimpan konfigurasi parameter sebagai templat.
- Mengimpor parameter dari templat untuk diterapkan ke satu atau beberapa instans.
>!Jika parameter dalam templat diperbarui, parameter instans tidak diperbarui kecuali jika diterapkan kembali secara manual ke instans. 
>Anda dapat menerapkan perubahan parameter ke satu atau beberapa instans dengan mengimpor templat.


## Membuat Templat Parameter
Anda dapat membuat templat parameter, mengubah nilai parameter, dan menerapkan templat ke instans.
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates), pilih **Parameter Templates** (Templat Parameter) di bilah sisi kiri, dan klik **Create Template** (Buat Templat).
![](https://main.qcloudimg.com/raw/bd2e7b2373beade127ddafbe46a7ba68.png)
2. Di kotak dialog pop-up, tentukan konfigurasi berikut, dan klik **Create and Set Parameters** (Buat dan Atur Parameter).
 - **Template Name** (Nama Templat): masukkan nama templat yang unik.
 - **Database Version** (Versi Database): pilih versi database.
 - **Template Description** (Deskripsi Templat): masukkan deskripsi singkat tentang templat parameter.
![](https://main.qcloudimg.com/raw/a93abb9d05b05c0018c46d5efa027221.png)
3. Setelah proses pembuatan selesai, Anda dapat mengubah, mengimpor, dan mengekspor parameter di halaman detail templat.

## Menerapkan Templat Parameter ke Instans
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates) dan pilih **Parameter Templates** (Templat Parameter) di bilah sisi kiri.
2. Dalam daftar templat parameter, cari templat yang diinginkan dan klik **Apply to Instances** (Terapkan ke Instans) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/4598668de63c22bcbef5f7a20b262f02.png)
3. Pada halaman yang ditampilkan, tentukan mode eksekusi dan instans, pastikan semua nilai parameter sudah benar, lalu klik **Submit** (Kirim).
 - **Execution Mode** (Mode Eksekusi): **Immediate execution** (Eksekusi langsung) dipilih secara default. Jika Anda memilih **During maintenance window** (Selama periode pemeliharaan), tugas modifikasi parameter akan dijalankan dan berlaku selama [periode pemeliharaan instans](https://intl.cloud.tencent.com/document/product/236/10929).
 - **MySQL Instance** (Instans MySQL): memilih satu atau beberapa instans yang perlu menerapkan templat parameter di wilayah yang ditentukan.
 - **Parameter Comparison** (Perbandingan Parameter): melihat nilai parameter yang diubah dari instans yang dipilih.
 >!Sebelum menerapkan templat parameter ke beberapa instans, pastikan parameter dapat diterapkan ke instans tersebut.
 >
![](https://main.qcloudimg.com/raw/cdb5878b84b497bbea7d981cb4e9749d.png)
4. (Opsional) Jika tugas modifikasi parameter atau modifikasi batch telah dikirimkan tetapi Anda ingin membatalkannya, Anda dapat memilih **[Task List](https://console.cloud.tencent.com/mysql/task)** ([Daftar Tugas]) di bilah sisi kiri di konsol, menemukan tugas, dan mengklik **Cancel** (Batal) di kolom **Operation** (Operasi). Anda dapat membatalkan tugas hanya sebelum dijalankan. Status tugas harus "Menunggu dijalankan".
![](https://main.qcloudimg.com/raw/98b1462f86e0b274ab8380726c5ddc52.png)


## Menyalin Templat Parameter
Untuk menyertakan sebagian besar parameter dan nilai kustom dari templat parameter yang ada di templat baru, Anda dapat menyalin templat yang ada.

### Metode 1. Menyalin templat parameter yang ada
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates), pilih **Parameter Templates** (Templat Parameter) di bilah sisi kiri, klik nama templat parameter atau **View Details** (Lihat Detail) di kolom **Operation** (Operasi) di kolom daftar templat, dan masuk ke halaman detail templat parameter.
2. Pilih **More** (Lainnya) > **Save as Template** (Simpan sebagai Templat) di bagian atas.
3. Di kotak dialog pop-up, tentukan konfigurasi berikut: 
  - **Template Name** (Nama Templat): masukkan nama templat yang unik.
  - **Template Description** (Deskripsi Templat): masukkan deskripsi singkat tentang templat parameter.
4. Setelah mengonfirmasi bahwa semua konfigurasi sudah benar, klik **Save** (Simpan).

### Metode 2. Menyimpan parameter instans sebagai templat parameter
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), pilih **Instance List** (Daftar Instans) di bilah sisi kiri, dan klik ID/nama instans dalam daftar instans untuk mengakses halaman manajemen instans.
2. Pilih **Database Management** (Manajemen Database) > **Parameter Settings** (Pengaturan Parameter) dan klik **Save as Template** (Simpan sebagai Templat).
3. Di kotak dialog pop-up, tentukan konfigurasi berikut:
  - **Template Name** (Nama Templat): masukkan nama templat yang unik.
  - **Template Description** (Deskripsi Templat): masukkan deskripsi singkat tentang templat parameter.
4. Setelah mengonfirmasi bahwa semuanya sudah benar, klik **Create and Save** (Buat dan Simpan).


## Memodifikasi Nilai Parameter dalam Templat Parameter
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates), pilih **Parameter Templates** (Templat Parameter) di bilah sisi kiri, klik nama templat parameter atau **View Details** (Lihat Detail) di kolom **Operation** (Operasi) di kolom daftar templat, dan masuk ke halaman detail templat parameter.
2. Klik **Batch Modify Parameters** (Modifikasi Parameter secara Massal) atau klik <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> di kolom **Current Value** (Nilai Saat Ini) untuk memodifikasi nilai parameter.
>!Jika Anda mengklik **Import Parameters** (Impor Parameter), Anda perlu mengunggah file konfigurasi parameter lokal. Untuk menghindari kegagalan pengimporan, file konfigurasi harus dalam format yang sama dengan file konfigurasi server database MySQL, atau Anda dapat menggunakan templat file parameter yang diekspor.
>
![](https://main.qcloudimg.com/raw/d582cbb01aec5e7c6072fb2b04f74b45.png)

## Mengimpor Templat Parameter
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates), pilih **Parameter Templates** (Templat Parameter) di bilah sisi kiri, klik nama templat parameter atau **View Details** (Lihat Detail) di kolom **Operation** (Operasi) di kolom daftar templat, dan masuk ke halaman detail templat parameter.
2. Klik **Import Parameters** (Impor Parameter).
>!Jika Anda mengklik **Import Parameters** (Impor Parameter), Anda perlu mengunggah file konfigurasi parameter lokal. Untuk menghindari kegagalan pengimporan, file konfigurasi harus dalam format yang sama dengan file konfigurasi server database MySQL, atau Anda dapat menggunakan templat file parameter yang diekspor.
>
3. Di kotak dialog pop-up, pilih file yang akan diunggah dan klik **Import and Overwrite Original Parameters** (Impor dan Timpa Parameter Asli).

## Mengekspor Templat Parameter
#### Metode 1
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates) dan pilih **Parameter Templates** (Templat Parameter) di bilah sisi kiri.
2. Dalam daftar templat parameter, cari templat yang diinginkan dan klik **Export** (Ekspor) di kolom **Operation** (Operasi).

#### Metode 2
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates), pilih **Parameter Templates** (Templat Parameter) di bilah sisi kiri, klik nama templat parameter atau **View Details** (Lihat Detail) di kolom **Operation** (Operasi) di kolom daftar templat, dan masuk ke halaman detail templat parameter.
2. Pilih **More** (Lainnya) > **Export Parameters** (Ekspor Parameter) di bagian atas.

## Menghapus Templat Parameter
Jika templat parameter dibuat secara berlebihan atau tidak lagi diperlukan, templat tersebut dapat dengan mudah dihapus.
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/mysql/parameter-templates) dan pilih **Parameter Templates** (Templat Parameter) di bilah sisi kiri.
2. Dalam daftar templat parameter, cari templat yang diinginkan dan klik **Delete** (Hapus) di kolom **Operation** (Operasi).
3. Klik **OK** (OKE) di kotak dialog pop-up.


## Lihat Juga
Untuk saran mengenai konfigurasi parameter kunci, lihat [Saran tentang Pengaturan Parameter](https://intl.cloud.tencent.com/document/product/236/38056).
