
## Skenario
Untuk menciptakan pengalaman pengguna yang lebih baik, aturan alarm dapat dikonfigurasi di Pemantauan Cloud. Alarm segera dipicu saat kondisi alarm yang dikonfigurasi untuk koneksi akselerasi tercapai.

## Petunjuk

Login ke [Konsol Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) sebelum melakukan prosedur berikut.

### Pemantauan koneksi

1. Klik **Alarm Policy** (Kebijakan Alarm) di bilah sisi kiri. Klik **Create** (Buat) untuk masuk ke halaman **Create Alarm Policy** (Buat Kebijakan Alarm).
2. Untuk **Policy Type** (Jenis Kebijakan), pilih **GAAP** > **Channel** (Saluran).
![](https://qcloudimg.tencent-cloud.cn/raw/f951241047178c919b8bfef1a3894133.png)
3. Di bagian **Alarm Policy** (Kebijakan Alarm), tambahkan saluran sesuai kebutuhan untuk **Policy Object** (Objek Kebijakan).
   Anda dapat memilih **Select template** (Pilih templat) atau **Configure manually** (Konfigurasi secara manual) untuk **rigger Condition** (Kondisi pemicu).
   Jika memilih **Select template** (Pilih templat), Anda dapat menggunakan kebijakan alarm yang telah dikonfigurasi sebelumnya. Jika tidak ada templat, Anda dapat membuat dan mengonfigurasi templat baru sebagai berikut. Templat akan disimpan ke konsol untuk penggunaan selanjutnya.
	1. Klik **Add Trigger Condition Template** (Tambahkan Templat Kondisi Pemicu) untuk masuk ke halaman konfigurasi templat.
![](https://qcloudimg.tencent-cloud.cn/raw/121bf297151fd5d14463d2a9f39a5989.png)
	2. Klik **Create** (Buat). Pada jendela pop-up, konfigurasi kondisi pemicu berikut:
		- **Template Name** (Nama Templat): Masukkan nama templat.
		- **Remarks** (Keterangan): Masukkan keterangan templat.
		- **Policy Type** (Jenis Kebijakan): Pilih layanan pemantauan, seperti **GAAP** > **Channel** (Saluran).
		- Gunakan kondisi pemicu prasetel: Pilih opsi ini untuk mengaktifkan kondisi pemicu prasetel untuk produk yang dipantau terkait.
		- Kondisi pemicu: termasuk alarm indikator dan alarm peristiwa. Anda dapat mengeklik **Add** (Tambahkan) untuk mengatur beberapa alarm.
	Jika memilih **Configure manually** (Konfigurasi secara manual), Anda dapat menambahkan beberapa kondisi pemicu alarm sesuai kebutuhan.
![](https://qcloudimg.tencent-cloud.cn/raw/4ce5c2222f27a23a50e29b7d6e675a61.png)
4. Di bagian **Configure Alarm Notification** (Konfigurasi Notifikasi Alarm), klik **Create Template** (Buat Templat), buat nama templat, lalu pilih objek dan saluran penerima.
>!Objek penerima harus diikatkan ke saluran. Jika tidak, Anda tidak akan menerima notifikasi alarm.
>
![](https://qcloudimg.tencent-cloud.cn/raw/96bc43097aed1a331162305ef08a6c61.png)
Klik **Select template** (Pilih templat) untuk memilih templat yang Anda butuhkan.
![](https://qcloudimg.tencent-cloud.cn/raw/4362a734429b1aadce77fd7b219358cb.png)

### Pemantauan pendengar

1. Pilih **Alarm Policy** (Kebijakan Alarm) di bilah sisi kiri. Klik **Create** (Buat) untuk masuk ke halaman **Create Alarm Policy** (Buat Kebijakan Alarm).
2. Untuk **Policy Type** (Jenis Kebijakan), pilih **GAAP** > **L4 Listener Origin Server Status** (Status Server Asal Pendengar L4) /**L7 Listener Origin Server Status** (Status Server Asal Pendengar L7) .
![](https://qcloudimg.tencent-cloud.cn/raw/31a0c004e5b18e3715f4b197791dc20f.png)
3. Pada bagian **Alarm Policy** (Kebijakan Alarm), pilih objek untuk **Policy Object** (Objek Kebijakan), dan pilih **Select template** (Pilih Templat) atau **Configure manual** (Konfigurasi manual) untuk **Trigger Condition** (Kondisi Pemicu). Jika Anda memilih **Configure manually** (Konfigurasi secara manual), Anda dapat mengatur kondisi pemicu untuk memberi tahu Anda bahwa server asal dianggap pengecualian.
![](https://qcloudimg.tencent-cloud.cn/raw/d75fdfe6dc7394fb9bdcdcbd6672915f.png)
4. Di bagian **Configure Alarm Notification** (Konfigurasi Notifikasi Alarm), klik **Create Template** (Buat Templat), buat nama templat, lalu pilih objek dan saluran penerima.
>!Objek penerima harus diikatkan ke saluran. Jika tidak, Anda tidak akan menerima notifikasi alarm.
>
![](https://qcloudimg.tencent-cloud.cn/raw/242dedea0ea3fb500e2c5cbf33ec449e.png)
Klik **Select template** (Pilih templat) untuk memilih templat yang Anda butuhkan.
![](https://qcloudimg.tencent-cloud.cn/raw/16a460eea88e69afbc2a3ca4e97f2d10.png)
