
TencentDB for Redis kompatibel dengan Redis 2.8, 4.0, dan 5.0. Tingkatkan ke versi yang kompatibel didukung, sehingga Anda dapat meningkatkan instans Anda ke versi yang lebih baru untuk fitur yang lebih banyak.

## Deskripsi Peningkatan
- Saat ini, hanya instans arsitektur standar yang dapat ditingkatkan ke versi yang kompatibel.
- Instans dapat ditingkatkan dari versi yang lebih rendah ke versi yang lebih tinggi; misalnya, Anda dapat meningkatkan dari Redis 2.8 ke 4.0 atau dari 4.0 ke 5.0.
- Peningkatan lintas-versi didukung; misalnya, Anda dapat meningkatkan dari Redis 2.8 ke 5.0.
- Jika instans ditingkatkan ke versi yang kompatibel, tidak ada perubahan penagihan yang akan terjadi.
- Penurunan ke versi yang kompatibel tidak didukung.

## Cara Kerja Peningkatan
1. Terapkan untuk sumber daya: terapkan sumber daya versi instans baru, termasuk proksi, node master Redis, dan sumber daya node replika Redis.
2. Sinkronkan data: sinkronkan data lengkap dan tambahan dari instans pada versi lama ke instans pada versi baru.
3. Tunggu beralih: tunggu hingga sinkronisasi data selesai atau tunggu jendela beralih.
4. Beralih instans: ketika kondisi beralih terpenuhi (sinkronisasi data hampir selesai, dan persyaratan untuk jendela beralih terpenuhi), berhenti menulis data ke instans lama, lepaskan alamat IP virtual (VIP) darinya, dan ikat VIP ke instans baru.
5. Selesaikan peningkatan: perbarui status instans.

## Dampak Peningkatan
Proses peningkatan terutama terdiri dari sinkronisasi data dan peralihan instans:
- Selama sinkronisasi data, layanan tidak akan terpengaruh.
- Selama peralihan, instans akan menjadi baca saja selama kurang dari 1 menit (untuk menunggu penyelesaian sinkronisasi data), dan pemutusan sesaat (dalam beberapa detik) akan terjadi; oleh karena itu, bisnis Anda harus memiliki mekanisme koneksi ulang otomatis.

## Petunjuk Peningkatan
1. Login ke [Konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), pilih wilayah di bagian atas daftar instans, klik ID/nama instans, dan masuk ke halaman manajemen instans.
2. Pada halaman detail instans, klik **Peningkatan Versi**.
![](https://main.qcloudimg.com/raw/ebc4ecc50af95d99be2fa23f45d11278.png)
3. Di kotak dialog pop-up, pilih versi dan waktu beralih, lalu klik **OK**.
Beralih adalah proses ketika instans baru menggantikan yang lama. Fitur peningkatan mendukung opsi **Beralih Sekarang** dan **Beralih Jendela Pemeliharaan**.
    - Beralih Sekarang: peralihan akan dilakukan ketika sinkronisasi data hampir selesai (data yang tersisa untuk disinkronkan kurang dari 10 MB).
    - Beralih Jendela Pemeliharaan : peralihan akan dilakukan selama jendela pemeliharaan instans. Jika ketentuan peralihan tidak dapat dipenuhi di jendela pemeliharaan saat ini, peralihan akan dicoba di jendela berikutnya. Anda dapat mengubah waktu pemeliharaan di "Jendela Pemeliharaan" di halaman detail instans.
![](https://main.qcloudimg.com/raw/f584ccc7b3004feb662e72e8ddcf819a.png)
4. Kembali ke daftar instans. Setelah status instans berubah menjadi “Berjalan", instans dapat digunakan secara normal.
