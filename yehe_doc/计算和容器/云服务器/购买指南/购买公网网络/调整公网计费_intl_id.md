>? Mode berlangganan bulanan saat ini dalam versi beta. Harga yang dipublikasikan di sini hanya untuk referensi. Lihat tagihan Anda untuk harga akhir. Untuk menggunakan opsi penagihan ini, harap [hubungi penjualan](https://intl.cloud.tencent.com/contact-sales).
>

## Menyesuaikan Bandwidth Jaringan Publik

<table>
<tr><th>Mode Penagihan Jaringan</th><th>Mode Penagihan CVM</th><th>Menyesuaikan Bandwidth</th></tr>
<tr><td>Langganan bandwidth bulanan</td><td>Langganan bulanan</td><td>Hanya mendukung upgrade bandwidth, dan Anda memiliki opsi untuk mengatur perubahan agar segera diterapkan atau pada waktu tertentu.</td></tr>
<tr><td rowspan=2>Tagihan per lalu lintas</td><td>Langganan bulanan</td><td rowspan=2>Bandwidth dapat diupgrade atau didowngrade, dan perubahan akan segera diterapkan. Biaya jaringan dihitung berdasarkan penggunaan lalu lintas. </td></tr>
<tr><td>Bayar sesuai pemakaian</td></tr>
</table>

## Mengubah Mode Penagihan

<table>
<tr><th>Mode Penagihan Jaringan</th><th>Mode Penagihan CVM</th><th>Mengubah Mode Penagihan Jaringan</th></tr>
<tr><td>Langganan bandwidth bulanan</td><td>Langganan bulanan</td><td>Tidak didukung.</td></tr>
<tr><td rowspan=2>Tagihan per lalu lintas</td><td>Langganan bulanan</td><td>Mendukung perubahan permanen pada langganan bandwidth bulanan untuk setiap CVM.</td></tr>
<tr><td>Bayar sesuai pemakaian</td><td>Tidak didukung.</td></tr>
</table>


## Contoh Penagihan

Harga satuan bandwidth tercantum di [Penagihan Jaringan Publik](https://intl.cloud.tencent.com/zh/document/product/213/10578).
>? Contoh ini hanya menghitung biaya jaringan. CVM dan biaya perangkat lainnya akan ditentukan secara terpisah.

### Menyesuaikan bandwidth

#### Mengupgrade bandwidth untuk **Monthly bandwidth subscription** (Langganan bandwidth bulanan)

Misal Anda membeli bandwidth langganan bulanan sebesar 2 Mbps untuk satu instans CVM di wilayah Beijing pada 1 November 2018. Anda mengupgrade bandwidth dari 2 Mbps menjadi 5 Mbps antara 20 dan 29 November 2018 dengan total 10 hari.![](https://main.qcloudimg.com/raw/a8ea05b86a9c2e5bda630928585acbe5.png)
Biaya bandwidth yang harus dibayar untuk langganan bandwidth bulanan awal di bulan November adalah: bandwidth \* harga satuan = 2Mbps \* 2,86 USD/Mbps = 5,72 USD
Biaya tambahan setelah peningkatan bandwidth: perbedaan bandwidth sebelum dan sesudah upgrade \* jumlah hari dengan bandwidth yang diupgrade/hari pembebanan biaya dalam sebulan (jumlah hari dalam beberapa bulan) = (3,57 USD/Mbps \* 3 Mbps + 2,86 USD/Mbps \* 2Mbps - 2,86 USD/Mbps \* 2Mbps) \* 10 hari/30 hari = 3,57 USD

#### Mengupgrade atau mendowngrade bandwidth untuk **bill-by-traffic** (tagihan per lalu lintas)

Anda dapat menyesuaikan batas bandwidth untuk instans CVM tagihan per lalu lintas tanpa biaya tambahan kapan saja Anda membutuhkannya. Jaringan publik dibebankan pada lalu lintas yang sebenarnya.

### Mengubah penagihan jaringan publik

#### Mengubah dari **bill-by-traffic** (tagihan per lalu lintas) menjadi **monthly bandwidth subscription** (langganan bandwidth bulanan)

Biaya lalu lintas akan ditentukan setiap jam pada saat perubahan. Untuk mengubah opsi penagihan, Anda hanya perlu membayar biaya langganan bandwidth bulanan.