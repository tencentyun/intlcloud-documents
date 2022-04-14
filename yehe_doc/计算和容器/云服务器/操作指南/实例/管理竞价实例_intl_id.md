## Skenario
Dokumen ini memberikan panduan tentang pengelolaan dan pembelian instans spot. Saat ini, instans spot tersedia melalui saluran berikut:
- **CVM console** (Konsol CVM): **Spot Instances** (Instans Spot) telah ditambahkan sebagai opsi untuk **Billing Mode** (Mode Penagihan) di halaman pembelian CVM.
- **BatchCompute console** (Konsol BatchCompute): Instans spot dapat dipilih saat pengguna mengirimkan pekerjaan dan membuat lingkungan komputasi di konsol BatchCompute.
- **TencentCloud API** (TencentCloud API): Parameter yang terkait dengan instans spot telah ditambahkan ke [RunInstances API](https://intl.cloud.tencent.com/document/product/213/33237).


## Petunjuk
### Konsol CVM

1. Login ke [halaman pembelian CVM](https://buy.cloud.tencent.com/cvm).
2. Pada halaman tab **Select a model** (Pilih model), atur **Billing Mode** (Mode Penagihan) ke **Spot Instances** (Instans Spot).
3. Tentukan **Region** (Wilayah), **Availability Zone** (Zona Ketersediaan), **Network** (Jaringan), **Instance** (Instans), dan konfigurasi lainnya seperti yang diperlukan dan diminta.
4. Periksa informasi instans spot yang akan dibeli dan detail biaya setiap item konfigurasi.
5. Klik **Purchase** (Beli) dan selesaikan pembayaran.
Setelah menyelesaikan pembayaran, Anda dapat login ke [konsol CVM](https://console.cloud.tencent.com/cvm) untuk memeriksa instans spot Anda.

### Konsol BatchCompute
- **Async API** (Async API): Ketika Anda mengirimkan pekerjaan, buat lingkungan komputasi, atau modifikasi jumlah instans yang diharapkan dalam lingkungan komputasi, instans BatchCompute akan memproses permintaan Anda secara asinkron. Ketika tidak dapat memenuhi permintaan saat ini karena alasan inventaris atau harga, instans BatchCompute terus menerapkan sumber daya instans spot hingga permintaan saat ini terpenuhi.
Jika Anda perlu merilis instans, Anda perlu menyesuaikan jumlah instans yang diharapkan di lingkungan komputasi melalui konsol BatchCompute. Jika Anda merilis instans melalui konsol CVM, konsol BatchCompute akan secara otomatis membuat instans hingga jumlah instans yang diharapkan terpenuhi.
- **Cluster Mode** (Mode Kluster): Lingkungan komputasi instans BatchCompute dapat mempertahankan sekumpulan instans spot sebagai kluster. Anda hanya perlu mengirimkan jumlah yang diharapkan, konfigurasi, dan harga maksimum instans spot. Lingkungan komputasi akan terus berlaku untuk instans spot hingga jumlah yang diharapkan terpenuhi. Meskipun instans spot tidak tersambung ke internet, lingkungan komputasi akan secara otomatis menerapkan instans spot lagi untuk memenuhi jumlah yang diharapkan.
- **Fixed Price** (Harga Tetap): Saat ini, instans spot disediakan dengan diskon tetap. Anda harus menetapkan nilai yang lebih besar atau sama dengan harga pasar saat ini. Untuk harga pasar, lihat [Instans Spot - Wilayah yang didukung dan jenis instans](https://intl.cloud.tencent.com/document/product/213/17817).

#### Petunjuk

1. Login ke [konsol BatchCompute](https://console.cloud.tencent.com/batch/env).
2. Pada halaman **Computing environment** (Lingkungan komputasi), pilih wilayah secara acak, seperti Guangzhou, lalu klik **New** (Baru).
Halaman **New computing environment** (Lingkungan komputasi baru) akan muncul.
3. Pada halaman **New computing environment** (Lingkungan komputasi baru), atur **Billing Type** (Jenis Penagihan) ke **Spot Instance** (Instans Spot), lalu tentukan konfigurasi seperti **Model Type** (Jenis Model), **Image** (Citra), **Name** (Nama), dan **Expected quantity** (Kuantitas yang diharapkan) sesuai kebutuhan, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/afb048292803098eeddd7c9ae6ede96a.png)
4. Klik **OK** (OKE) untuk menyelesaikan pembuatan.
Kemudian, Anda dapat memeriksa lingkungan komputasi baru di [konsol BatchCompute](https://console.cloud.tencent.com/batch/env). Untuk melihat kemajuan pembuatan instans CVM yang sedang dibuat di lingkungan komputasi, klik **Activity Logs** (Log Aktivitas) dan **Instance List** (Daftar Instans) untuk lingkungan komputasi.


### TencentCloud API
Di RunInstances API, Anda dapat menentukan parameter [InstanceMarketOptionsRequest](https://intl.cloud.tencent.com/document/api/213/15753#InstanceMarketOptionsRequest) untuk mengaktifkan atau menonaktifkan mode instans spot dan mengonfigurasi informasi tentang instans spot.
* **Sync API** (Sync API): Saat ini, RunInstances menyediakan API permintaan sinkronisasi satu kali. Ini berarti bahwa jika aplikasi gagal karena inventaris tidak mencukupi atau harga yang diminta lebih rendah dari harga pasar, RunInstances API segera mengembalikan kode kegagalan dan tidak berlaku untuk instans spot lagi.
* **Fixed Price** (Harga Tetap): Saat ini, instans spot disediakan dengan diskon tetap. Anda harus menetapkan nilai yang lebih besar atau sama dengan harga pasar saat ini. Untuk harga pasar, lihat [Instans Spot - Wilayah yang didukung dan jenis instans](https://intl.cloud.tencent.com/document/product/213/17817).

#### Contoh
Anda memiliki instans di Zona 3 Guangzhou, dan mode penagihan instans adalah bayar sesuai pemakaian per jam dan dalam mode spot. Konfigurasi spesifik dari mode penagihan adalah sebagai berikut:
- MaxPrice: 0,0923 USD/jam
- SpotInstanceType: one-time
- ImageId: img-pmqg1cw7
- InstanceType: S2.MEDIUM4 (Standard 2, 2-core, 4GB)
- InstanceCount: 1

#### Meminta parameter
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
&Placement.Zone=ap-guangzhou-3
&InstanceChargeType=SPOTPAID
&InstanceMarketOptions.MarketType=spot
&InstanceMarketOptions.SpotOptions.MaxPrice=0.0923
&InstanceMarketOptions.SpotOptions.SpotInstanceType=one-time
&ImageId=img-pmqg1cw7
&InstanceType=S2.MEDIUM4
&InstanceCount=1
&<common request parameters>
```

#### Parameter respons
```
{
  "Response": {
    "InstanceIdSet": [
      "ins-1vogaxgk"
    ],
    "RequestID": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```
