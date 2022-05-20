## Ikhtisar
Periode pemeliharaan adalah konsep yang sangat penting untuk TencentDB for SQL Server. Untuk memastikan stabilitas instans TencentDB for SQL Server, sistem backend melakukan operasi pemeliharaan pada instans selama periode pemeliharaan dari waktu ke waktu. Sebaiknya tetapkan waktu pemeliharaan yang dapat diterima untuk instans Anda, biasanya selama jam normal, untuk meminimalkan potensi dampak pada bisnis Anda.

Selain itu, sebaiknya operasi juga melakukan migrasi data selama waktu pemeliharaan, seperti penyesuaian spesifikasi instans, peningkatan versi instans, dan peningkatan kernel instans. Saat ini, konsep periode pemeliharaan didukung oleh instans utama dan baca saja.

Ambil peningkatan spesifikasi instans database sebagai contoh. Mengambil peningkatan spesifikasi instans database sebagai contoh, karena operasi ini melibatkan migrasi data, setelah peningkatan selesai, pemutusan sementara dari database dapat terjadi. Saat peningkatan dimulai, **waktu peralihan** dapat dipilih sebagai **selama periode pemeliharaan**, sehingga peralihan spesifikasi instans akan diaktifkan selama **periode pemeliharaan** berikutnya setelah peningkatan instans selesai. Perlu diketahui bahwa ketika Anda melakukannya, peralihan tidak akan terjadi segera setelah peningkatan spesifikasi database selesai; sebagai gantinya, sinkronisasi akan berlanjut hingga instans memasuki **periode pemeliharaan** berikutnya saat peralihan akan dilakukan. Dengan cara ini, keseluruhan waktu yang diperlukan untuk meningkatkan instans dapat diperpanjang.

>?
>- Sebelum pemeliharaan dilakukan untuk TencentDB for SQL Server, pemberitahuan akan dikirimkan ke kontak yang telah dikonfigurasi di akun Tencent Cloud Anda melalui SMS dan email.
>- Peralihan instans disertai dengan pemutusan dari database yang berlangsung hanya dalam beberapa detik. Harap pastikan bahwa bisnis Anda memiliki mekanisme koneksi ulang.

## Petunjuk
### Mengatur waktu pemeliharaan
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail instans.
2. Di bagian **Maintenance Info** (Info Pemeliharaan) di halaman detail instans, klik **Modify** (Modifikasi).
![](https://main.qcloudimg.com/raw/141ecd7d3a0ce63ac514aa6c8b4a530f.png)
3. Di kotak jendela pop-up, pilih **Maintenance Window** (Periode Pemeliharaan) dan **Maintenance Time** (Waktu Pemeliharaan) sesuai kebutuhan, lalu klik **OK** (OKE).
![](https://main.qcloudimg.com/raw/d3cdb9e92661e4cdf11bec5861bfb53d.png)

### Peralihan segera
Jika tugas dikonfigurasi untuk dialihkan selama periode pemeliharaan, tetapi Anda harus segera mengalihkannya dalam keadaan khusus, Anda dapat mengklik **Switch Now** (Beralih Sekarang) di kolom **Operation** (Operasi) di [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver).
>?Peralihan langsung berlaku untuk operasi yang melibatkan migrasi data seperti penyesuaian spesifikasi instans, peningkatan versi instans, dan peningkatan kernel instans.
