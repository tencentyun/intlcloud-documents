Melalui migrasi online, Anda dapat memigrasikan sistem dan aplikasi pada server sumber dari IDC Anda atau platform cloud lainnya ke Tencent Cloud. Ini memenuhi persyaratan bisnis untuk cloudifikasi perusahaan, migrasi lintas vendor, migrasi lintas akun atau lintas wilayah, dan deploymnet cloud hibrida.
>? Server sumber dapat berupa server fisik, mesin virtual, atau server cloud pada platform cloud lain, seperti AWS, Microsoft Azure, Google Cloud Platform, Alibaba Cloud, atau Huawei Cloud.
>

## Kasus Penggunaan

Migrasi online berlaku untuk skenario berikut:
- Cloudifikasi arsitektur TI
- Deployment arsitektur cloud hibrida
- Migrasi lintas-cloud
- Migrasi lintas akun atau lintas wilayah

## Perbedaan dari Migrasi Offline

Dalam migrasi offline, Anda perlu membuat citra untuk disk sistem atau disk data di server sumber, lalu memigrasikan citra ke Cloud Virtual Machine (CVM) atau Cloud Block Storage (CBS). Anda tidak perlu membuat citra untuk migrasi online. Sebagai gantinya, Anda dapat menjalankan alat migrasi di server sumber untuk memigrasikannya ke CVM tujuan.

## Fitur

Saat ini, migrasi online mendukung fitur migrasi server.

## Persiapan

- Daftarkan akun Tencent Cloud dan siapkan CVM tujuan.
- Hentikan aplikasi di server sumber untuk mencegah aplikasi yang ada agar tidak terpengaruh oleh migrasi.
[Klik di sini](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) untuk mengunduh paket alat migrasi terkompresi.
- Periksa apakah server sumber dan CVM tujuan memenuhi persyaratan migrasi. Misalnya, disk cloud CVM tujuan harus memiliki kapasitas yang cukup untuk menyimpan data yang dimigrasikan dari server sumber.

## Memulai Migrasi
Gunakan go2tencentcloud yang disediakan oleh Tencent Cloud untuk migrasi. Untuk informasi selengkapnya tentang alat tersebut, lihat [Alat Migrasi Online](https://intl.cloud.tencent.com/document/product/213/35640).

## Pertanyaan Umum

Untuk informasi selengkapnya, harap lihat [Tentang Migrasi Layanan](https://intl.cloud.tencent.com/document/product/213/32395).



