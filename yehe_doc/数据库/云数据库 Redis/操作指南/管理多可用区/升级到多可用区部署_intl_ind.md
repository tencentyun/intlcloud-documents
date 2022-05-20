## Ikhtisar

Multi-AZ dibuat dengan menggabungkan beberapa AZ di wilayah yang sama. Klaster multi-AZ yang di-deploy memiliki kemampuan pemulihan bencana yang lebih baik daripada klaster AZ tunggal yang di-deploy dan dapat melindungi instans database Anda dari kegagalan tingkat IDC atau pemadaman AZ. Klaster AZ tunggal yang di-deploy yang ada dapat ditingkatkan secara otomatis ke klaster multi-AZ melalui migrasi data online tanpa gangguan bisnis. 

## Penagihan

 Fitur multi-AZ saat ini tersedia secara gratis; yaitu, klaster AZ tunggal yang di-deploy dapat ditingkatkan ke klaster multi-AZ secara gratis.

## Batas Penggunaan

Fitur ini saat ini tidak tersedia di wilayah Shenzhen Finance, Jakarta, dan Mumbai dan akan tersedia di lebih banyak wilayah dan AZ di masa mendatang.

## Catatan

- Jika [Membaca Node Lokal Saja](https://intl.cloud.tencent.com/document/product/239/41049) tidak diperlukan, peningkatan ke deployment multi-AZ hanya akan melibatkan migrasi metadata tanpa memengaruhi layanan, yang umumnya membutuhkan waktu kurang dari tiga menit untuk diselesaikan.
- Jika [Membaca Node Lokal Saja](https://intl.cloud.tencent.com/document/product/239/41049) diperlukan, Anda perlu meningkatkan versi proksi dan versi minor kernel Redis, yang akan melibatkan migrasi data dan mungkin membutuhkan waktu berjam-jam untuk diselesaikan. Akan ada satu atau beberapa pemutusan sementara dalam waktu tiga menit setelah peningkatan selesai, jadi pastikan bisnis Anda memiliki mekanisme koneksi ulang otomatis.

## Prasyarat

- Wilayah klaster memiliki setidaknya dua AZ.
- Basis data ada di v4.0 atau lebih baru.
- Instans dalam status **Running** (Berjalan).

## Petunjuk

1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis).
2. Di atas **instance list** (daftar instans) di sebelah kanan, pilih wilayah.
3. Dalam daftar instans, temukan instans target.
4. Klik **Instance ID** (ID instans) dari instans target dengan warna biru untuk masuk ke halaman **Instance Details** (Detail Instans).
5. Di bagian **Basic Info** (Info Dasar) di halaman **Instance Details** (Detail Instans), klik **Upgrade to Support Multi-AZ Deployment** (Tingkatkan untuk Mendukung Deployment Multi-AZ) setelah **AZ** (AZ).
![](https://main.qcloudimg.com/raw/1fb0cc13e207c84446d64a3a725c5c1c.png)
6. Di jendela **Upgrade to Support Multi-AZ Deployment** (Tingkatkan untuk Mendukung Deployment Multi-AZ), pelajari lebih lanjut tentang dampak peningkatan ke deployment multi-AZ, konfirmasikan apakah akan mendukung [Membaca Node Lokal Saja](https://intl.cloud.tencent.com/document/product/239/41049), dan klik **OK** (OKE).
7. **Instance Status** (Status Instans) di **Basic Info** (Info Dasar) menjadi **Upgrading to support multi-AZ deployment** (Meningkatkan untuk mendukung deployment multi-AZ). Tunggu statusnya menjadi **Running** (Berjalan).

## API Terkait

| API                                                      | Deskripsi |
| :----------------------------------------------------------- | :--------------- |
| [UpgradeVersionToMultiAvailabilityZones](https://intl.cloud.tencent.com/document/product/239/40162) | Upgrade instans untuk mendukung deployment multi-AZ |

