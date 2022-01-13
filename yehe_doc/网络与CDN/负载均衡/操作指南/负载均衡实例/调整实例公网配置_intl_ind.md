Anda bisa menyesuaikan bandwidth atau cara penagihan jaringan publik instance CLB sesuai kebutuhan secara real-time.

## Batasan
- Instance CLB IPv4: penyesuaian konfigurasi jaringan hanya didukung untuk akun tagihan per IP, tetapi tidak untuk akun tagihan per CVM.
- Instance CLB IPv6: penyesuaian konfigurasi jaringan didukung untuk akun tagihan per IP dan tagihan per CVM.
- Untuk informasi lebih jauh tentang cara memeriksa jenis akun Anda, silakan buka [Memeriksa Jenis Akun](https://intl.cloud.tencent.com/document/product/684/15246).

## Batas Bandwidth
<table>
<tbody><tr><th>Mode Tagihan Instance</th><th>Mode Tagihan Jaringan</th><th >Rentang Batas Bandwidth (dalam Mbps)</th></tr>
<tr><td rowspan="3">Bayar sesuai pemakaian</td><td>Tagihan per bandwidth (per jam)</td><td  rowspan="3">0 - 2048 (inklusif)</td></tr>
<tr><td>Tagihan per lalu lintas</td></tr>
<tr><td>Paket bandwidth</td></tr>
</tbody></table>

>? Jika Anda perlu mengatur batas bandwidth yang lebih tinggi, silakan [kirimkan tiket](https://console.cloud.tencent.com/workorder/category) atau hubungi perwakilan penjualan Tencent Cloud Anda.
>

## Menyesuaikan Bandwidth
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2.Pada halaman **Instance Management** (Manajemen Instance), pilih satu wilayah, dan klik **More** -> **Adjust Bandwidth** (Selengkapnya -> Sesuaikan Bandwidth) di sebelah kanan instance CLB jaringan publik.
3.Di kotak dialog, atur batas bandwidth dan klik **Submit** (Kirim).

## Mengubah Cara Penagihan
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2.Pada halaman **Instance Management** (Manajemen Instance), pilih satu wilayah, klik **More** (Lainnya) di sebelah kanan instance CLB jaringan publik dan terus menyesuaikan cara penagihan jaringan.
<table>
<tbody><tr><th>Cara Penagihan Instance</th><th>Cara Penagihan Jaringan</th><th >Penyesuaian</th></tr>
<tr><td rowspan="3">Bayar sesuai pemakaian</td><td>Tagihan per bandwidth (per jam)</td><td>Tambahkan IP ke paket bandwidth: cara penagihan instance tetap sama; cara penagihan jaringan dialihkan ke menggunakan paket bandwidth; setiap instance hanya bisa dialihkan cara penagihannya satu kali.</td></tr>
<tr><td>Tagihan per lalu lintas</td><td><ul><li>Alihkan ke langganan bulanan: cara penagihan instance dialihkan ke langganan bulanan; cara penagihan jaringan dialihkan ke tagihan per bandwidth (bulanan); setiap instance hanya bisa dialihkan cara penagihannya satu kali.</li><li>Tambahkan IP ke paket bandwidth: cara penagihan instance tetap sama; cara penagihan jaringan dialihkan ke menggunakan paket bandwidth; setiap instance bisa dialihkan cara penagihannya berulang kali.</li></ul></td></tr>
<tr><td>Paket bandwidth</td><td>Hapus IP dari paket bandwidth: cara penagihan instance tetap sama; cara penagihan jaringan dialihkan ke tagihan per lalu lintas; setiap instance bisa dialihkan cara penagihannya berulang kali.</td></tr>
</tbody></table>
3.Klik **Submit** (Kirim) di kotak dialog pop-up.

