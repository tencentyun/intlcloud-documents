## Skenario Operasi
TencentDB for SQL Server menyediakan alat pengembalian untuk mengembalikan instans. Data historis dapat dibangun kembali dengan menggunakan cadangan berkala dan transaksi real-time untuk mengembalikan instans ke titik waktu tertentu tempat bagian waktu semua data dijamin identik.
Cadangan data dan log di TencentDB for SQL Server disimpan selama tujuh hari; oleh karena itu, Anda dapat mengembalikan data instans ke titik waktu mana pun dalam tujuh hari terakhir. Dokumen ini menjelaskan cara mengembalikan instans di konsol.

## Petunjuk
1. Login ke [Konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver), klik ID instans untuk masuk ke halaman detail instans, dan klik **Rollback** (Pengembalian) di sudut kanan atas.
2. Di kotak dialog pop-up, pilih database yang akan dikembalikan, atur waktu pengembalian, putuskan apakah akan menimpa database asli, dan klik **Next** (Selanjutnya).
>!
>- Pengembalian saat ini hanya didukung untuk instans yang sama, dan Anda dapat memilih untuk menimpa database asli atau membuat database duplikat.
>- Jika Anda memilih untuk membuat database duplikat, perhatikan bahwa kapasitas disk setelah mengembalikan tidak dapat melebihi kapasitas disk yang tersedia untuk instans; jika tidak, pengembalian akan gagal.
>
![](https://main.qcloudimg.com/raw/917bc0d8782e54948bd4cd16aa24875e.png)
3. Setelah mengonfirmasi bahwa informasi pengembalian sudah benar, klik **Rollback** (Kembalikan) untuk memulai tugas pengembalian.
4. Kembali ke daftar instans tempat Anda dapat melihat bahwa status instans berubah menjadi "Executing task" (Menjalankan tugas). Anda dapat melihat kemajuan pengembalian dalam daftar tugas di sudut kanan atas halaman detail.
![](https://main.qcloudimg.com/raw/f093a8173aba0d90de8214b5806e5cf7.png)
5. Setelah tugas pengembalian berhasil, Anda dapat melihat database yang dihasilkan di tab **Manage Database** (Kelola Database).

