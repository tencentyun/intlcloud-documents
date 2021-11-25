Mengembalikan data snapshot ke disk cloud dapat memulihkan data disk ke status saat snapshot dibuat.Metode ini sangat berguna jika terjadi kesalahan data atau kehilangan data yang disebabkan oleh perubahan tertentu.

Snapshot hanya bisa dikembalikan ke disk cloud tempatnya dibuat.Jika Anda perlu mendapatkan data snapshot dari disk cloud lain, silakan gunakan layanan [Membuat Disk Cloud dari Snapshot](/doc/product/362/5757).

Catatan:

- Saat Anda mengembalikan snapshot ke disk cloud elastis, disk harus dilepas.
- Saat Anda mengembalikan snapshot ke disk cloud non-elastis yang dibeli dengan CVM, instance CVM harus dimatikan.

## Mengembalikan Snapshot di Konsol
1) Buka [Konsol CVM](https://console.cloud.tencent.com/cvm/).

2) Klik "Snapshot" di panel navigasi.

3) Pilih snapshot yang perlu dikembalikan ke disk dalam daftar snapshot, dan klik "Rollback".

## Mengembalikan Snapshot melalui API
Anda dapat menggunakan API [`ApplySnapshot`](https://intl.cloud.tencent.com/zh/document/product/362/15643) untuk mengembalikan snapshot.
