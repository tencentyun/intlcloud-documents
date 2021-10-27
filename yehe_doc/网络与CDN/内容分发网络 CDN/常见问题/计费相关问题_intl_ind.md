### Bisakah CDN ditagih berdasarkan jumlah permintaan?
Tidak. Saat ini, CDN tidak mendukung penagihan berdasarkan jumlah permintaan.

### Apa yang akan terjadi jika saldo akun saya menjadi negatif?
Untuk informasi selengkapnya, silakan lihat [pembayaran terlambat](https://intl.cloud.tencent.com/document/product/228/2949#.E6.AC.A0.E8.B4.B9.E8.AF.B4.E6.98.8E) pada dokumen uraian penagihan.

### Jika server asal menggunakan COS, apakah saya akan ditagih menurut lalu lintas yang dihasilkan oleh tarik-asal dari CDN ke COS?
Tidak. Lalu lintas yang dihasilkan oleh tarik-asal dari CDN ke COS ditagih berdasarkan COS, bukan CDN.Untuk informasi selengkapnya, silakan lihat [COS sebagai Server Asal](https://intl.cloud.tencent.com/document/product/228/32977).

### Jika dimatikan (atau dinonaktifkan), apakah CDN akan menghasilkan lalu lintas dan memakan biaya?
Setelah layanan akselerasi nama domain CDN dimatikan, jika nama domain masih dikonfigurasi dengan CNAME, kode status 404 akan dikembalikan untuk permintaan yang telah diselesaikan ke simpul dan sejumlah kecil lalu lintas akan digunakan.Konsol akan merekam data lalu lintas ini sebagai pedoman Anda.Log yang sesuai juga akan dihasilkan.Namun, karena nama domain Anda telah dimatikan, Anda tidak akan ditagih atas penggunaan lalu lintas dan paket log ini.Kami sarankan Anda mengubah resolusi tarik-asal terlebih dahulu sebelum mematikan layanan akselerasi tersebut.

### Bagaimana saya mengubah cara penagihan CDN?

Jika Anda merasa cara penagihan yang dipilih tidak cocok untuk kondisi bisnis Anda yang sebenarnya (untuk informasi selengkapnya tentang bagaimana memilih cara penagihan yang tepat bagi Anda, silakan lihat [Memilih Rencana Penagihan](https://intl.cloud.tencent.com/document/product/228/2949#.E8.AE.A1.E8.B4.B9.E6.96.B9.E5.BC.8F.E9.80.89.E6.8B.A9)), Anda dapat mengubahnya dengan mengikuti prosedur di bawah ini:
1.Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), lihat halaman ikhtisar layanan, lalu klik **Change** (Ubah) di bagian cara penagihan di sebelah kanan.
![](https://main.qcloudimg.com/raw/38b82d3d166970552437b5525b74c44f.png)
2.Ubah cara penagihan sebelumnya **Bill by Traffic** (Tagih sesuai Lalu Lintas) menjadi **Bill by Bandwidth** (Tagih sesuai Bandwidth).
![](https://main.qcloudimg.com/raw/6fd1575557d0c4b7b06be9f1fc30e1da.png)
3.Setelah Anda mengubah cara penagihan menjadi **Bill by Bandwidth** (Tagih sesuai Bandwidth), biaya untuk total penggunaan yang dihasilkan pada tanggal saat itu akan ditagih dan dipotong pada hari berikutnya:

### Jika server asal menggunakan CVM, apakah saya akan ditagih atas lalu lintas yang dihasilkan oleh tarik-asal dari CDN ke CVM?

Tidak. CDN tidak menagih bayaran atas jenis lalu lintas ini.

### Berapa tingkat konversi dari Gbps ke Mbps dalam tagihan CDN?

Dalam tagihan CDN, 1 Gbps = 1000 Mbps, 1 Mbps = 1000 Kbps, dan 1 Kbps = 1000 bps.

### Apakah hanya lalu lintas downstream yang dapat ditagih di CDN?

Ya.CDN hanya menagih bayaran untuk lalu lintas downstream, bukan lalu lintas upstream.


### Apakah ada penundaan dalam menggunakan API untuk mengueri data?Berapa lama penundaan tersebut?
Ada penundaan tertentu dalam menggunakan API untuk mengueri data.Kueri data real-time, seperti data akses dan data penagihan, mengalami penundaan sekitar 5–10 menit, sedangkan kueri data analitik, seperti peringkat, akan mengalami penundaan sekitar setengah jam.Data tersebut dikalibrasi di backend sekitar pukul 3 pagi Waktu Beijing.
