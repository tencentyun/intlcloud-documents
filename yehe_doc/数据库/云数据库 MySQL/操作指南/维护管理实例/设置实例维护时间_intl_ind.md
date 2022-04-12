## Ikhtisar
Jendela pemeliharaan adalah konsep yang sangat penting untuk TencentDB for MySQL. Untuk memastikan stabilitas instans TencentDB for MySQL, sistem backend melakukan operasi pemeliharaan pada instans selama periode pemeliharaan dari waktu ke waktu. Sebaiknya tetapkan periode pemeliharaan yang dapat diterima untuk instans Anda, biasanya selama jam normal, untuk meminimalkan potensi dampak pada bisnis Anda.

Selain itu, sebaiknya operasi juga melakukan migrasi data selama jendela pemeliharaan, seperti penyesuaian spesifikasi instans, peningkatan versi instans, dan peningkatan kernel instans. Saat ini, jendela pemeliharaan didukung oleh instans sumber, replika baca saja, dan instans pemulihan bencana.

Mengambil peningkatan spesifikasi instans database sebagai contoh, karena operasi ini melibatkan migrasi data, setelah peningkatan selesai, pemutusan sementara dari database dapat terjadi. Saat peningkatan dimulai, **Switch Time** (Waktu Peralihan) dapat dipilih sebagai **During maintenance time** (Selama waktu pemeliharaan), sehingga peralihan spesifikasi instans akan diaktifkan dalam **maintenance window** (periode perawatan) berikutnya setelah peningkatan instans selesai. Perlu diketahui bahwa ketika Anda melakukannya, peralihan tidak akan terjadi segera setelah peningkatan spesifikasi database selesai; sebagai gantinya, sinkronisasi akan berlanjut hingga instans memasuki **maintenance window** (jendela pemeliharaan) berikutnya saat peralihan akan dilakukan. Dengan cara ini, keseluruhan waktu yang diperlukan untuk meningkatkan instans dapat diperpanjang.

>?
>- Sebelum pemeliharaan dilakukan untuk TencentDB for MySQL, pemberitahuan akan dikirimkan ke kontak yang telah dikonfigurasi di akun Tencent Cloud Anda melalui SMS dan email.
>- Peralihan instans disertai dengan pemutusan dari database yang berlangsung hanya dalam beberapa detik. Harap pastikan bahwa bisnis Anda memiliki mekanisme koneksi ulang.

## Petunjuk
### Mengatur periode pemeliharaan
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail instans.
2. Di bagian **Maintenance Info** (Info Pemeliharaan), klik **Modify** (Modifikasi).
![](https://main.qcloudimg.com/raw/388e3aa6ca18c6cb947eb4d053ad1eb5.png)
3. Di kotak dialog pop-up, pilih **Maintenance Window** (Jendela Pemeliharaan) dan **Maintenance Time** (Waktu Pemeliharaan), lalu klik **OK** (OKE).
![](https://qcloudimg.tencent-cloud.cn/raw/91738d5593aad8f573fde932420ae9fe.png)

<span id="lijiqiehuan"></span>
### Melakukan peralihan langsung
Jika tugas dikonfigurasi untuk dialihkan selama masa pemeliharaan, tetapi Anda harus segera mengalihkannya dalam keadaan khusus, Anda dapat mengklik **Switch Now** (Beralih Sekarang) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/fd9780d4f9e1d8094bcb82f215deb366.png)

>?
>- Peralihan langsung berlaku untuk operasi yang melibatkan migrasi data seperti penyesuaian spesifikasi instans, peningkatan versi instans, dan peningkatan kernel instans.
>- Untuk peningkatan versi, jika dikaitkan dengan beberapa instans, peralihan akan dilakukan dalam urutan dari replika baca saja ke instans sumber.
