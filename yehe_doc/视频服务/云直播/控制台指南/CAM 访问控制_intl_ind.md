CSS mendukung kontrol izin melalui CAM, tempat Anda dapat mengelola nama domain CSS, konfigurasi, dan data akun Anda. Anda dapat membuat, mengelola, atau menghentikan pengguna atau grup pengguna dan memberikan izin akses API kepada pengguna atau grup pengguna tersebut untuk tujuan pengelolaan identitas dan kontrol kebijakan.

Anda dapat menggunakan CAM untuk mengikat pengguna atau grup pengguna ke kebijakan yang mengizinkan atau menolak mereka mengakses sumber daya tertentu untuk menyelesaikan tugas tertentu.

## Konsep

- Akun root: akun Tencent Cloud terdaftar.
- Sub-pengguna: dibuat dan dimiliki sepenuhnya oleh akun root.
- Kolaborator: setelah akun ditambahkan sebagai kolaborator akun root, akun tersebut menjadi salah satu sub-akun dari akun root dan memiliki identitas akun root.
- Grup pengguna: dibuat untuk pengguna dengan fungsi yang sama dan dapat diikatkan dengan kebijakan untuk manajemen otorisasi terpusat.

Informasi selengkapnya tentang definisi dan izin dapat dilihat di CAM [User Types (Jenis Pengguna)](https://intl.cloud.tencent.com/document/product/598/32633).

## Petunjuk
### Langkah 1. Buat sub-pengguna atau grup pengguna

Satu atau beberapa sub-pengguna dengan peran dan kebijakan tertentu dapat dibuat untuk satu akun root. Sub-pengguna memiliki ID unik dan kredensial identitas yang dapat digunakan untuk login ke konsol Tencent Cloud untuk konfigurasi. Sub-pengguna juga memiliki izin akses API. Anda dapat login ke [konsol CAM](https://console.cloud.tencent.com/cam/) untuk membuat sub-pengguna, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/c1c92bdd08c8cf19ac17ba80cd4a11be.png)
Informasi selengkapnya dapat dilihat di [Creating Sub-user (Membuat Sub-pengguna)](https://intl.cloud.tencent.com/document/product/598/13674) dan [Creating User Group (Membuat Grup Pengguna)](https://intl.cloud.tencent.com/document/product/598/33380).

### Langkah 2. Menambahkan kebijakan ke sub-pengguna atau grup pengguna

Anda dapat menambahkan kebijakan dan memberikan izin kepada pengguna atau grup pengguna di halaman manajemen pengguna atau grup pengguna dan manajemen kebijakan. Informasi selengkapnya dapat dilihat di [Authorization Management (Manajemen Otorisasi)](https://intl.cloud.tencent.com/document/product/598/10602).

<dx-tabs>
::: Metode 1. Menambahkan kebijakan ke sub-pengguna atau grup pengguna
Masuk ke halaman pengguna/grup pengguna, lalu pilih pengguna/grup pengguna tempat kebijakan akan ditambahkan.
- Klik **Users** > **User List** (Pengguna > Daftar Pengguna) di bilah sisi kiri, pilih pengguna/grup pengguna tempat kebijakan akan ditambahkan, klik **Authorize** (Berikan Izin) di sebelah kanan, pilih kebijakan CSS yang sesuai, lalu klik **Confirm** (Konfirmasi). ![](https://main.qcloudimg.com/raw/9da12095cfa57813a373ab9ffeabc9a4.png)

  

  ![](https://main.qcloudimg.com/raw/f09b5d456ba1fd554ad321ddcc67cbdc.png)

- Klik **Users** > **User List** (Pengguna > Daftar Pengguna) atau **User Groups** (Grup Pengguna) di bilah sisi kiri, klik nama pengguna/grup pengguna tempat kebijakan akan ditambahkan untuk masuk ke halaman detail, klik **Associate Policy** (Kaitkan Kebijakan), pilih kebijakan CSS yang sesuai, dan klik **Confirm** (Konfirmasi).
![](https://main.qcloudimg.com/raw/f09b5d456ba1fd554ad321ddcc67cbdc.png)
:::
::: Metode 2. Mengaitkan kebijakan dengan pengguna/grup pengguna
Klik **Policies** (Kebijakan) di bilah sisi kiri, pilih kebijakan yang akan ditambahkan, klik **Associate Users/Groups** (Kaitkan Pengguna/Grup) di kolom **Operation** (Operasi), pilih pengguna/grup pengguna yang akan diberi izin, lalu klik **Confirm** (Konfirmasi).
![](https://main.qcloudimg.com/raw/5b5e0dc032934846e39e7aee740ae34b.png)

:::
</dx-tabs>

#### Kebijakan yang dapat ditambahkan
- **Preset policy** (Kebijakan prasetel): klik **Policies** (Kebijakan) di bilah sisi kiri untuk masuk ke halaman **Policies** (Kebijakan), tempat Anda dapat melihat semua kebijakan yang ada.
   - Kebijakan prasetel CSS mencakup [QcloudLIVEFullAccess](https://console.cloud.tencent.com/cam/policy/detail/9545933&QcloudLIVEFullAccess&2) (kebijakan baca dan tulis) dan [QcloudLIVEReadOnlyAccess](https://console.cloud.tencent.com/cam/policy/detail/13346800&QcloudLIVEReadOnlyAccess&2) (kebijakan hanya-baca).
   - Untuk menggunakan tag, otorisasi [QcloudTAGFullAccess](https://console.cloud.tencent.com/cam/policy/detail/1592575&QcloudTAGFullAccess&2) (akses baca dan tulis penuh dengan tag) diperlukan.
   - Untuk menggunakan log real-time, otorisasi [QcloudCamFullAccess](https://console.cloud.tencent.com/cam/policy/detail/596169&QcloudCamFullAccess&2) (akses baca/tulis penuh ke CAM) diperlukan.
- **Custom policy** (Kebijakan kustom): buka halaman **Policies** (Kebijakan), klik **Create Custom Policy** (Buat Kebijakan Kustom), dan pilih **Create by Policy Generator** (Buat dengan Pembuat Kebijakan). Informasi selengkapnya dapat dilihat di [Custom Policy (Kebijakan Kustom)](https://intl.cloud.tencent.com/document/product/598/10601).
>? Saat ini, beberapa API CSS mendukung otorisasi tingkat sumber daya.

**Contoh operasi:** jika Anda perlu memberikan izin API **DescribeLiveDomains** kepada sub-pengguna untuk nama domain tertentu, ikuti langkah-langkah di bawah ini untuk melakukan konfigurasi:
	1. Buat kebijakan tingkat domain yang mengizinkan akses ke API, buka halaman **Create by Policy Generator** (Buat dengan Pembuat Kebijakan), lalu atur item konfigurasi berikut:
<table>
<tr><th>Item Konfigurasi</th><th>Diperlukan</th><th>Deskripsi</th></tr>
<tr>
<td>Effect (Efek)</td><td>Ya</td><td>Pilih <b>Allow (Izinkan)</b></td>
</tr><tr>
<td>Service (Layanan)</td><td>Ya</td><td>Pilih <b>Cloud Streaming Services (Layanan Streaming Cloud)</b></td>
</tr><tr>
<td>Action (Tindakan)</td><td>Ya</td><td>Pilih <b>DescribeLiveDomains</b></td>
</tr><tr>
<td>Resource (Sumber Daya)</td><td>Ya</td>
<td>Pilih semua sumber daya atau sumber daya tertentu yang ingin Anda otorisasi.<ul style="margin:0"><li>Layanan Tencent Cloud dengan perincian otorisasi di tingkat operasi atau tingkat layanan <b>tidak mendukung deskripsi sumber daya enam segmen; untuk layanan ini, cukup pilih semua sumber daya</b>. </li><li>Untuk layanan Tencent Cloud dengan perincian otorisasi di tingkat sumber daya, Anda dapat memilih sumber daya tertentu. Informasi seputar metode deskripsi sumber daya dapat dilihat di panduan CAM terkait di <a href="https://intl.cloud.tencent.com/document/product/598/10588">CAM-Enabled Products (Produk yang Didukung CAM)</a>. Untuk mengetahui perincian otorisasi khusus layanan Tencent Cloud, lihat Perincian Otorisasi di <a href="https://intl.cloud.tencent.com/document/product/598/10588">CAM-Enabled Products (Produk yang Didukung CAM)</a>.< /li></ul></td>
</tr><tr>
<td>Condition (Kondisi)</td><td>Tidak</td>
<td>Atur kondisi efektif untuk otorisasi di atas dan masukkan IP sumber yang akan diberi otorisasi sehingga memungkinkan akses ke operasi tertentu hanya jika permintaan datang dari rentang IP yang ditentukan. Anda juga dapat menambahkan kondisi lain untuk membatasi lebih lanjut kebijakan. Informasi selengkapnya dapat dilihat di <a href="https://intl.cloud.tencent.com/document/product/598/10608">Condition (Kondisi)</a>.</td>
</tr></table>

<img src="https://qcloudimg.tencent-cloud.cn/raw/da4b1d1379c74e8d5eeb3f79908191e6.png">

> ! Jika ingin mengizinkan beberapa layanan, Anda dapat mengeklik **Add Permissions** (Tambahkan Izin) untuk mengonfigurasi kebijakan otorisasi untuk layanan ini.

2. Klik **Next** (Selanjutnya) untuk membuat kebijakan. Kemudian, kaitkan kebijakan dengan pengguna/grup pengguna menggunakan salah satu dari dua metode di atas.
![](https://qcloudimg.tencent-cloud.cn/raw/c88a7d7181c31262d9ed46ce938361db.png)


### Langkah 3. Menggunakan sub-akun
Anda dapat menggunakan identitas sub-akun (ID dan kata sandi sub-akun yang dibuat oleh akun root) untuk memanggil API yang diberi izin (misalnya `DescribeLiveDomains`) untuk mendapatkan informasi CSS (misalnya semua domain di akun terkait).

