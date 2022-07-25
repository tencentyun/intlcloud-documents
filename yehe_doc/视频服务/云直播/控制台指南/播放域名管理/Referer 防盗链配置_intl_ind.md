Anda dapat mengatur daftar blokir/daftar izin perujuk dan aturan untuk memblokir/mengizinkan permintaan pemutaran ulang untuk melindungi konten streaming langsung. Anda juga dapat memilih untuk mengizinkan perujuk kosong atau tidak.

## Cara Mengonfigurasi

URL perujuk didasarkan pada protokol HTTP. CSS menggunakan bidang referer (perujuk) dalam permintaan HTTP untuk mengidentifikasi sumber dan memverifikasi permintaan, lalu menentukan diterima atau ditolaknya permintaan.

## Catatan
- Informasi perujuk disertakan dalam permintaan HTTP. Oleh karena itu, konfigurasi perujuk tidak efektif untuk permintaan non-HTTP (seperti RTMP, WebRTC, QUIC). Jika Anda ingin membatasi akses permintaan RTMP agar pengguna yang berniat jahat tidak dapat melewati perlindungan hotlink perujuk melalui pull RTMP, silakan [kirimkan tiket](https://console.cloud.tencent.com/workorder/category).
- Pengaktifan, penonaktifan, atau modifikasi perujuk akan diterapkan dalam waktu 15‒20 menit setelah konfigurasi. Anda tidak perlu melakukan push pada streaming lagi.
- Fitur perlindungan hotlink perujuk memverifikasi informasi perujuk di header permintaan HTTP untuk memeriksa validitas permintaan dan mengizinkan atau menolak streaming langsung sesuai dengan hasil pemeriksaan. Namun, mungkin ada kasus perujuk palsu berhasil melewati verifikasi untuk melakukan hotlink ke layanan. Oleh karena itu, kami menyarankan Anda untuk tidak terlalu bergantung pada perujuk untuk melindungi konten Anda.

## Prasyarat

- Anda telah mengaktifkan layanan CSS dan login ke [konsol CSS](https://console.cloud.tencent.com/live/livestat).
- Anda telah [menambahkan nama domain pemutaran ulang](https://intl.cloud.tencent.com/document/product/267/35970).


[](id:open)
## Mengaktifkan Perujuk

1.Pilih **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **playback domain** (domain pemutaran ulang) target atau klik **Manage** (Kelola) di sebelah kanan untuk masuk ke halaman manajemen domain.
2.Dalam **Access Control** > **Referer Configuration** (Kontrol Akses > Konfigurasi Perujuk), klik **Edit** untuk masuk ke halaman konfigurasi perujuk.
 ![](https://main.qcloudimg.com/raw/32461edf0353c2c95925b74d80dc25b3.png)
3.Klik ![](https://main.qcloudimg.com/raw/c032c517e25867ff592f128424154688.png) untuk mengaktifkan perujuk dan melakukan konfigurasi sebagai berikut:
 ![](https://main.qcloudimg.com/raw/551044de4acd79683ae69cf106a87c0b.png)

<table id="setmess">
<tr><th width="14%">Item Konfigurasi</th><th>Deskripsi</th>
</tr><tr>
<td>Referer Type (Jenis Perujuk)</td>
<td>Pilih <b>Blocklist (Daftar Blokir)</b> atau <b>Allowlist (Daftar Izin)</b> sebagai jenis perujuk.
<ul style="margin:0">
<li>Anda tidak dapat memilih keduanya.</li>
<li>Saat daftar izin perujuk dikonfigurasikan, sumber permintaan di daftar akan diizinkan untuk mengakses konten streaming langsung, sementara sumber permintaan yang tidak ada di daftar akan diblokir.</li>
<li>Saat daftar blokir perujuk dikonfigurasikan, sumber permintaan di daftar akan diblokir sehingga tidak dapat mengakses konten streaming langsung, sementara sumber permintaan yang tidak ada di daftar akan diizinkan untuk mengakses.</li>
</ul></td>
</tr><tr>
<td>Allow Empty Referer (Izinkan Perujuk Kosong)</td>
<td><ul style="margin:0">
<li>Jika fitur ini diaktifkan, akses akan diizinkan untuk permintaan HTTP dengan bidang perujuk kosong atau tidak ada. Pengguna dapat mengakses URL streaming langsung secara langsung melalui browser.</li>
<li>Jika fitur ini dinonaktifkan, permintaan dengan perujuk kosong akan ditolak.</li>
</ul></td>
</tr><tr>
<td>Referer Patterns (Pola Perujuk)</td>
<td><ul style="margin:0">
<li>Anda dapat memasukkan hingga <b>100</b> pola. Harap pisahkan setiap pola dengan pemisah baris.</li>
<li>Anda dapat memasukkan <b>IP</b> atau <b>nama domain</b>. Bidang ini mendukung awalan jalur (nama domain dan IP) dan wildcard (nama domain) untuk pencocokan. Misalnya:<ul>
<li/>Jika Anda memasukkan <code>101.1.0.1</code> dan <code>www.test.com</code>, konfigurasi akan diterapkan untuk <code>101.1.0.1/157</code> dan <code>www.test.com/tencent</code>.
<li/>Jika Anda memasukkan <code>*.test.com</code>, konfigurasi akan diterapkan untuk <code>www.test.com</code> dan <code>a.test.com</code>.</ul></li>
<li>Jika Anda tidak memasukkan pola perujuk, daftar blokir/daftar izin tidak akan dikonfigurasikan.</li>
</ul></td>
</tr></table>

4. Klik **Save** (Simpan) untuk menyimpan konfigurasi.


[](id:change)
## Memodifikasi Perujuk
1. Pilih **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **playback domain** (domain pemutaran ulang) target atau klik **Manage** (Kelola) di sebelah kanan untuk masuk ke halaman manajemen domain.
2. Dalam **Access Control** > **Referer Configuration** (Kontrol Akses > Konfigurasi Perujuk), klik **Edit** untuk masuk ke halaman konfigurasi perujuk.
3. Modifikasi [item konfigurasi](#setmess), lalu klik **Save** (Simpan).

![](https://main.qcloudimg.com/raw/a8c79376ed22b4e47f35e69411c6df10.png)

[](id:close)
## Menonaktifkan Perujuk
Setelah [mengaktifkan perujuk](#open), Anda dapat menonaktifkannya dengan melakukan langkah-langkah berikut:

1. Pilih **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **playback domain** (domain pemutaran ulang) target atau klik **Manage** (Kelola) di sebelah kanan untuk masuk ke halaman manajemen domain.
2. Dalam **Access Control** > **Referer Configuration** (Kontrol Akses > Konfigurasi Perujuk), klik **Edit** untuk masuk ke halaman konfigurasi perujuk.
3. Klik ![](https://main.qcloudimg.com/raw/e72f89a0deb6858428dc3e93ce7e7088.png) untuk menonaktifkan perujuk.

![](https://main.qcloudimg.com/raw/eb36bc40cca9f19e198fc742256fed21.png)






