## Ikhtisar ENI
[Antarmuka Jaringan Elastis (ENI)](https://intl.cloud.tencent.com/document/product/576/18525) merujuk pada tipe antarmuka jaringan virtual yang bisa diikat ke instance CVM di VPC.ENI bisa bebas dimigrasi antara instance CVM dalam VPC dan AZ yang sama, membantu Anda membangun kluster ketersediaan tinggi dengan mudah, mengimplementasikan failover berbiaya rendah, dan mengelola jaringan dengan cara yang lebih baik.
Server asli CLB bisa diikat ke CVM dan ENI.Khususnya, instance CLB berkomunikasi dengan server asli melalui jaringan pribadi, dan jika beberapa instance CVM dan ENI diikat ke instance CLB, lalu lintas akses akan diteruskan ke IP pribadi instance CVM dan ENI.
> Fitur pengikatan ENI CLB sedang dalam pengujian beta.Jika Anda ingin menggunakannya, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=163&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB) untuk mendaftar.

## Prasyarat
ENI harus diikat ke instance CVM terlebih dahulu sebelum bisa diikat ke instance CLB.Karena instance CLB hanya meneruskan lalu lintas sebagai penyeimbang beban, tetapi tidak memproses logika bisnis, instance CVM sebagai sumber daya komputasi diperlukan untuk memproses permintaan pengguna.Silakan masuk ke [Konsol ENI](https://console.cloud.tencent.com/vpc/eni) untuk mengikat ENI yang dibutuhkan ke instance CVM terlebih dahulu.
![](https://main.qcloudimg.com/raw/3d7c79999350a4b80e0a2b2f546b559f.png)

## Petunjuk
1.Anda harus mengonfigurasi pendengar CLB terlebih dahulu.Untuk informasi selengkapnya, silakan lihat [Ikhtisar Pendengar CLB](https://intl.cloud.tencent.com/document/product/214/6151).
2.Klik **+** di sebelah kiri pendengar yang dibuat untuk memperluas nama domain dan jalur URL, pilih jalur URL yang diinginkan, dan tampilkan server asli terikat yang ada di sebelah kanan pendengar.
![](https://main.qcloudimg.com/raw/0c0ed8c9e456cfb52126f34537f0f779.png)
3.Klik **Bind** (Ikat), pilih server asli yang akan diikat dan konfigurasikan port server dan bobot di jendela pop-up.Anda bisa memilih "CVM" atau "ENI" sebagai server asli.
- CVM: Anda bisa mengikat IP pribadi primer dari ENI primer dari semua instance CVM di VPC yang sama sebagai instance CLB.
- ENI: Anda bisa mengikat semua IP ENI di VPC yang sama sebagai instance CLB kecuali IP pribadi primer dari ENI primer dari instance CVM, seperti IP pribadi sekunder dari ENI primer dan IP pribadi dari ENI sekunder.Untuk informasi selengkapnya mengenai tipe-tipe IP ENI, silakan lihat [ENI - Konsep Utama](https://intl.cloud.tencent.com/document/product/576/18526).
![](https://main.qcloudimg.com/raw/89fdb725e535b81361d9a80ab0984e7a.png)
4.Konfigurasi khusus setelah pengikatannya seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/46defc2ad3e445e4acd6808c22aeb937.png)
