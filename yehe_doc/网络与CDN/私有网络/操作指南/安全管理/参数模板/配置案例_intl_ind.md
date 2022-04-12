## Kasus Penggunaan Templat Parameter
Templat parameter adalah cara yang efisien, cepat, dan mudah dipelihara untuk menambahkan aturan dalam grup keamanan. Misalnya, saat Anda perlu menambahkan beberapa rentang IP, IP yang telah ditentukan, atau port protokol dari beberapa jenis, Anda dapat menentukan templat parameter. Anda juga dapat menggunakan templat parameter selanjutnya untuk mempertahankan sumber IP dan port protokol dalam aturan grup keamanan.
>?Semua alamat IP dan port protokol dalam dokumen ini adalah contoh. Harap ganti sesuai kondisi bisnis aktual Anda selama konfigurasi.
>


## Deskripsi Contoh
Misalnya Anda ingin mengonfigurasi aturan grup keamanan berikut dan nantinya perlu memperbarui rentang IP sumber masuk dan port protokol:
+ Aturan masuk:
 + Rentang IP sumber yang diizinkan: 10.0.0.16-10.0.0.30; port protokol: TCP:80,443
 + Blok CIDR sumber yang diizinkan: 192.168.3.0/24; port protokol: TCP:3600-15000

+ Aturan keluar:
 Alamat IP target yang ditolak: 192.168.10.4; port protokol: TCP:800


## Solusi
Karena Anda memiliki kebijakan grup keamanan yang sama untuk beberapa rentang IP dan port protokol, dan Anda nantinya perlu memperbarui rentang IP sumber, Anda dapat menggunakan templat parameter untuk menerapkan penambahan dan pemeliharaan aturan grup keamanan.



### Langkah 1. Buat templat parameter
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih **Security** (Keamanan) > **Parameter Template** (Templat Parameter) di bilah sisi kiri untuk mengakses halaman manajemen.
3. Pada tab **IP Address** (Alamat IP), klik **+ New** (+Baru) guna membuat templat parameter alamat IP untuk menambahkan aturan masuk dan keluar.
4. Di jendela pop-up, masukkan rentang IP sumber dan klik **Submit** (Kirim).</br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/581bf5c79ec186d05290c8ab73138338.png" width="45%" />
</br>
Templat parameter alamat IP yang baru dibuat adalah seperti yang ditunjukkan di bawah.
<img src="https://qcloudimg.tencent-cloud.cn/raw/67f474a18a1f4cca9001995700d80559.png" >
5. Pada tab **Protocol Port** (Port Protokol), klik **+ New** (+Baru) untuk membuat templat parameter port protokol guna menambahkan aturan masuk dan keluar.
<img src="https://qcloudimg.tencent-cloud.cn/raw/fa453b19c81e823dee3afc0e5b473d72.png" width="45%" /> 
</br>
Templat parameter port protokol yang baru dibuat adalah seperti yang ditunjukkan di bawah:
<img src="https://qcloudimg.tencent-cloud.cn/raw/9ce16cdc7fdbeec0f3117ca4c8e3a863.png" >

### Langkah 2. Menambahkan aturan grup keamanan
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih **Security** (Keamanan) > **Security Group** (Grup Keamanan) di bilah sisi kiri untuk mengakses halaman manajemen.
3. Dalam daftar, temukan grup keamanan yang perlu mengimpor templat parameter dan klik ID-nya untuk masuk ke halaman detail.
4. Pada halaman tab **Inbound Rules or Outbound Rules** (Aturan Masuk atau Aturan Keluar), klik **Add Rules** (Tambahkan Aturan).
5. Di jendela pop-up, pilih jenis kustom, pilih templat parameter alamat IP yang sesuai untuk sumber/target, pilih templat parameter port protokol yang sesuai untuk port protokol tersebut, dan klik **Complete** (Selesai).
![](https://qcloudimg.tencent-cloud.cn/raw/9039d1de4a8a2891873faaec92627fee.png)

	
### Langkah 3. Memperbarui templat parameter
Misalkan Anda perlu menambahkan aturan masuk dengan sumber IP sebagai rentang IP `10.0.1.0/27` dan port protokol menjadi `UDP:58`. Anda dapat langsung memperbarui templat parameter alamat IP `ipm-0ge3ob8e` dan port protokol `ppm-4ty1ck3i`.
1. Pada tab **IP Address** (Alamat IP) templat parameter, cari templat parameter `ipm-0ge3ob8e`.
2. Klik **Edit** (Edit) di sebelah kanan.
![](https://qcloudimg.tencent-cloud.cn/raw/f7f28bf7fdb77f25c6c1e2fbf5555809.png)
3. Di jendela pop-up, tambahkan rentang IP `10.0.1.0/27` di baris baru dan klik **Submit** (Kirim).
<img src="https://qcloudimg.tencent-cloud.cn/raw/0be07de1ae0e9858ec94327cb0b3ba75.png" width="45%" />
4. Pada tab **Protocol Port** (Port Protokol) pada templat parameter, cari templat parameter `ppm-4ty1ck3i`.
5. Klik **Edit** (Edit) di sebelah kanan.
![](https://qcloudimg.tencent-cloud.cn/raw/9ba28cdac71dbded7259eee9e74d128a.png)
6. Di jendela pop-up, tambahkan port protokol masuk `UDP:58` di baris baru dan klik **Submit** (Kirim).</br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/b4f15b9ef711caae75920b2f70780667.png" width="45%" />
