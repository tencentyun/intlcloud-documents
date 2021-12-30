Setelah dibuat, tabel rute perlu dihubungkan ke subnet untuk mengontrol lalu lintas keluar dari subnet. Dokumen ini menjelaskan cara menghubungkan tabel rute dengan atau memisahkannya dari subnet.

## Menghubungkan ke Subnet
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih **Rute Tables** (Tabel Rute) di bilah sisi kiri untuk membuka halaman pengelolaan.
3. Ada dua metode untuk menghubungkan ke subnet:
 + Dalam daftar, pilih tabel rute yang perlu dihubungkan ke subnet, dan klik **More** (Lainnya)> **Associated Subnet** (Subnet Terhubung) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/0e8f63501b1a2c8c8c99d4f9d838b4e3.png)
 + Klik ID tabel rute untuk membuka halaman detail, pilih tab **Associated Subnet** (Subnet Terhubung), dan klik **+Associate Subnet** (+Hubungkan Subnet).
![](https://main.qcloudimg.com/raw/6e814d4f11035afba7f35100ef4bcde6.png)
4. Di jendela pop-up, pilih subnet yang akan dihubungkan (tabel rute dapat dihubungkan ke beberapa subnet secara bersamaan, dan Anda dapat memfilter menurut ID/nama subnet dengan cepat). Harap evaluasi dampak bisnis dari koneksi ke subnet. Konfirmasi dampaknya, dan klik **OK** (OKE).
>!Setelah tabel rute dihubungkan ke subnet, tabel rute asli yang terhubung ke subnet akan diganti dengan yang baru, dan lalu lintas keluar subnet akan dijalankan sesuai dengan kebijakan di tabel rute baru. Harap evaluasi dampak bisnis dengan cermat.
  >


## Pemutusan Koneksi dari Subnet
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih **Rute Tables** (Tabel Rute) di bilah sisi kiri untuk membuka halaman pengelolaan.
3. Klik ID tabel rute untuk membuka halaman detail, beralih ke tab **Associated Subnet** (Subnet Terhubung), dan klik **Disassociate** (Putuskan Koneksi).
![](https://main.qcloudimg.com/raw/077e50e31696c2f9733d3e7030a8e709.png)
4. Di jendela pop-up, pilih tabel rute baru untuk subnet yang akan dipisahkan, dan klik **OK** (OKE) untuk menyelesaikan pemutusan koneksi tabel rute saat ini dari subnet. Kebijakan lalu lintas keluar subnet akan dijalankan berdasarkan tabel rute baru yang dipilih untuknya.

