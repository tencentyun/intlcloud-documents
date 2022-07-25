Fitur watermark dinonaktifkan secara default untuk push langsung. Dokumen ini menjelaskan cara mengikat/melepaskan ikatan nama domain push ke/dari templat watermark untuk mengaktifkan/menonaktifkan fitur watermark.
 
## Catatan
- Konfigurasi templat akan diterapkan dalam waktu sekitar 5–10 menit.
- Setelah templat berhasil diikat, fitur watermark akan diaktifkan untuk alamat push di nama domain push yang ditentukan.
- Satu nama domain hanya dapat diikatkan ke satu templat watermark. Setelah terikat, semua streaming di nama domain tersebut akan diberi watermark sesuai dengan templat ini.

## Prasyarat
- Anda telah login ke [konsol CSS](https://console.cloud.tencent.com/live) dan menambahkan [nama domain push](https://intl.cloud.tencent.com/document/product/267/35970).
- Anda telah membuat [templat watermark](https://intl.cloud.tencent.com/document/product/267/31073)..


## Mengikat Templat Watermark
1. Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **push domain name** (nama domain push) yang akan dikonfigurasikan atau **Manage** (Kelola) untuk membuka halaman detail nama domain.
2. Klik **Template Configuration** (Konfigurasi Templat) dan, di area **Live Watermarking** (Pemberian Watermark Langsung), klik **Edit**.
![](https://qcloudimg.tencent-cloud.cn/raw/c9a415b0848a1d22b6e236c0ab4771ba.png)
3. Pilih templat watermark dan klik **Confirm** (Konfirmasi).
![](https://qcloudimg.tencent-cloud.cn/raw/b597758441bcabcbb3f38d74e649b4da.png)
>? Anda dapat mengeklik **Preview** (Pratinjau) di kolom **Operation** (Operasi) untuk melihat watermark.

## Melepaskan Ikatan Templat Watermark
1. Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **push domain name** (nama domain push) yang akan dikonfigurasikan atau **Manage** (Kelola) untuk membuka halaman detail nama domain.
2. Pilih **Template Configuration** (Konfigurasi Templat) dan klik **Edit** di bagian **Watermark Configuration** (Konfigurasi Watermark).
3. Hapus templat target dan klik **Confirm** (Konfirmasi).
![](https://qcloudimg.tencent-cloud.cn/raw/7a009d4780d4c91f0f06707abd9e22d9.png)
