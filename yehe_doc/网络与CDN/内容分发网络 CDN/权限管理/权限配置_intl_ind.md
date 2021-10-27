CDN mengizinkan Anda mengonfigurasi kebijakan kueri dan pengelolaan untuk nama domain dengan granularitas halus. Anda dapat memberikan izin pada tingkat nama domain melalui pernyataan kebijakan khusus.	

>?Karena dukungan untuk CDN API 2.0 telah berakhir, silakan pilih **Create by Policy Generator** (Buat dengan Penghasil Kebijakan) atau **Authorize by Tag** (Izinkan dengan Tag) untuk membuat kebijakan baru. Sebaiknya tidak menggunakan opsi **Create by Product Feature or Project Permission** (Buat dengan Fitur Produk atau Izin Proyek). 

1. Masuk ke [konsol CAM](https://console.cloud.tencent.com/cam/overview) dan klik **Policy** (Kebijakan) untuk masuk ke halaman pengelolaan kebijakan. Klik **Create Custom Policy** (Buat Kebijakan Khusus):
![img](https://main.qcloudimg.com/raw/b986334f0d3acde5eb9526fe01d669bb.png)

2. Pilih **Create by Policy Generator** (Buat dengan Penghasil Kebijakan):
![img](https://main.qcloudimg.com/raw/55a2e3b5b0011b2a8e520df6fc37ff57.png)

3. Pilih **CDN** (CDN) pada daftar turun layanan dan pilih tindakan yang akan diberi izin. Jika Anda ingin memberikan izin baca/tulis penuh, centang **All actions** (Semua tindakan). Untuk menautkan tindakan tertentu dengan fitur konsol, silakan lihat [Izin Konsol](https://intl.cloud.tencent.com/document/product/228/35229).
![img](https://main.qcloudimg.com/raw/43b88d53d2beb2b2c167a4a732dc6ded.png)

4. Masukkan nama domain yang akan diberi izin sebagai sumber daya:
	- Untuk semua nama domain: centang **All resources** (Semua sumber daya) dan klik **Confirm** (Konfirmasikan).

	- Untuk nama domain tertentu: centang **Specific Resource** (Sumber Daya Tertentu) dan klik **Add a 6-segment resource description** (Tambahkan uraian sumber daya 6 segmen).

	Pada jendela pop-up di sebelah kanan, masukkan nama domain dan klik **Confirm** (Konfirmasikan). Anda dapat mengulangi operasi tersebut untuk menambahkan banyak nama domain.


5. Setelah konfigurasi selesai, klik **Confirm** (Konfirmasikan) dan **Next** (Selanjutnya). Hubungkan kebijakan yang dibuat dengan pengguna atau kelompok pengguna yang sudah ada, dan terakhir klik **Done** (Selesai) untuk memberikan izin.

