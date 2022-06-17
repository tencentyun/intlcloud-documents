>!Dokumen ini menjelaskan fitur manajemen akses **SMS**. Informasi selengkapnya tentang manajemen akses untuk layanan Tencent Cloud lainnya dapat dilihat di [CAM-Enabled Products (Produk yang Didukung CAM)](https://intl.cloud.tencent.com/document/product/598/10588).

Suatu [kebijakan default](https://intl.cloud.tencent.com/document/product/382/38455) dalam kontrol akses SMS memang lebih mudah digunakan untuk menerapkan otorisasi, tetapi perincian kontrol izinnya terlalu rumit dan tidak dapat disederhanakan ke tingkat aplikasi SMS dan [TencentCloud API (API TencentCloud)](https://intl.cloud.tencent.com/product/api). Jika memerlukan kontrol izin dengan perincian sederhana, Anda perlu membuat kebijakan kustom.

## Metode Pembuatan Kebijakan Kustom
Ada beberapa cara untuk membuat kebijakan kustom. Tabel di bawah ini menunjukkan perbandingan berbagai metode. Lihat petunjuk di bawah ini untuk selengkapnya.

| Entri Pembuatan | Metode Pembuatan | Efek | Sumber Daya | Tindakan | Fleksibilitas |
|--------------|---------------|-------------|----------------|--------------|------|
| [Konsol CAM](https://console.cloud.tencent.com/cam/policy) | Penghasil kebijakan | Pemilihan manual | Deskripsi sintaks | Pemilihan manual | Sedang |
| [Konsol CAM](https://console.cloud.tencent.com/cam/policy) | Sintaks kebijakan | Deskripsi sintaks | Deskripsi sintaks | Deskripsi Sintaks | Tinggi |
| API Server CAM | [CreatePolicy (Buat Kebijakan)](https://intl.cloud.tencent.com/document/product/598/32248) | Deskripsi sintaks | Deskripsi sintaks | Deskripsi sintaks | Tinggi |

>?
>- SMS tidak mendukung pembuatan kebijakan kustom dengan fitur produk atau proyek.
>- Pemilihan manual berarti Anda dapat memilih objek dari daftar kandidat yang ditampilkan di konsol.
>- Deskripsi sintaks berarti Anda dapat mendeskripsikan objek melalui [sintaks kebijakan otorisasi](#.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95).

## Sintaks Kebijakan Otorisasi
### Deskripsi sintaks sumber daya
Seperti disebutkan di atas, perincian sumber daya manajemen izin di SMS adalah aplikasi. Deskripsi aplikasi dalam sintaks kebijakan mengikuti [metode deskripsi sumber daya CAM](https://intl.cloud.tencent.com/document/product/598/10606). Pada contoh di bawah, ID akun root developer adalah 12345678 dan developer telah membuat tiga aplikasi dengan `App` 1400000000, 1400000001, dan 1400000002.
- **Deskripsi sintaks kebijakan untuk semua aplikasi SMS**
```
"resource": ["qcs::sms::uin/12345678:app/*"]
```
- **Deskripsi sintaks kebijakan untuk satu aplikasi SMS**
```
"resource": [ "qcs::sms::uin/12345678:app/1400000001"]
```
- **Deskripsi sintaks kebijakan untuk beberapa aplikasi SMS**
```
"resource": [ "qcs::sms::uin/12345678:app/1400000000","qcs::sms::uin/12345678:app/1400000001"]
```

### Deskripsi sintaks tindakan
Seperti disebutkan di atas, perincian tindakan manajemen izin di SMS adalah API TencentCloud. Untuk informasi selengkapnya, lihat [Authorizable Resources and Actions (Sumber Daya dan Tindakan yang Dapat Diotorisasi)](https://intl.cloud.tencent.com/document/product/382/38454). API TencentCloud, seperti `DescribeAppList` (mendapatkan daftar aplikasi) dan `DescribeAppInfo` (mendapatkan informasi aplikasi) digunakan sebagai contoh di bawah ini.
- **Deskripsi sintaks kebijakan untuk semua API TencentCloud SMS**
```
"action": [
"name/sms:*"
]
```
- **Deskripsi sintaks kebijakan untuk satu API TencentCloud**
```
"action": [
"name/sms:DescribeAppList"
]
```
- **Deskripsi sintaks kebijakan untuk beberapa API TencentCloud**
```
"action": [
"name/sms:DescribeAppList",
"name/sms:DescribeAppInfo"
]
```

## Kasus Penggunaan Kebijakan Kustom
### Menggunakan penghasil kebijakan
Dalam contoh di bawah ini, kami akan membuat kebijakan kustom yang memungkinkan semua tindakan. kecuali konsol API `DeleteAppInfo`, untuk dilakukan pada aplikasi SMS 1400000001.
1. Akses halaman **[Kebijakan](https://console.cloud.tencent.com/cam/policy)** di konsol CAM menggunakan Tencent Cloud [akun root](https://intl.cloud.tencent.com/document/product/598/32633) dan klik **Create Custom Policy** (Buat Kebijakan Kustom).
2. Pilih **Create by Policy Generator** (Buat dengan Penghasil Kebijakan) untuk mengakses halaman pembuatan kebijakan.
3. Pilih layanan dan tindakan.
	● Pilih **Allow** (Izinkan) untuk **Effect** (Efek).
	● Pilih **Short Message Service (sms)** untuk **Service** (Layanan).
	● Centang semua item untuk **Action** (Tindakan).
	● Masukkan `qcs::sms::uin/12345678:app/1400000001` untuk **Resource** (Sumber Daya) sesuai dengan [deskripsi sintaks sumber daya](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0).
	● Item konfigurasi **Condition** (Kondisi) tidak perlu dikonfigurasi.
	● Klik **Add Statement** (Tambahkan Pernyataan) dan pernyataan "Any action is allowed on the SMS application 1400000001" (Tindakan apa pun diperbolehkan di aplikasi SMS 1400000001) akan muncul di bagian bawah halaman.
4. Terus tambahkan pernyataan lain pada halaman yang sama.
	● Pilih **Deny** (Tolak) untuk **Effect** (Efek).
	● Pilih **Short Message Service (sms)** untuk **Service** (Layanan).
	● Beri centang pada `DeleteAppInfo` (yang dapat ditemukan dengan cepat menggunakan mesin pencari) untuk **Action** (Tindakan).
	● Masukkan `qcs::sms::uin/12345678:app/1400000001` untuk **Resource** (Sumber Daya) sesuai dengan [deskripsi sintaks sumber daya](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0).
	● Item konfigurasi **Condition** (Kondisi) tidak perlu dikonfigurasi.
	● Klik **Add Statement** (Tambahkan Pernyataan) dan pernyataan "The `DeleteAppInfo` action is denied on the SMS application 1400000001" (Tindakan `DeleteAppInfo` ditolak di aplikasi SMS 1400000001) akan muncul di bagian bawah halaman.
5. Klik **Next** (Berikutnya) dan ganti nama kebijakan sesuai kebutuhan (atau biarkan apa adanya).
6. Klik **Done** (Selesai) untuk membuat kebijakan kustom.
Selanjutnya, kebijakan ini dapat diberikan ke sub-akun lain dengan cara yang sama seperti [memberikan akses penuh ke SMS ke sub-akun yang ada](https://intl.cloud.tencent.com/document/product/382/38455#.E5.B0.86-sms-.E5.85.A8.E8.AF.BB.E5.86.99.E8.AE.BF.E9.97.AE.E6.9D.83.E9.99.90.E6.8E.88.E4.BA.88.E5.B7.B2.E5.AD.98.E5.9C.A8.E7.9A.84.E5.AD.90.E8.B4.A6.E5.8F.B7).

### Menggunakan sintaks kebijakan
Dalam contoh di bawah ini, kami akan membuat kebijakan kustom yang memungkinkan semua tindakan pada aplikasi SMS 1400000001 dan 1400000002, tetapi menolak tindakan `DeleteAppInfo` untuk aplikasi 1400000001.
1. Akses halaman **[Kebijakan](https://console.cloud.tencent.com/cam/policy)** di konsol CAM menggunakan Tencent Cloud [akun root](https://intl.cloud.tencent.com/document/product/598/32633) dan klik **Create Custom Policy** (Buat Kebijakan Kustom).
2. Pilih **Create by Policy Syntax** (Buat dengan Sintaks Kebijakan) untuk mengakses halaman pembuatan kebijakan.
3. Di kotak **Select a template type** (Pilih jenis template), pilih **Blank Template** (Template Kosong).
>?Template kebijakan digunakan untuk membuat kebijakan dengan menyalin kebijakan yang ada (prasetel atau kustom), lalu membuat penyesuaian pada salinannya. Selama penggunaan sebenarnya, Anda dapat memilih template kebijakan yang sesuai berdasarkan kondisi sebenarnya untuk mengurangi kesulitan dan beban kerja penulisan konten kebijakan.
4. Klik **Next** (Berikutnya) dan ganti nama kebijakan sesuai kebutuhan (atau biarkan apa adanya).
5. Masukkan konten kebijakan berikut di kotak **Policy Content** (Konten Kebijakan):
```
{
 "version": "2.0",
 "statement": [
     {
          "effect": "allow",
          "action": [
              "name/SMS:*"
          ],
          "resource": [
              "qcs::sms::uin/12345678:app/1400000001",
              "qcs::sms::uin/12345678:app/1400000002"
          ]
      },
      {
          "effect": "deny",
          "action": [
              "name/SMS: DeleteAppInfo "
          ],
          "resource": [
              "qcs::SMS::uin/12345678:app/1400000001"
          ]
      }
  ]
}
```
>?Konten kebijakan harus mengikuti [logika sintaks kebijakan CAM](https://intl.cloud.tencent.com/document/product/598/10603), dengan sintaks "sumber daya" dan "tindakan" seperti yang ditunjukkan di atas dalam [Deskripsi sintaks sumber daya](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0) dan [Deskripsi sintaks tindakan](#.E6.93.8D.E4.BD.9C.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0).
6. Klik **Complete** (Selesai) untuk membuat kebijakan kustom.
Selanjutnya, kebijakan ini dapat diberikan ke sub-akun lain dengan cara yang sama seperti [memberikan akses penuh ke SMS ke sub-akun yang ada](https://intl.cloud.tencent.com/document/product/382/38455#.E5.B0.86-sms-.E5.85.A8.E8.AF.BB.E5.86.99.E8.AE.BF.E9.97.AE.E6.9D.83.E9.99.90.E6.8E.88.E4.BA.88.E5.B7.B2.E5.AD.98.E5.9C.A8.E7.9A.84.E5.AD.90.E8.B4.A6.E5.8F.B7).
