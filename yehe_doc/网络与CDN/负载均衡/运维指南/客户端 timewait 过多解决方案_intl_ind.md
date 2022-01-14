## Latar belakang
Ketika menjalankan pengujian tekanan di CLB, koneksi Anda bisa gagal akibat terlalu banyak TIME-WAIT klien (semua port ditempati dalam waktu singkat).Berikut adalah alasan dan solusinya:

## Deskripsi parameter Linux
**tcp_timestamps:** untuk mengaktifkan cap waktu TCPCap waktu dinegosiasikan dalam handshake tiga arah TCP.Tanpa dukungan kedua belah pihak, parameter ini tidak akan digunakan dalam koneksi ini.
**tcp_tw_recycle:** untuk mengaktifkan penggunaan ulang kondisi TIME-WAIT TCP.
**tcp_tw_reuse:** ketika diaktifkan, koneksi dalam kondisi TIME_WAIT yang melampaui 1 detik dapat digunakan ulang secara langsung.

## Analisis Sebab
Klien memiliki TIME_WAIT terlalu banyak karena menutup koneksi secara proaktif.Ketika klien menutup koneksi, koneksi akan masuk ke dalam kondisi TIME_WAIT dan dapat digunakan kembali setelah 60 detik secara default.Dalam kasus ini, Anda dapat mengaktifkan parameter `tcp_tw_recycle` dan `tcp_tw_reuse` untuk memudahkan penggunaan ulang koneksi dalam kondisi TIME_WAIT.
Jika `tcp_timestamps` saat ini dinonaktifkan di CLB, parameter `tcp_tw_recycle` dan `tcp_tw_reuse` yang diaktifkan oleh klien tidak akan berlaku efektif, dan koneksi dalam kondisi TIME_WAIT tidak dapat digunakan kembali dengan cepat.Poin-poin berikut menjelaskan beberapa parameter Linux dan alasan mengapa `tcp_timestamps` tidak dapat diaktifkan di CLB:

1. tcp_tw_recycled dan tcp_tw_reuse hanya berlaku efektif ketika tcp_timestamps diaktifkan.

2. tcp_timestamps dan tcp_tw_recycle tidak dapat diaktifkan secara bersamaan karena klien jaringan publik gagal mengakses server melalui gateway NAT.Penyebabnya adalah sebagai berikut:

Jika tcp_tw_recycle dan tcp_timestamps sama-sama diaktifkan, cap waktu dalam permintaan koneksi soket dari IP sumber yang sama (server yang sama) pasti bertambah dalam 60 detik.Dengan mengambil kernel 2.6.32 sebagai contoh, detailnya adalah sebagai berikut:

![](https://mc.qcloudimg.com/static/img/2199611fec3b323a7b8fd3bb38459913/Linux1.png)

> tmp_opt.saw_tstamp: soket ini mendukung tcp_timestamp
sysctl_tw_recycle: tcp_tw_recycle telah diaktifkan untuk server ini
TCP_PAWS_MSL: 60s; komunikasi TCP terakhir dari IP sumber berlangsung dalam 60 detik
TCP_PAWS_WINDOW: 1; cap waktu komunikasi TCP terakhir dari IP sumber lebih besar daripada cap waktu komunikasi TCP ini

3.Di CLB (Lapisan-7), tcp_timestamps dinonaktifkan karena klien jaringan publik gagal mengakses server melalui gateway NAT, seperti yang terlihat dalam contoh berikut:

a.Kuintupel masih dalam kondisi TIME_WAIT.Dalam kebijakan alokasi port dari gateway NAT, kuintupel yang sama digunakan kembali dua kali masa pakai segmen maksimum (2MSL), dan paket SYN dikirim.

b.Ketika tcp_timestamps diaktifkan dan dua kondisi berikut terpenuh, paket SYN akan anjlok (karena opsi cap waktu diaktifkan, dan paket dianggap lama).
i.Cap waktu terakhir kali > Cap waktu kali ini
ii.Paket diterima dalam 24 hari (bidang cap waktu adalah 32-bit dan cap waktu diperbarui satu kali per 1 millidetik secara default di dalam Linux. Cap waktu akan membungkus setelah 24 hari).
Catatan:Masalah ini lebih jelas di perangkat seluler karena klien sama-sama memiliki IP jaringan publik terbatas di bawah gateway NAT dari ISP dan kuintupel dapat digunakan kembali di 2MSL.Cap waktu yang dikirim dari klien berbeda mungkin tidak bertambah.
Dengan mengambil kernel 2.6.32 sebagai contoh, detailnya adalah sebagai berikut:

![](https://mc.qcloudimg.com/static/img/6228a7dc25c670d4d2fbddc9ea400779/Linux2.png)

> rx_opt->ts_recent: cap waktu terakhir kali
rx_opt->rcv_tsval: cap waktu yang diterima pada waktu ini
get_seconds(): waktu saat ini
rx_opt->ts_recent_stamp: waktu ketika paket sebelumnya diterima

## Solusi
Jika klien memiliki terlalu banyak TIME_WAIT, lihat solusi di bawah:

**1.HTTP menggunakan koneksi tidak persisten (Koneksi: tutup).Dalam kasus ini, CLB secara proaktif menutup koneksi, dan klien tidak akan menghasilkan TIME_WAIT**.

**2.Jika skenarionya membutuhkan koneksi persisten, aktifkan opsi SO_LINGER pada soket dan gunakan RST untuk menutup koneksi guna menghindari kondisi TIME_WAIT dan mencapai penggunaan ulang port secara cepat**.
