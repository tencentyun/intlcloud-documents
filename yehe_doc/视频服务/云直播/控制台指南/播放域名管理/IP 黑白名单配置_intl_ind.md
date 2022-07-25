Dokumen ini menjelaskan cara mengonfigurasikan daftar izin/daftar blokir IP untuk memfilter permintaan dan mengontrol akses ke konten streaming.

## Ikhtisar
- IP **allowlist** (Daftar izin IP): Hanya alamat IP dalam daftar yang dapat mengakses konten streaming Anda.
- IP **blocklist** (Daftar blokir IP): Alamat IP dalam daftar tidak dapat mengakses konten streaming Anda.

## Prasyarat
Anda telah mengaktifkan CSS dan login ke [konsol CSS](https://console.cloud.tencent.com/live/livestat).
Anda telah menambahkan [nama domain pemutaran ulang](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:set)
## Mengonfigurasikan Daftar Izin/Daftar Blokir IP
1. Pilih **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **playback domain** (domain pemutaran ulang) target atau klik **Manage** (Kelola) di sebelah kanan untuk masuk ke halaman manajemen domain.
2. Klik **Access Control** (Kontrol Akses), lalu temukan **IP Allowlist/Blocklist** (Daftar Izin/Daftar Blokir IP).
![](https://qcloudimg.tencent-cloud.cn/raw/de64819fab139753ecde2ee7f20a5f63.png)
3. Klik ![](https://qcloudimg.tencent-cloud.cn/raw/b64d8a4343b3a1e340db3adb9002db60.png) untuk mengaktifkan daftar izin/daftar blokir IP dan menyelesaikan pengaturan berikut:
![](https://qcloudimg.tencent-cloud.cn/raw/a9cc1a4e8f9485c9fb057c0edaba177b.png)

<table>
<thead><tr><th>Item Konfigurasi</th><th>Deskripsi</th></tr></thead>
<tbody><tr>
<td>Authenticate By (Autentikasi menurut)</td>
<td>Allowlist or blocklist (Daftar izin atau daftar blokir):<ul style="margin:0">
<li>Anda tidak dapat memilih keduanya.</li>
<li>Jika Anda mengonfigurasi daftar izin, hanya alamat IP di daftar yang dapat mengakses konten streaming Anda.</li>
<li>Jika Anda mengonfigurasi daftar blokir, alamat IP di daftar tidak dapat mengakses konten streaming Anda.</li></ul></td>
</tr><tr>
<td>IP List (Daftar IP)</td>
<td>Anda dapat menambahkan hingga 200 item. Pisahkan item dengan pemisah baris.<ul style="margin:0">
<li>Mendukung alamat IP dan CIDR (/8/16/24), tetapi tidak mendukung nomor port.</li>
<li>Saat ini tidak mendukung IPv6.</li></ul></td>
</tr>
</tbody></table>

4. Klik **Save** (Simpan) untuk menyimpan konfigurasi (penerapan konfigurasi memerlukan waktu beberapa saat).
![](https://qcloudimg.tencent-cloud.cn/raw/8a0bf90247475062eef4aa43d34eb08f.png)

[](id:change)
## Memodifikasi Konfigurasi Daftar Izin/Daftar Blokir IP
1. Pilih **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **playback domain** (domain pemutaran ulang) target atau klik **Manage** (Kelola) di sebelah kanan untuk masuk ke halaman manajemen domain.
2. Klik **Access Control** (Kontrol Akses) dan, di area **IP Allowlist/Blocklist** (Daftar Izin/Daftar Blokir IP), klik **Edit**.
3. Modifikasi konfigurasi, lalu klik **Save** (Simpan).
![](https://qcloudimg.tencent-cloud.cn/raw/f60c0cdf3fe6cb94f15867f349bc4cc3.png)

[](id:close)
## Menonaktifkan Daftar Izin/Daftar Blokir IP
Ikuti langkah-langkah di bawah ini untuk menonaktifkan daftar izin/daftar blokir IP:
1. Pilih **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **playback domain** (domain pemutaran ulang) target atau klik **Manage** (Kelola) di sebelah kanan untuk masuk ke halaman manajemen domain.
2. Klik **Access Control** (Kontrol Akses), lalu temukan **IP Allowlist/Blocklist** (Daftar Izin/Daftar Blokir IP).
3. Klik ![img](https://main.qcloudimg.com/raw/e72f89a0deb6858428dc3e93ce7e7088.png) untuk menonaktifkan daftar izin/daftar blokir IP.
![](https://qcloudimg.tencent-cloud.cn/raw/226d47604696996735ec23b887931d35.png)
