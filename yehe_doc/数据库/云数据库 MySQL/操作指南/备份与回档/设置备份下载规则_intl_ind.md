
Secara default, Anda dapat mengunduh file cadangan instans TencentDB for MySQL melalui jaringan publik atau pribadi. Untuk membatasi unduhan, sesuaikan pengaturan unduhan cadangan.
>?
>- Pengaturan unduhan cadangan didukung di wilayah berikut:
>Guangzhou, Shanghai, Beijing, Shenzhen, Chengdu, Chongqing, Nanjing, Hong Kong (Tiongkok), Beijing Finance, Shanghai Finance, Shenzhen Finance, Toronto, Singapura, Silicon Valley, Frankfurt, Seoul, Mumbai, Bangkok, Moskow, dan Tokyo.
>- Cara mengaktifkan pengaturan unduhan cadangan:
> - Sebelum 9 November 2021, Anda harus [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk mengaktifkan fitur ini.
> - Mulai 9 November 2021, fitur ini tersedia di konsol.

## Mengatur Aturan Unduhan Cadangan
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), pilih **Database Backup** (Cadangan Database) di bilah sisi kiri, dan pilih wilayah di bagian atas.
2. Pada tab **Download Settings** (Pengaturan Unduhan), lihat pengaturan unduhan cadangan dan klik **Edit** (Edit) untuk memodifikasinya.
>?Unduh melalui jaringan publik diaktifkan secara default dan ketika diaktifkan, unduh melalui jaringan pribadi juga diizinkan.
>
![](https://qcloudimg.tencent-cloud.cn/raw/530fbf3e6c93eea06ff23e112cad84c0.png)
3. Pada halaman yang ditampilkan, tetapkan aturan unduhan dan klik **OK** (OKE).
   - Unduh melalui jaringan publik:
     - Diaktifkan: Anda tidak dapat menetapkan aturan unduhan apa pun.
     - Dinonaktifkan: Anda dapat mengatur aturan unduhan dengan mengizinkan atau memblokir IP dan VPC tertentu.
   - Tetapkan aturan unduhan:
     - Jika Anda tidak menentukan nilai apa pun, kondisi tidak akan berlaku.
     - Anda harus memisahkan nilai kondisi IP dengan koma.
     - Anda dapat memasukkan IP atau rentang IP sebagai nilai kondisi IP.
     - Jika tidak ada persyaratan IP dan VPC yang ditetapkan, tidak akan ada batasan unduhan melalui jaringan pribadi.
![](https://qcloudimg.tencent-cloud.cn/raw/7e0a4a48af62fdd643259f8902fcd95f.png)
4. Setelah konfigurasi selesai, kembali ke tab **Download Settings** (Pengaturan Unduhan) untuk melihat aturan yang berlaku.
![](https://qcloudimg.tencent-cloud.cn/raw/cb4ac45dcde8a57610b0eaec9075c6cb.png)

## Mengotorisasi Sub-akun untuk Mengatur Aturan Unduhan Cadangan
Secara default, sub-akun tidak memiliki izin untuk menetapkan aturan unduhan cadangan untuk instans TencentDB for MySQL. Dengan demikian, Anda perlu membuat kebijakan CAM untuk memberikan izin kepada sub-akun tertentu.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) adalah layanan web yang disediakan oleh Tencent Cloud yang membantu Anda mengelola akses dengan aman ke sumber daya di bawah akun Tencent Cloud Anda. CAM memungkinkan Anda membuat, mengelola, atau menghentikan pengguna atau grup pengguna dan mengontrol siapa yang diizinkan untuk menggunakan sumber daya Tencent Cloud Anda melalui pengelolaan identitas dan kebijakan.

Saat menggunakan CAM, Anda dapat mengaitkan kebijakan dengan pengguna atau grup pengguna untuk mengizinkan atau melarang mereka menggunakan sumber daya tertentu untuk menyelesaikan tugas tertentu. Untuk informasi selengkapnya tentang kebijakan CAM, harap lihat [Logika Sintaksis](https://intl.cloud.tencent.com/document/product/598/10603).

### Memberi otorisasi sub-akun
1. Login ke [konsol CAM](https://console.cloud.tencent.com/cam) dengan akun root, temukan sub-pengguna target dalam daftar pengguna, dan klik **Authorize** (Beri Otorisasi).
![img](https://qcloudimg.tencent-cloud.cn/raw/89d7cf063bd376a0cc4f4db0c78e7e56.png)
2. Di jendela pop-up, pilih kebijakan prasetel **QcloudCDBFullAccess** (QcloudCDBFullAccess) dan klik **OK** (OKE) untuk menyelesaikan otorisasi.
![](https://qcloudimg.tencent-cloud.cn/raw/0819ca9a1a81fc00968f0a263dc7727e.png)

### Sintaksis kebijakan
Sintaksis kebijakan berikut digunakan untuk mengotorisasi sub-akun untuk menetapkan aturan unduhan cadangan untuk instans TencentDB for MySQL:
```
{
       "version":"2.0",
       "statement":
       [
          {
             "effect":"effect",
             "action":["action"],
             "resource":["resource"]
            }
       ] 
}
```
- **version** (versi) diperlukan. Saat ini, hanya nilai "2.0" yang diizinkan.
- **statement** (pernyataan) menjelaskan detail dari satu atau beberapa izin. Elemen ini berisi izin atau sekumpulan izin yang terdiri dari elemen lain seperti efek, tindakan dan sumber daya. Satu kebijakan hanya memiliki satu pernyataan.
- **effect** (efek) diperlukan. Ini menggambarkan hasil dari sebuah pernyataan. Hasilnya bisa berupa "allow" (izinkan) atau "deny" (tolak) eksplisit.
- **action** (tindakan) diperlukan. Ini menjelaskan operasi yang diizinkan atau ditolak. Operasi dapat berupa API (diawali dengan "name") atau kumpulan fitur (kumpulan API tertentu yang diawali dengan "permid").
- **resource** (sumber daya) diperlukan. Ini menjelaskan detail otorisasi.

### Operasi API
Dalam pernyataan kebijakan CAM, Anda dapat menentukan operasi API apa pun dari layanan apa pun yang mendukung CAM. API yang diawali dengan `name/cdb:` harus digunakan untuk TencentDB for MySQL. Untuk menentukan beberapa operasi dalam satu pernyataan, pisahkan dengan koma seperti yang ditunjukkan di bawah ini:
```
"action":["name/cdb:action1","name/cdb:action2"]
```
Anda juga dapat menentukan beberapa operasi menggunakan wildcard. Misalnya, Anda dapat menentukan semua operasi yang namanya dimulai dengan "Describe" seperti yang ditunjukkan di bawah ini:
```
"action":["name/cdb:Describe*"]
```

### Jalur sumber daya
Format umum jalur sumber daya adalah sebagai berikut:
```
qcs::service_type::account:resource
```
- service_type: menjelaskan singkatan produk, seperti `cdb` di sini.
- akun: adalah akun root dari pemilik sumber daya, seperti "uin/326xxx46".
- sumber daya: menjelaskan informasi sumber daya terperinci dari layanan tertentu. Setiap instans TencentDB for MySQL (instanceId) adalah sumber daya.

Contohnya adalah sebagai berikut:
```
 "resource": ["qcs::cdb::uin/326xxx46:instanceId/cdb-kfxxh3"]
```
Di sini, `cdb-kfxxh3` adalah ID sumber daya instans TencentDB for MySQL, yaitu, `resource` dalam pernyataan kebijakan CAM.

### Contoh
Contoh berikut hanya menunjukkan penggunaan CAM. Untuk daftar lengkap API yang digunakan untuk menetapkan aturan unduhan cadangan MySQL, lihat [dokumentasi API](https://intl.cloud.tencent.com/document/product/236/43327).
```
{
       "version":"2.0",
       "statement":
       [
          {
             "effect":"allow",
             "action": ["name/cdb: ModifyBackupDownloadRestriction"],
             "resource": ["*"]
            }
       ]
}
```

### Menyesuaikan kebijakan CAM untuk menetapkan aturan unduhan cadangan MySQL
1. Login ke [konsol CAM](https://console.cloud.tencent.com/cam/policy) dengan akun root, pilih **Policies** (Kebijakan) di bilah sisi kiri, dan klik **Create Custom Policy** (Buat Kebijakan Kustom).
![img](https://qcloudimg.tencent-cloud.cn/raw/4ddc463dc28ee48b9dd63d862fa41ea1.png)
2. Di kotak dialog pop-up, pilih **Create by Policy Generator** (Buat berdasarkan Generator Kebijakan).
3. Pada halaman **Select Service and Action** (Pilih Layanan dan Tindakan), pilih item konfigurasi, klik **Add Statement** (Tambahkan Pernyataan), dan klik **Next** (Selanjutnya).
   - Layanan: pilih **TencentDB for MySQL** (TencentDB for MySQL).
   - Tindakan: pilih semua API pengaturan aturan unduhan cadangan MySQL. Untuk informasi selengkapnya, lihat [dokumentasi API](https://intl.cloud.tencent.com/document/product/236/43327).
   - Sumber Daya: untuk informasi selengkapnya, lihat [Metode Deskripsi Sumber Daya](https://intl.cloud.tencent.com/document/product/598/10606). Anda dapat memasukkan `*` untuk menunjukkan bahwa aturan unduhan cadangan untuk instans TencentDB for MySQL di wilayah yang ditentukan dapat diatur.
![](https://qcloudimg.tencent-cloud.cn/raw/5372ae1d2ac16ff63b63fbf175f3fccf.png)
4. Pada halaman **Edit Policy** (Edit Kebijakan), masukkan **Policy Name** (Nama Kebijakan) (seperti `BackupDownloadRestriction`) sesuai kebutuhan dan **Description** (Deskripsi) lalu klik **Done** (Selesai).
![](https://qcloudimg.tencent-cloud.cn/raw/3c5454e0da412c0e12beebb4b045979d.png)
5. Kembali ke daftar kebijakan dan Anda dapat melihat kebijakan khusus yang baru saja dibuat.
![](https://qcloudimg.tencent-cloud.cn/raw/d242b34c0b9cad83d130444d84e205e0.png)

