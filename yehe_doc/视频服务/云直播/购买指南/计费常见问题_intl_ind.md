## Penagihan CSS

[](id:live_que1)
### Apa saja item CSS yang dapat dikenai tagihan? Bagaimana cara mengetahui biaya apa saja yang harus saya bayar?
Item CSS yang dapat dikenai tagihan meliputi layanan dasar dan layanan dengan nilai tambah. Biaya layanan tambahan akan dikenakan jika fitur bernilai tambah yang disediakan bersama oleh CSS dan layanan lain Tencent Cloud digunakan.

- **Biaya layanan dasar**: ditagih berdasarkan lalu lintas/bandwidth downstream yang dihasilkan dengan menghubungkan pengguna ke server asal cache. Dengan kata lain, biaya lalu lintas/bandwidth akan dikenakan selama konten streaming langsung Anda ditonton oleh pemirsa.
>?CSS menyediakan dua opsi mode penagihan, yaitu tagihan berdasarkan lalu lintas dan tagihan berdasarkan bandwidth. Detail harga dapat dilihat di “Bill-by-Traffic/Bandwidth” (Tagihan Berdasarkan Lalu Lintas/Bandwidth) di [Billing Overview (Ikhtisar Penagihan)](https://intl.cloud.tencent.com/document/product/267/2818#bill-by-traffic.2Fbandwidth). Untuk beralih mode penagihan, lihat [Changing Billing Modes (Beralih Mode Penagihan)](https://intl.cloud.tencent.com/document/product/267/30411).
- **Biaya layanan dengan nilai tambah**: layanan ini meliputi transcoding, perekaman, pengambilan tangkapan layar, dan deteksi pornografi, yang semuanya dinonaktifkan secara default. Anda akan dikenai biaya jika mengaktifkan dan menggunakan layanan tersebut. Detail harga dapat dilihat di “Value-Added Service Fees” (Biaya Layanan dengan Nilai Tambah) di [CSS Pricing Overview (Ikhtisar Harga CSS)](https://intl.cloud.tencent.com/document/product/267/2819#value-added-service-fees).
- **Biaya layanan tambahan**: layanan dengan nilai tambah yang disediakan bersama oleh CSS dan layanan lain Tencent Cloud serta dikenai biaya sesuai dengan aturan penagihan layanan terkait. Penggunaan layanan tersebut akan dikenai biaya layanan tambahan. Detail harga dapat dilihat di “Extended Service Fees” (Biaya Layanan Tambahan) di [CSS Pricing Overview (Ikhtisar Harga CSS)](https://intl.cloud.tencent.com/document/product/267/2819#extended-service-fees).

[](id:live_que2)
### Bagaimana cara mengetahui jika akun saya memiliki pembayaran yang sudah melewati jatuh tempo?
Anda dapat login ke [konsol CSS](https://console.cloud.tencent.com/live), lalu mengeklik **Billing Center** (Pusat Penagihan) di kanan atas untuk masuk ke halaman “Account Info” (Informasi Akun). Akun Anda memiliki pembayaran yang sudah lewat jatuh tempo jika saldo yang tersedia kurang dari 0 USD. Agar Anda dapat terus menggunakan CSS dan layanan lainnya, harap selesaikan pembayaran yang sudah melewati jatuh tempo dengan mengisi ulang saldo akun Anda.

[](id:live_que3)
### Apakah saya akan dikenai biaya untuk push upstream?
- Secara default, biaya ditagihkan berdasarkan penggunaan downstream. Akan tetapi, penggunaan upstream juga akan dikenai tagihan jika rasio penggunaan upstream terhadap penggunaan downstream lebih dari 1:10 dan bandwidth puncak upstream harian melampaui 100 Mbps.
- Penggunaan upstream akan dikenai tagihan sesuai dengan mode penagihan dan aturan harga bertingkat yang sama dengan penggunaan downstream. **Aturan penagihan untuk penggunaan upstream telah diterapkan sejak pukul 00.00 tanggal 1 Juli 2021**.

[](id:live_que4)
### Kapan biaya layanan dengan nilai tambah mulai ditagih?
Setelah layanan bernilai tambah yang terikat dengan nama domain push, misalnya perekaman, pengambilan tangkapan layar, deteksi pornografi, dan pemberian watermark, diaktifkan, biaya akan dikenakan saat push dimulai. Setelah layanan bernilai tambah yang terikat dengan nama domain pemutaran ulang, misalnya transcoding, diaktifkan, biaya akan dikenakan saat pemutaran ulang dimulai. Jika Anda membuat templat transcoding dan mengikatkannya dengan nama domain pemutaran ulang, biaya transcoding tidak akan dikenakan jika tidak ada pemutaran ulang. Pengaktifan pemberian watermark atau pencampuran streaming dapat dikenai biaya transcoding standar, yang akan ditagihkan berdasarkan resolusi streaming langsung output.



## Penagihan Transcoding

[](id:tran_que1)
### Bagaimana penagihan biaya transcoding langsung dilakukan? Bagaimana cara memperkirakan biaya transcoding?
Transcoding langsung dikenai tagihan berdasarkan codec transcoding, resolusi, dan durasi terkait. Saat pencampuran streaming dan pemberian watermark diproses di modul transcoding, penggunaan fitur-fitur tersebut juga akan dikenai biaya transcoding. Informasi selengkapnya dapat dilihat di [Transcoding Billing (Penagihan Transcoding)](https://intl.cloud.tencent.com/document/product/267/39604).
Jika streaming langsung yang sama ditonton oleh beberapa pemirsa dengan bitrate yang sama, biaya transcoding hanya akan ditagih satu kali.

**Contoh:** Anda menggunakan transcoding langsung dan pemberian watermark langsung pada tanggal 1 Januari 2021 untuk transcoding streaming langsung A menjadi `H.264_720P` selama 1 jam dan pemberian watermark streaming langsung B dengan 480p selama 30 menit.
Biaya transcoding yang harus Anda bayar pada tanggal 2 Januari 2021 adalah 0,0057 (USD/menit) × 60 (menit) + 0,0028 (USD/menit) × 30 (menit) = 0,426 USD.

[](id:tran_que2)
### Mengapa muncul tagihan transcoding padahal saya tidak menggunakan transcoding langsung?
Layanan transcoding langsung meliputi transcoding real-time langsung, pencampuran streaming, dan pemberian watermark. Penggunaan pencampuran streaming atau pemberian watermark juga akan dikenai biaya transcoding.

[](id:tran_que3)
### Apakah pencampuran streaming langsung pasti akan dikenai biaya transcoding?
Ya. Biaya transcoding akan ditagih berdasarkan streaming langsung output setelah pencampuran streaming. Karena sumber daya transcoding akan terpakai setelah pencampuran streaming berhasil, durasi pencampuran streaming akan digunakan untuk penagihan, baik untuk streaming yang diputar ulang maupun yang tidak. Hal ini berbeda dengan transcoding biasa, yang dikenai tagihan berdasarkan durasi pemutaran ulang.



## Penagihan Perekaman Langsung
[](id:record_que1)
### Bagaimana penagihan biaya perekaman langsung dilakukan?
Perekaman langsung dikenai tagihan berdasarkan jumlah puncak saluran perekaman bersamaan pada bulan berjalan, dan jumlah total saluran perekaman dalam suatu periode statistik merupakan puncak saluran bersamaan. Satu streaming langsung yang direkam dalam satu format file dihitung sebagai satu saluran perekaman. Jika Anda merekam dalam dua format (MP4 dan HLS), keduanya akan dihitung sebagai dua saluran perekaman.

[](id:record_que2)
### Bagaimana cara menghitung puncak saluran perekaman langsung?
Ketika satu streaming langsung (satu ID streaming) direkam dalam satu format file, streaming tersebut akan dihitung sebagai satu saluran perekaman langsung. Kueri terkait jumlah saluran perekaman saat ini akan dibuat satu kali setiap 5 menit, dan nilai maksimum titik sampel pada bulan berjalan akan digunakan sebagai puncak saluran perekaman bulanan untuk penagihan.
**Contoh:**

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">ID Streaming</th>
<th rowspan=2 width="10%" style="text-align:center;">File Rekaman<br> Format</th>
<th colspan=7 width="50%" style="text-align:center;">Bulan Berjalan (Hari Ke-1 Sampai Ke-30)</th>
</tr><tr>
<td style="text-align:center;">Hari Ke-1</td><td style="text-align:center;">Hari Ke-2</td><td style="text-align:center;">Hari Ke-3</td>
<td style="text-align: center; ">…</td>
<td style="text-align:center;">Hari Ke-28</td><td style="text-align:center;">Hari Ke-29</td><td style="text-align:center;">Hari Ke-30</td>
</tr><tr>
<td rowspan=4 style="text-align:center;">A</td>
<td style="text-align:center;">HLS</td><td></td><td></td><td></td>
<td rowspan=13 style="text-align:center;">Perekaman tidak digunakan</td>
<td id="ye"></td><td id="ye"></td>
<td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td>
</tr><tr>
<td rowspan=4 style="text-align:center;">B</td>
<td style="text-align:center;">HLS</td><td></td><td id="gr"></td><td id="gr"></td><td id="gr"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td id="gr"></td><td id="gr"></td><td></td><td id="gr"></td><td id="gr"></td><td></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td></td><td id="gr"></td><td></td><td id="gr"></td><td></td><td id="gr"></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td></td><td id="gr"></td><td></td><td id="gr"></td><td></td><td></td>
</tr><tr>
<td rowspan=4 style="text-align:center;">C</td>
<td style="text-align:center;">HLS</td><td id="br"></td><td></td><td id="br"></td><td id="br"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td></td><td></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td></td><td></td><td></td><td id="br"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td></td><td></td><td></td><td></td><td></td><td id="br"></td>
</tr><tr>
<td colspan=2 style="text-align:center;">Saluran Perekaman</td>
<td style="text-align:center;">5</td><td style="text-align:center;">7</td><td style="text-align:center;">6</td><td style="text-align:center;">11</td><td style="text-align:center;">6</td><td style="text-align:center;">5</td>
</tr><tr>
<td colspan=2 style="text-align:center;">Puncak Saluran Perekaman</td><td colspan=7 style="text-align:center;">11</td>
</tr>
</table>

>? 
>- Kuning: tugas perekaman dengan ID streaming **A**.
>- Hijau: tugas perekaman dengan ID streaming **B**.
>- Biru: tugas perekaman dengan ID streaming **C**.




[](id:record_que3)
### Mengapa saya dikenai biaya sebesar 10,5882 USD setelah menggunakan perekaman langsung? 
Jika dua streaming langsung direkam secara bersamaan atau satu streaming langsung direkam menjadi dua format file, dua saluran perekaman akan dibuat. Perekaman langsung dikenai tagihan berdasarkan puncak saluran perekaman dengan harga 5,2941 USD per saluran per bulan sehingga jika ada dua saluran dalam satu bulan, biaya sebesar 10,5882 USD akan dikenakan. Informasi selengkapnya dapat dilihat di [Live Recording Billing (Penagihan Perekaman Langsung)](https://intl.cloud.tencent.com/document/product/267/39605).
Anda sebaiknya membuka **Bill Details** > **[Bill by Instance](https://console.cloud.tencent.com/expense/bill/summary)** (Detail Tagihan > Tagihan Berdasarkan Instans) di Billing Center (Pusat Penagihan) untuk melihat detail penagihan perekaman langsung. Anda dapat mengeklik **Bill Details** (Detail Tagihan) di kolom "Operation" (Operasi) untuk melihat puncak saluran perekaman aktual bulan sebelumnya.

