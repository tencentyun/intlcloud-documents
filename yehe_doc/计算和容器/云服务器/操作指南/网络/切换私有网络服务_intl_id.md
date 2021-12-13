## Ikhtisar

Tencent Cloud menyediakan jaringan klasik dan VPC untuk berbagai skenario. Berbagai fitur ditawarkan untuk membantu Anda mengelola jaringan secara fleksibel.
- Beralih antar jaringan:
 - **Switching from the classic network to VPC** (Beralih dari jaringan klasik ke VPC): Tencent Cloud memungkinkan Anda memigrasikan satu atau beberapa instans CVM dari jaringan klasik ke VPC sekaligus.
 - **Switching between VPCs** (Beralih antara VPC): Tencent Cloud memungkinkan Anda memigrasikan satu atau beberapa instans CVM dari VPC A ke VPC B sekaligus.
- Menentukan alamat IP kustom.
- Memilih untuk mempertahankan HostName.

## Prasyarat
- Sebelum migrasi, lepas ikatan instans CVM dari CLB dan ENI di jaringan pribadi dan publik dan lepaskan alamat IP sekunder dari ENI primer. Ikat ulang instans setelah migrasi.


## Petunjuk
### Menentukan atribut jaringan dari instans CVM
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Di halaman **Instances** (Instans), temukan instans target yang ingin Anda migrasikan.
Instans ada di jaringan klasik jika “Jaringan: Jaringan Klasik” muncul di kolom **Instance Configuration** (Konfigurasi Instans), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/bb54a50bd8a42e5aeac6ce02bc3c6a4d.png)
>!
>- Migrasi dari jaringan klasik ke VPC TIDAK DAPAT dikembalikan. Setelah migrasi, instans CVM tidak akan dapat berkomunikasi dengan layanan Tencent Cloud di jaringan klasik.
>- Setelah Anda menentukan atribut jaringan instans CVM, Anda dapat [memigrasikan instans ke VPC](#changeVPC) sesuai kebutuhan.




### Memigrasikan ke VPC<span id="changeVPC"></span>
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Di halaman **Instances** (Instans), migrasikan instans target ke VPC.
	- **Method 1** (Metode 1): untuk memigrasikan instans ke VPC, cari dan pilih **More** (Lainnya) -> **Resource Adjustment** (Penyesuaian Sumber Daya) -> **Switch VPC** (Beralih VPC) di kolom **Operation** (Operasi).
	![](https://main.qcloudimg.com/raw/e688912e2ad9ea46ce7027f17e1a8045.png)
	- **Method 2** (Metode 2): untuk mengelompokkan instans ke VPC, pilih instans target, lalu klik **More Actions** (Tindakan Lainnya) -> **Resource Adjustment** (Penyesuaian Sumber Daya) -> **Switch VPC** (Beralih VPC) di bagian atas daftar instans.
	>! Migrasi massal hanya didukung untuk instans CVM di zona ketersediaan yang sama.
	>
	![](https://main.qcloudimg.com/raw/b15f3e4e6c212ff496d38c3753c9a4da.png)
3. Di jendela **Switch VPC** (Beralih VPC) yang muncul, baca catatannya, lalu klik **Next** (Selanjutnya).
4. Pilih VPC tujuan dan subnet yang sesuai, lalu klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/acaca8c4343d8e5357bd33b75f1f5f68.png)
5. Tentukan alamat IP yang telah ditetapkan sebelumnya dan opsi HostName untuk **Set IP** (Menetapkan IP) sesuai kebutuhan, lalu klik **Next** (Selanjutnya).
>? 
> - Jika tidak ada alamat IP yang ditentukan sebelumnya, sistem akan secara otomatis menetapkan alamat IP.
> - Saat menentukan opsi HostName, Anda dapat memilih **Reset HostName** (Atur ulang HostName) atau **Retain the original HostName of the instance** (Pertahankan HostName instans asli).
> 
![](https://main.qcloudimg.com/raw/c3908fef18c46a5f88aebfca2204f5c0.png)
6. Lakukan operasi sesuai petunjuk di halaman **Shutdown CVM** (Mematikan CVM), lalu klik **Start Migration** (Mulai Migrasi). Setelah migrasi selesai, Anda dapat login ke konsol CVM. Pada halaman **Instances** (Instans), Anda akan melihat bahwa **Modifying instance VPC attributes** (Memodifikasi atribut VPC instans) ditampilkan di kolom **Status** (Status) dari instans yang dimigrasikan.
>!
>- Selama migrasi, instans CVM perlu dimulai ulang. Dengan demikian, jangan melakukan operasi lain selama waktu ini.
>- Periksa status instans setelah migrasi dan verifikasi apakah akses jaringan pribadi dan login jarak jauh berfungsi dengan baik.
>
![](https://main.qcloudimg.com/raw/759d34a61cc6b0d1e430525e3283d43b.png)




