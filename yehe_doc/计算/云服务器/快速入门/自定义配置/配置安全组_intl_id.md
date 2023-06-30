Dokumen ini menjelaskan cara membuat dan mengonfigurasi grup keamanan untuk sebuah instans. Untuk informasi selengkapnya, lihat [Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/12452).


## Mengonfigurasi Grup Keamanan
1. Pilih **New security group** (Grup keamanan baru).
> Jika Anda sudah memiliki grup keamanan, Anda dapat memilih **Existing Security Groups** (Grup Keamanan yang Ada).
>
![](https://main.qcloudimg.com/raw/c08ca9a0262f4911fdac90925762e4a6.png)
2. Pilih alamat IP atau port untuk dibuka berdasarkan kebutuhan Anda yang sebenarnya.
Aturan untuk grup keamanan baru adalah sebagai berikut:<ul>
<li><b>ICMP</b>: membuka protokol ICMP dan mengizinkan ping server melalui jaringan publik.</li>
<li><b>TCP:80</b>: membuka port 80 dan mengizinkan akses ke layanan Web melalui HTTP.</li></li>
<li><b>TCP:22</b>: membuka port 22 dan memungkinkan koneksi jarak jauh ke CVM Linux melalui SSH.</li>
<li><b>TCP:443</b>: membuka port 443 dan mengizinkan akses ke layanan Web melalui HTTPS.</li>
<li><b>TCP:3389</b>: membuka port 3389 dan memungkinkan koneksi jarak jauh ke CVM Windows melalui RDP.</li>
<li><b>Jaringan pribadi</b>: membuka jaringan pribadi dan mengizinkan akses jaringan pribadi di antara berbagai sumber daya cloud (IPv4).</li></ul>
<blockquote class="d-mod-explain">
<div class="d-mod-title d-explain-title">
<i class="d-icon-explain"></i>Catatan:
</div>
<ul><li> Setelah Anda memilih alamat IP atau port yang akan dibuka, aturan masuk dan keluar yang terperinci akan ditampilkan di halaman tab <b>Security Group Rule</b> (Aturan Grup Keamanan).</li><li>Untuk membuka port lain bagi bisnis Anda, lihat <a href="https://intl.cloud.tencent.com/document/product/213/32369">Kasus Penggunaan Grup Keamanan</a> untuk <a href="https://intl.cloud.tencent.com/document/product/213/34271">membuat grup keamanan</a>. Untuk alasan keamanan, kami sarankan agar Anda hanya membuka port saat benar-benar diperlukan guna menghindari risiko keamanan yang tidak perlu.
</li></ul>
</blockquote>
3. Konfigurasikan informasi lain seperti yang diminta.

## Aturan Grup Keamanan

**Inbound rules** (Aturan masuk): mengizinkan lalu lintas ke CVM yang terkait dengan grup keamanan.
**Outbound rules** (Aturan keluar): menunjukkan lalu lintas keluar dari CVM.

- Aturan dalam grup keamanan adalah **prioritized from top to bottom** (diprioritaskan dari atas ke bawah).
- Saat CVM terikat ke grup keamanan tanpa aturan, semua lalu lintas masuk dan keluar ditolak secara default. Jika aturan tersedia, maka aturannya berlaku.
- Saat CVM terikat ke beberapa grup keamanan, grup keamanan dengan **smaller numbers have higher priority** (angka lebih kecil memiliki prioritas lebih tinggi).
- Saat CVM terikat ke beberapa grup keamanan, aturan penolakan berlaku untuk grup keamanan dengan prioritas terendah secara default.

## Batas Grup Keamanan

Untuk informasi selengkapnya, lihat [Batas Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/15379).
