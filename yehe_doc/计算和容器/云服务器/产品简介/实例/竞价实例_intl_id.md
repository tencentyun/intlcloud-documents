## Apa yang dimaksud dengan instans spot?
Instans spot adalah mode instans CVM baru yang menampilkan harga diskon dan mekanisme gangguan sistem, yang berarti Anda dapat membeli instans spot dengan harga diskon, tetapi sistem dapat mengambil alih instans tersebut secara otomatis. Saat menggunakan instans spot, operasinya hampir sama dengan yang Anda lakukan dengan instans CVM yaitu bayar sesuai pemakaian, termasuk operasi konsol, masuk jarak jauh, deployment layanan, dan asosiasi dengan VPC.

- Referensi: [Pertanyaan Umum > Tentang Instans > Instans Spot](https://intl.cloud.tencent.com/document/product/213/17817)
- Referensi: [Instans Spot](https://intl.cloud.tencent.com/document/product/213/17926)

## Kebijakan khusus untuk tahap saat ini
- **Diskon tetap**: Semua instans spot tersedia dengan diskon tetap, yaitu diskon 80% dari harga instans bayar sesuai pemakaian dengan spesifikasi yang sama. Diskon untuk beberapa jenis instans mungkin sedikit disesuaikan.
- **Gangguan sistem karena pasokan tidak mencukupi**: Saat ini, instans spot tidak akan terganggu karena alasan harga, yaitu harga pasar lebih tinggi dari tawaran Anda, tetapi dapat terganggu jika instans spot kekurangan pasokan. Jika persediaan tidak mencukupi, Tencent Cloud akan secara acak mengambil alih instans spot yang dialokasikan.
- **Tersedia hampir di semua wilayah**: Instans spot tersedia hampir di semua wilayah Tencent Cloud. Jenis instans yang didukung oleh instans spot sama dengan yang didukung oleh instans bayar sesuai pemakaian. Untuk wilayah terbaru dan jenis instans yang didukung, lihat [Instans Spot - Wilayah dan jenis instans yang didukung >>](https://intl.cloud.tencent.com/document/product/213/17817).

## Fitur Produk
### 1. Efektivitas biaya
![](https://main.qcloudimg.com/raw/8179ef6629ac0a0b4b9c3c9cd6f80ffa.png)
Instans spot dijual dengan diskon hingga 90% dari harga instans bayar sesuai pemakaian.
- **Rentang diskon**: Instans spot dijual dengan diskon hingga 90% dari harga instans bayar sesuai pemakaian dengan spesifikasi yang sama.
- **Pengecualian**: Diskon hanya berlaku untuk memori dan CPU CVM. Item penagihan terkait CVM lainnya termasuk disk sistem, disk data, bandwidth, dan citra berbayar tidak memenuhi syarat untuk mendapatkan diskon.
- **Fluktuasi harga**: Diskon stabil untuk jangka waktu tertentu. Namun, jika ada pembelian massal di zona ketersediaan, harganya mungkin akan mengalami fluktuasi. Saat ini, diskonnya tetap sebesar 80%.

### 2. Mekanisme gangguan sistem
![](https://main.qcloudimg.com/raw/a4db964d52400b9a00d3c7e96c0b833d.png)
Tidak seperti instans bayar sesuai pemakaian yang hanya dapat dirilis oleh pengguna, instans spot dapat terganggu oleh sistem karena alasan harga atau ketersediaan sumber daya.
![](https://main.qcloudimg.com/raw/824a585f8dfeb1914f4d72ea1eafdb6c.png)
- **Harga**: Jika harga pasar lebih tinggi dari tawaran tertinggi Anda, instans spot Anda akan diambil alih. Namun, pada tahap ini, harga pasar akan tetap.
- **Ketersediaan sumber daya**: Jika instans spot kekurangan pasokan, Tencent Cloud akan mengambil alih instans spot berdasarkan kekurangannya. Setelah persediaan mencukupi, Anda dapat mengajukan permohonan instans spot lagi.

## Skenario yang tidak dapat diterapkan
Karena instans spot mungkin terganggu, siklus prosesnya tidak di bawah kendali Anda. Oleh karena itu, sebaiknya jangan menjalankan layanan dengan persyaratan stabilitas tinggi pada instans spot. Misalnya:
- Layanan database
- Layanan online dan situs web tanpa load balancer
- Node kontrol inti dalam arsitektur terdistribusi
- Pekerjaan komputasi big data berkepanjangan yang berlangsung lebih dari 10 jam

## Skenario dan industri yang berlaku
### Skenario yang berlaku
- Komputasi big data
- Layanan online dan situs web dengan load balancer
- Layanan crawler web
- Skenario komputasi lainnya dengan tingkat perincian mendalam atau dukungan untuk mulai ulang checkpoint

### Industri yang berlaku
- Pengurutan dan analisis gen
- Analisis bentuk kristal obat
- Video transcoding dan rendering
- Analisis data keuangan dan transaksi
- Pemrosesan citra dan multimedia
- Perhitungan sains, seperti dalam geografi dan hidromekanik

## Pembatasan
- **Kuota**: Kuota instans spot membatasi jumlah total inti vCPU dari semua instans spot yang Anda miliki di zona ketersediaan. Saat ini, setiap akun dapat memiliki hingga 50 inti vCPU di setiap zona ketersediaan. Untuk mendapatkan kuota yang lebih tinggi, kirimkan tiket.
- **Pembatasan operasi 1**: Peningkatan dan penurunan konfigurasi tidak didukung untuk instans spot.
- **Pembatasan operasi 2**: Anda tidak dapat mengalihkan metode penagihan instans spot ke langganan bulanan.
- **Pembatasan operasi 3**: instans spot tidak mendukung fitur "Tanpa Biaya saat Dinonaktifkan".
- **Pembatasan operasi 4**: instans spot tidak mendukung penginstalan ulang sistem.

## Praktik Terbaik
### 1. Membagi tugas
- Bagi tugas yang berkepanjangan menjadi subtugas mendetail untuk mendapatkan kemungkinan gangguan yang lebih rendah.
- Gunakan rangkaian big data seperti EMR yang dilengkapi dengan mekanisme pembagian.

### 2. Menggunakan load balancer untuk memastikan stabilitas layanan online dan situs web
- Gunakan load balancer, seperti CLB, pada lapisan akses.
- Gunakan kombinasi beberapa instans bayar sesuai pemakaian dan banyak instans spot untuk sumber daya backend.
- Pantau gangguan instans spot dan hapus instans yang akan mengalami gangguan dari CLB.

### 3. Menggunakan mode penjadwalan komputasi yang mendukung mulai ulang checkpoint
- Simpan hasil komputasi menengah pada produk penyimpanan permanen seperti COS, CFS, dan NAS.
- Pantau instans mana yang akan mengalami gangguan menggunakan metadata dan simpan hasil komputasi dalam periode retensi selama 2 menit.
- Lanjutkan komputasi terakhir saat instans spot dimulai lagi.
