## Kasus Penggunaan
Tabel berikut memerinci kasus penggunaan CDN.Anda dapat mengeklik untuk melihat detailnya.

<table  style="width:890">
<thead>
<tr>
<th scope="col" style="width: 100px;">Kasus Penggunaan</th>
<th scope="col">Deskripsi</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href = "#m1">Akselerasi situs web</a></td>
<td >CDN memberikan kemampuan penayangan dipercepat untuk konten statis, seperti halaman web, gambar, dan file-file kecil dalam konteks bisnis, seperti portal web, ecommerce, dan komunitas UGC sehingga meningkatkan pengalaman pengguna secara signifikan. </td>
</tr>
<tr>
<td><a href = "#m2">Akselerasi unduhan</a></td>
<td >CDN memberikan akselerasi unduhan yang stabil dan berkualitas tinggi untuk game, aplikasi, atau paket penginstalan ROM.</td>
</tr>
<tr>
<td><a href = "#m3">Akselerasi Audio/Video</a></td>
<td>Didukung oleh pengalaman Tencent yang matang dalam mengoperasikan video online, CDN dapat mengelola permintaan sekaligus dalam jumlah sangat besar untuk pemutaran ulang audio dan video online selama jam-jam sibuk sehingga secara efektif menjamin ketersediaan layanan dan kecepatan transfer media yang tinggi sambil tetap memberikan pengalaman menonton yang stabil, lancar, dan kaya. </td>
</tr>
<tr>
<td><a href = "#m4">ECDN</a></td>
<td >Enterprise Content Delivery Network (ECDN) merupakan produk Tencent Cloud yang berdiri sendiri untuk akselerasi sumber daya dinamis atau dinamis-statis yang lengkap dan serbaada.ECDN dapat otomatis mengidentifikasi sumber daya dinamis dan statis sambil tetap mengimplementasikan akselerasi serentak untuk semua jenis sumber daya di satu platform saja. </td>
</tr>
<tr>
<td><a href = "#m5">SCDN</a></td>
<td >Tencent Cloud SCDN memberikan kemampuan perlindungan keamanan yang mumpuni di luar semua keunggulan akselerasi CDN.Tencent Cloud SCDN dapat membentengi diri dari serangan DDoS bertubi-tubi dan serangan CC besar-besaran serta memberikan WAF dari intrusi situs web.Anda dapat dengan cepat terkoneksi dan mengaktifkan SCDN di CDN.</td>
</tr>
</tbody>
</table>
## Deskripsi Kasus Penggunaan
<span ID = "m1"></span>
### Akselerasi situs web
Akselerasi situs web itu cocok untuk semua jenis situs web, seperti portal web, platform ecommerce, dan komunitas UGC.CDN dapat meng-cache dan mempercepat penayangan konten statis di situs web Anda.Untuk mempercepat konten dinamis, gunakan [ECDN](https://intl.cloud.tencent.com/product/ecdn).

<blockquote class="d-mod-explain">
<div class="d-mod-title d-explain-title">
<i class="d-icon-explain"></i>Apa itu konten statis dan dinamis?
</div>
<p></p>
<ul>
<li>Konten statis merujuk pada konten yang tetap sama ketika diminta. <br>Contoh: .html, .css, dan berupa file, gambar, video, paket penginstalan perangkat lunak, file APK, dan file kompresi.</li>
<li>Konten dinamis merujuk pada konten yang berubah-ubah ketika diminta. <br>Contoh:API dan file .jsp, .asp, .php, .perl, dan .cgi.</li>
</ul>
</blockquote>
CDN memberikan kemampuan penayangan konten statis yang mumpuni sehingga secara signifikan mempercepat pemuatan halaman dan menghadirkan pengalaman penjelajahan yang lancar dan cepat untuk pengguna akhir yang tersebar lokasi geografinya.Selama jam-jam sibuk layanan ketika pengguna dalam jumlah besar sama-sama aktif, CDN dapat mengurangi tekanan pada server asal sehingga bisa menjamin akses yang stabil dan lancar ke layanan dan halaman web.
![](https://main.qcloudimg.com/raw/c2291b131ce33d1eb39ec35167453437.png)


<span ID = "m2"></span>
### Akselerasi unduhan
Akselerasi unduhan ini cocok untuk mempercepat pengunduhan berbagai file, seperti game, aplikasi, dan paket penginstalan ROM

Ditopang oleh cadangan bandwidth elastis dalam jumlah sangat besar, CDN dapat mengatasi gelombang lalu lintas dan mempercepat pengunduhan file-besar sehingga menjamin stabilitas layanan dan memberikan pengalaman unduhan yang efisien bagi semua pengguna akhir.
![](https://main.qcloudimg.com/raw/ada400d5a04d58fb73662e6bc028232c.png)


<span ID = "m3"></span>
### Akselerasi Audio/Video
Akselerasi Audio/video ini cocok untuk berbagai jenis situs web dan aplikasi audio/video sesuai permintaan, seperti aplikasi audio/video, platform audio/video online, dan IPTV.Berbekal kemampuan penayangan yang lebih baik dan dukungan pengalaman Tencent yang matang dalam mengoperasikan video online, Tencent Cloud CDN secara efektif dapat menjamin pemutaran ulang audio/video yang lancar untuk semua pengguna akhir selama jam-jam sibuk dengan permintaan serentak dalam jumlah sangat besar.
![](https://main.qcloudimg.com/raw/0e852cfff1cd2f131f3ab1256a5b3a51.png)


<span ID = "m4"></span>
### ECDN
[ECDN](https://intl.cloud.tencent.com/product/ecdn) ini cocok untuk situs web dan aplikasi dengan sumber daya hibrida dinamis/statis atau sumber daya dinamis dalam jumlah besar, seperti file .asp, .jsp, .php, .cgi., dan .perl, API, dan permintaan interaksi database.

ECDN, saat ini berupa produk yang berdiri sendiri, dapat menghadirkan pengalaman akselerasi yang berperforma tinggi dan satu atap kepada pengguna akhir melalui integrasi caching edge statis dengan pengoptimalan rute tarik-asal dinamis, penjadwalan permintaan secara cerdas pada simpul layanan optimal, identifikasi otomatis sumber daya statis dan dinamis, dan pemanfaatan algoritme kalkulasi rute optimal milik Tencent serta teknologi pengoptimalan TCP, .
![](https://main.qcloudimg.com/raw/a6f7d54e98720a3d4a18d673fc1f9b4c.png)

<span ID = "m5"></span>

### SCDN
SCDN ECDN, saat ini berupa produk yang berdiri sendiri, dapat menghadirkan pengalaman akselerasi yang berperforma tinggi dan satu atap kepada pengguna akhir melalui integrasi caching edge statis dengan pengoptimalan rute tarik-asal dinamis, penjadwalan permintaan secara cerdas pada simpul layanan optimal, identifikasi otomatis sumber daya statis dan dinamis, dan pemanfaatan algoritme kalkulasi rute optimal milik Tencent serta teknologi pengoptimalan TCP, .
SCDN dibangun pada CDN sehingga Anda tidak perlu menggarap kembali konfigurasi DNS.Perlindungan keamanan jaringan dapat diaktifkan dengan cepat untuk nama-nama domain yang dipercepat oleh CDN.
![](https://main.qcloudimg.com/raw/164d28b237eb5dbe05a57b631d98616e.png)



​	