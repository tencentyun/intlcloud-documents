Setiap subnet harus dihubungkan dengan satu [tabel rute](https://intl.cloud.tencent.com/document/product/215/31810), yang digunakan untuk mengontrol arah lalu lintas keluar subnet. Anda dapat mengubah tabel rute terkait Subnet di halaman **VPC -> Subnet** sesuai dengan kebutuhan perutean subnet. Jika Anda perlu membuat tabel rute, harap lihat [Membuat Tabel Rute Kustom](https://intl.cloud.tencent.com/document/product/215/35236).

## Dampak sistem
Mempertimbangkan bahwa tabel rute berdampak langsung pada arus lalu lintas di subnet, setiap perubahan seperti hubungan tabel rute atau entri rute harus dipertimbangkan dengan cermat sesuai dengan kebutuhan bisnis aliran jaringan.

## Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih **Subnet** (Subnet) di bilah sisi kiri untuk membuka halaman pengelolaan subnet.
3. Sistem menyediakan dua metode untuk mengubah tabel rute yang terhubung dengan subnet.
    + Klik **More** > **Change Route Table** (Lainnya > Ubah Tabel Rute) di kolom **Operation** (Operasi) di sisi kanan subnet yang perlu mengubah tabel rute.
       ![](https://main.qcloudimg.com/raw/154c5a6ff6b746a1a593fc4ac6a5ece9.png)
	+ Klik ID subnet yang perlu diubah tabel rutenya untuk membuka halaman detail, beralih ke tab **Routing Rules** (Aturan Rute), dan klik **Change Route Table** (Ubah Tabel Rute).
	   ![](https://main.qcloudimg.com/raw/572762da3d2163b3c30ed07c8a167130.png)
4. Di jendela pop-up, pilih tabel rute baru di daftar pilihan, konfirmasi dampaknya terhadap bisnis Anda, dan klik **Confirm** (Konfirmasi).
![](https://main.qcloudimg.com/raw/c51606ba642517ffc01bcbf666abab49.png)
