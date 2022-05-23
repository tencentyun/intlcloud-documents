
## Ikhtisar
TencentDB for Redis mendukung [pemisahan baca/tulis](https://intl.cloud.tencent.com/document/product/239/33132) untuk skenario bisnis dengan lebih banyak pembacaan tetapi lebih sedikit penulisan, yang dapat mengatasi permintaan baca yang berkonsentrasi pada data yang sering dibaca dengan baik. Mendukung hingga mode 1-master 5-replika untuk menawarkan performa baca 5x.
>!
>- Mengaktifkan pemisahan baca/tulis dapat menyebabkan inkonsistensi pembacaan data (data pada node replika lebih lama dari pada node master). Oleh karena itu, silakan periksa apakah bisnis Anda dapat mentolerir inkonsistensi data terlebih dahulu.
>- Menonaktifkan pemisahan baca/tulis dapat mengganggu koneksi yang ada untuk sementara, jadi Anda disarankan untuk melakukannya di luar jam sibuk.

## Petunjuk
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis) dan klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Node Management** (Manajemen Node) dan klik **Read-Only Replica** (Replika Baca Saja) di sudut kanan atas untuk mengaktifkan pemisahan baca/tulis.
![](https://main.qcloudimg.com/raw/1d66625e3868fa6850648bd1737f7435.png)
3. Di jendela pop-up, pilih **Master Node** (Node Master) dan/atau **Replica Node** (Node Replika). Jika Anda memilih **Master Node** (Node Master), tombol **Read-Only Replica** (Replika Baca Saja) akan diaktifkan.
![](https://qcloudimg.tencent-cloud.cn/raw/518ee9eda54a17fa431dfc419cc2a899.png)
4. Setelah mengonfirmasi bahwa semuanya sudah benar, klik **OK**.
