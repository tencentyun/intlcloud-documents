Perkembangan teknologi audio-visual kian canggih dan mendorong pertumbuhan yang sangat pesat di industri siaran langsung di seluruh dunia. Perusahaan internet Tiongkok memanfaatkan pengalaman globalisasi sebelumnya dari berbagai perusahaan sektor layanan dan memasuki pasar global secara bersama-sama. Berbagai platform terkemuka menjual produk dengan merambah pasar internasional demi meningkatkan daya saing, sedangkan platform-platform kecil terus mencari peluang baru setelah menyadari sulitnya bertahan di tengah persaingan dalam negeri yang keras. Akan tetapi, kompetisi di tingkat global pun tidak kalah sengit. Tiga (3) perusahaan raksasa, YouTube, Periscope, dan Facebook, mungkin telah menguasai pasar dengan nilai melebihi pangsa pasar wajar masing-masing. Namun demikian, masih tersisa persentase yang besar dan belum tersentuh untuk platform kecil dan sedang. Tencent Cloud terus memperkuat cadangan sumber daya siaran langsung global dan mengoptimalkan performa akselerasi siaran langsung dengan tujuan membantu platform siaran langsung untuk menguasai pasar internasional.
![](https://main.qcloudimg.com/raw/220512d9f3ec1cdaa7b2f04c7b1e6150.png) 

Selain push dan pemutaran ulang, layanan siaran langsung yang lengkap juga harus menyediakan autentikasi, transcoding, pengambilan tangkapan layar, perekaman, panggilan balik, deteksi pornografi, DRM, dan fitur-fitur lainnya. Gambar berikut menampilkan berbagai modul fitur dasar solusi CSS Global Tencent Cloud.  

![](https://main.qcloudimg.com/raw/057d12ecc304f5e64918536ff2871035.png)


Fitur dasar siaran langsung global secara umum sama dengan fitur dasar siaran langsung domestik. Akan tetapi, siaran langsung global memiliki lebih banyak tantangan. Hal ini disebabkan terutama oleh area geografi yang lebih luas, lingkungan jaringan yang lebih kompleks, dan kualitas jaringan lintas batas yang lebih rendah. Untuk mengurangi latensi dan lag serta meningkatkan stabilitas dan keandalan layanan, Tencent Cloud telah mengoptimalkan **arsitektur, jaringan, keamanan, dan sumber daya** CSS untuk skenario siaran langsung global.

<span id="deploy"></span>
### Deployment Beberapa Node Pusat
**Tencent Cloud telah membangun banyak sekali IDC pusat di Hong Kong (Tiongkok), Thailand, Singapura, Jerman, Toronto, Silicon Valley, Rusia, Afrika Selatan, dan Korea Selatan serta terus memperluas pembangunan ke lebih banyak negara dan wilayah.** IDC pusat ini meng-hosting semua modul yang diperlukan untuk siaran langsung global dan di-deploy secara merata dengan arsitektur yang terdesentralisasi agar dapat melayani pengguna akhir global dengan lebih baik dan menjamin failover yang cepat jika terjadi perkecualian IDC. Dengan mempertimbangkan dampak rendahnya kualitas dan stabilitas jaringan lintas batas terhadap latensi dan lag siaran langsung, interkoneksi node pusat dilakukan melalui Direct Connect. Interkoneksi node pusat Tiongkok Daratan dilakukan dengan node pusat di luar Tiongkok Daratan melalui lini Direct Connect dengan node Hong Kong sebagai relai. Detail arsitektur dapat dilihat di gambar berikut:
![](https://main.qcloudimg.com/raw/db15dda3beb4c7015c5c9505e0164756.png)
Untuk menunjukkan performa akselerasi node pusat mancanegara dengan jelas, kami membandingkan statistik pengguna akhir Tiongkok yang menonton streaming langsung AS. Seperti yang dapat Anda lihat di grafik berikut, akselerasi melalui Direct Connect mempertahankan tingkat lag tetap rendah dan jaringan tetap stabil.
![](https://main.qcloudimg.com/raw/4eedf1119b50fda15f83b0bafcbccf0d.png)

<span id="speed"></span>
### Akselerasi di Wilayah Edge
Node pusat dapat memenuhi semua kebutuhan pengguna akhir lokal, tetapi kebutuhan pengguna akhir di negara dan wilayah tanpa node pusat juga harus dipenuhi. Karena berbagai pembatasan, tidak ada node pusat yang dibangun di wilayah tersebut sehingga diperlukan node cache. Negara dan wilayah tersebut disebut wilayah edge. Kualitas jaringan lintas batas di wilayah ini relatif rendah dan tingkat lag pull lintas wilayahnya cukup tinggi. Contoh wilayah edge meliputi Malaysia, Indonesia, Timur Tengah, India, Afrika, dan Amerika Selatan. Untuk wilayah-wilayah edge ini, Tencent Cloud menetapkan prioritas untuk modul layanan. Prioritas pertama adalah memastikan bahwa pengguna lokal yang sah dapat menonton streaming langsung tanpa membutuhkan transmisi lintas batas untuk data lokal. Layanan modul lain ditarik ulang dari server edge ke node pusat dan terakhir diterapkan pada node pusat. **Seperti yang dapat dilihat di grafik berikut, setelah akselerasi node lokal diaktifkan di wilayah edge, tingkat lag berkurang secara signifikan dan performa akselerasi jauh lebih tinggi daripada performa akselerasi penyedia layanan lain di industri yang sama.**
![](https://main.qcloudimg.com/raw/590d25023541030ee6266e862a75cc73.png)

<span id="disaster_tolerance"></span>
### Akses dan Failover Optimal
Seperti halnya Tiongkok Daratan, wilayah-wilayah lain juga sering kali memiliki banyak ISP, seperti DTAC, AIS, dan TURE di Thailand; Chunghwa Telecom, Taiwan Mobile, dan so-net di Taiwan (Tiongkok); serta Telkomsel, XL, dan INDOSAT di Indonesia. Kecepatan akses lintas ISP bergantung pada bandwidth dan sumber daya. Untuk meningkatkan pengalaman akses pengguna akhir di jaringan yang dioperasikan oleh berbagai ISP, sistem penjadwalan Tencent Cloud memungkinkan pengguna akhir untuk mengakses ISP masing-masing. Selain itu, node cache yang dibangun secara lokal biasanya mengandalkan lini BGP untuk akses dan pemasangan tautan dengan ISP lokal.
Sebagai contoh, untuk pengguna akhir tiga ISP (DTAC, AIS, dan TURE) di Thailand, sistem penjadwalan pusat mengumpulkan informasi IP dan ISP dalam jumlah besar dan secara otomatis menjadwalkannya ke node CDN terdekat berdasarkan IP, dengan akurasi pengenalan lebih dari **99,5%**. Peralihan antarpusat data dengan perkecualian juga didukung. Jika node pemantauan dan deteksi menemukan perkecualian di suatu wilayah, sistem akan secara otomatis beralih ke pusat data yang paling optimal.
![](https://main.qcloudimg.com/raw/e4725d92c9d6adcd3df0cb9a6fa29793.png)

<span id="net"></span>
### Pengoptimalan Transmisi Jaringan
Ketika streaming langsung ditransmisikan ke jaringan mancanegara, metode transmisi TCP biasa tidak dapat menjamin latensi transmisi yang rendah. Karena jarak transmisi mancanegara yang jauh, pembatasan bandwidth jalur keluar internasional, dan kualitas jaringan yang sering fluktuatif, TCP tidak cocok untuk transmisi data mancanegara karena peningkatan (upgrade) dan pengoptimalannya memakan waktu lebih lama serta tingkat kehilangan paket lebih tinggi. Tencent Cloud menggunakan Quick UDP Internet Connections (QUIC) untuk meningkatkan keandalan transmisi data di jaringan mancanegara. Akselerasi proksi data lapisan atas dengan QUIC diterapkan di lapisan aplikasi. Artinya, penyesuaian yang tepat pada parameter atau algoritme kemacetan dapat diterapkan seketika sehingga dapat memperbaiki latensi yang tinggi dan tingkat kehilangan paket yang tinggi, mencegah kemacetan, dan mengurangi waktu round-trip (RTT) secara efisien. **Pengujian dengan data aktual menunjukkan bahwa skema hasil optimasi Tencent Cloud mengurangi waktu koneksi sebesar 40% dan tingkat lag sebesar 20% secara rata-rata dibandingkan dengan skema TCP pada umumnya.**
![](https://main.qcloudimg.com/raw/95c2367e21cbfea268617aff354d1b9d.png)

Grafik berikut menunjukkan perbandingan lag untuk pemirsa global yang menonton streaming langsung yang di-push oleh host di UEA ke node cache UEA. Anda dapat melihat bahwa lag terlihat tetap rendah ketika streaming dipercepat melalui QUIC.
![](https://main.qcloudimg.com/raw/02fe6d2f5cfe7d1c496446811d64548c.png)

<span id="reserve"></span>
### Cadangan Sumber Daya Massal
Selain berbagai arsitektur dan solusi teknis, cadangan sumber daya juga sangat penting bagi layanan siaran langsung. Tanpa dukungan sumber daya global, semua teknologi hanya sekadar teori. Tencent Cloud telah menerapkan strategi globalisasi dan melakukan investasi jangka panjang di pasar mancanegara. Seperti yang dapat dilihat di bagan distribusi node global Tencent Cloud di awal dokumen ini, **Tencent Cloud telah membangun lebih dari 2.000+ node transmisi di lebih dari 50 negara dan wilayah, dengan total bandwidth sebesar 100+ Tbps di 50+ mitra ISP global dan 1.000+ node cache mancanegara.** Selain itu, Tencent Cloud bekerja sama dengan banyak ISP di wilayah yang sama untuk memastikan ada sedikitnya 3 salinan data cadangan pemulihan bencana yang tersedia di setiap jalur keluar demi menjamin stabilitas dan keandalan layanan. Informasi selengkapnya dapat dilihat di [CDN](https://intl.cloud.tencent.com/document/product/228/2941?from_cn_redirect=1#nodes-outside-mainland-china)

<span id="open"></span>
### Cara Mengaktifkan
Layanan CSS Global dapat diaktifkan langsung di [konsol CSS](https://console.cloud.tencent.com/live).
- Jika belum memiliki akun Tencent Cloud, Anda perlu mendaftar terlebih dahulu sesuai dengan petunjuk di [Signing up for a Tencent Cloud Account] (Membuat Akun Tencent Cloud)](https://intl.cloud.tencent.com/document/product/378/17985), lalu [mengirimkan permohonan aktivasi layanan CSS)](https://intl.cloud.tencent.com/document/product/267/30410).
- Jika sudah memiliki akun Tencent Cloud dan sudah mengaktifkan CSS, Anda dapat langsung melanjutkan ke langkah berikutnya.

Buka konsol CSS, pilih **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain) di bilah sisi kiri, lalu klik **Add Domain** (Tambahkan Domain).
![](https://qcloudimg.tencent-cloud.cn/raw/e0131c5904b8e2a8c20034b10fb7127b.png)

Di jendela pop-up, pilih jenis sebagai **Playback Domain** (Domain Pemutaran Ulang), pilih **Acceleration Region** (Wilayah Akselerasi) yang sesuai, lalu masukkan **Domain Name** (Nama Domain) yang perlu dipercepat.
