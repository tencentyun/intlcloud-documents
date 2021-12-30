1. **Creating HAVIP** (Membuat HAVIP)
Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/havip) dan buat HAVIP. Untuk petunjuk detail, lihat [Membuat HAVIP](https://intl.cloud.tencent.com/document/product/215/31820#.E5.88.9B.E5.BB.BA-havip).
2. **Binding and configuration** (Pengikatan dan konfigurasi)
Konfigurasinya sama dengan mode tradisional. Server backend mendeklarasikan dan menegosiasikan perangkat yang akan terikat dengan HAVIP yang dibuat. Anda hanya perlu menentukan alamat IP virtual dalam file konfigurasi sebagai HAVIP.
Di pengelola kluster, tambahkan HAVIP yang baru saja dibuat.
3. **Verification** (Verifikasi)
Setelah konfigurasi selesai, langsung beralih node untuk pengujian.
Dalam situasi normal, Anda akan melihat bahwa jaringan pulih setelah gangguan singkat (tidak ada gangguan sama sekali jika peralihan cukup cepat), dan layanan online tidak akan terpengaruh.

