
## Ikhtisar
Dokumen ini menjelaskan cara menskalakan instans secara elastis di konsol TencentDB for Redis untuk lebih mengoptimalkan pemanfaatan sumber daya dan biaya secara real-time.


## Petunjuk
### Menskalakan instans edisi memori dalam arsitektur standar
>!
>- Setelah konfigurasi disesuaikan, instans akan dikenakan harga konfigurasi baru.
>- Untuk memperluas kapasitas instans edisi memori dalam arsitektur standar, jika sisa kapasitas mesin fisik yang tersedia tidak mencukupi, migrasi akan terjadi, yang tidak akan memengaruhi akses Anda ke instans. Namun, jika instans menjalankan Redis 2.8, pemutusan koneksi flash akan terjadi setelah migrasi selesai, jadi sebaiknya bisnis Anda memiliki mekanisme koneksi ulang.
>- Karena kapasitas maksimum instans edisi memori dalam arsitektur standar adalah 64 GB, Anda tidak dapat memperluas kapasitasnya lebih dari 64 GB.
>- Untuk menghindari kegagalan dalam pengurangan kapasitas, kapasitas setelah pengurangan harus minimal 1,3 kali jumlah data yang ada. Setelah pengurangan kapasitas, Anda akan menerima pengembalian dana otomatis.

1. Login ke [Konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), temukan instans yang diinginkan dalam daftar instans, dan pilih **Configure** (Konfigurasi) > **Expand Node** (Perluas Node), **Reduce Node** (Kurangi Node), **Add Replica** (Tambahkan Replika), atau **Delete Replica** (Hapus Replika) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/9b8e7bf10a2848977ee274a3425cfb14.png)
2. Di kotak dialog pop-up, sesuaikan konfigurasi dan klik **OK**.
3. Kembali ke daftar instans. Setelah status instans berubah menjadi "Berjalan", instans dapat digunakan secara normal.


### Menskalakan instans edisi memori dalam arsitektur kluster
>!
>- Setelah konfigurasi disesuaikan, instans akan dikenakan harga konfigurasi baru.
>- Untuk menghindari kegagalan dalam pengurangan kapasitas, kapasitas setelah pengurangan harus minimal 1,3 kali jumlah data yang ada. Setelah pengurangan kapasitas, Anda akan menerima pengembalian dana otomatis.
>- Saat pecahan ditambahkan atau dihapus, sistem akan secara otomatis menyeimbangkan konfigurasi slot dan memigrasikan data, yang mungkin gagal dalam kasus yang jarang terjadi. Disarankan Anda melakukan operasi tersebut selama periode tidak sibutk untuk menghindari dampak migrasi pada akses bisnis.

1. Login ke [Konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), temukan instans yang diinginkan dalam daftar instans, dan pilih **Configure** (Konfigurasi) > **Add Shard** (Tambahkan Pecahan), **Delete Shard** (Hapus Pecahan), **Expand Node** (Perluas Node), **Reduce Node** (Kurangi Node), **Add Replika** (Tambahkan Replika), atau **Delete Replica** (Hapus Replika) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/129b79387c1a469e9b7f9cfcb4e1b1b7.png)
2. Di kotak dialog pop-up, sesuaikan konfigurasi dan klik **OK**.
3. Kembali ke daftar instans. Setelah status instans berubah menjadi "Berjalan", instans dapat digunakan secara normal.

