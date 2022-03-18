Tencent Cloud menyediakan citra publik Linux dengan konfigurasi default, tetapi sebaiknya konfigurasi `sysctl` secara terpisah untuk beradaptasi dengan bisnis spesifik Anda. Dokumen ini menjelaskan konfigurasi citra publik Tencent Cloud Linux secara default dan optimal dan membantu Anda menyesuaikannya secara manual sesuai kebutuhan.
>?
>- Parameter yang dinyatakan sebagai “-” di bawah **Initial Configuration** (Konfigurasi Awal) menggunakan konfigurasi default citra resmi.
>- Perintah `sysctl -w` hanya membuat konfigurasi berlaku sementara, sedangkan parameter yang ditulis ke `/etc/sysctl.conf` berlaku secara permanen.


### Terkait jaringan
<table>
<tr>
<th>Parameter</th><th>Deskripsi</th><th>Konfigurasi Awal</th>
</tr>
<tr>
<td><code>net.ipv4.tcp_tw_recycle</code></td>
<td>Parameter ini digunakan untuk mendaur ulang koneksi TIME_WAIT dengan cepat. Jika diaktifkan, kernel akan memeriksa stempel waktu paket.<br>Sebaiknya jangan mengaktifkan parameter ini, karena bisa saja kehilangan paket saat stempel waktu tidak meningkat secara monoton. Parameter ini tidak digunakan di versi kernel yang lebih baru.</td>
<td>0</td>
</tr>
<tr>
<td><code>net.core.somaxconn</code></td>
<td>Parameter ini digunakan untuk menentukan status ESTABLISH di akhir handshake tiga arah saat tidak ada antrean ACCEPT. Antrean ACCEPT yang lebih panjang menunjukkan tingkat pemrosesan klien yang rendah, atau lonjakan koneksi baru dalam waktu singkat. Mengatur <code>net.core.somaxconn</code> terlalu rendah dapat menyebabkan hilangnya paket karena koneksi SYN baru akan dibuang saat server menerima paket SYN dan tabel somaxconn penuh. Mengaturnya terlalu tinggi hanya diperlukan untuk layanan konkurensi tinggi, tetapi latensinya dapat meningkat.
</td>
<td>128</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_max_syn_backlog</code></td>
<td>Parameter ini menentukan jumlah maksimal koneksi dalam antrean SYN_RECV, yang pernah digunakan untuk mempertahankan serangan synflood umum. Namun, jika <code>tcp_syncookies=1</code>, koneksi dalam antrean SYN_RECV akan melebihi batas atas.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_syncookies</code></td>
<td>Parameter ini digunakan untuk mengaktifkan Cookie SYN, yang mencegah beberapa serangan SYN. Jika diaktifkan, koneksi masih dapat dibuat saat antrean SYN dipenuhi. Namun, SHA1 akan digunakan untuk memverifikasi Cookie, yang secara teoritis meningkatkan penggunaan CPU.</td>
<td>1</td>
</tr>
<tr>
<td><code>net.core.rmem_default</code><br>
<code>net.core.rmem_max</code><br>
<code>net.ipv4.tcp_mem</code><br>
<code>net.ipv4.tcp_rmem</code>
</td>
<td>Parameter ini digunakan untuk mengonfigurasi ukuran cache dari data yang diterima. Mengatur parameter ini terlalu tinggi dapat membuang sumber daya memori, sementara mengaturnya terlalu rendah dapat menyebabkan hilangnya paket. Anda dapat mengaturnya sesuai dengan konkurensi dan throughput bisnis Anda.<ul><li>rmem_default: konfigurasi optimal secara teoritis sama dengan nilai bandwidth dibagi RTT, yang akan menimpa konfigurasi tcp_rmem dan tcp_rmem </li><li>rmem_max: kira-kira lima kali rmem_default</li><li>tcp_mem: total memori TCP yang digunakan, yang secara otomatis diatur ke 3/32, 1/8, atau 3/16 dari memori CVM yang tersedia. Parameter tcp_mem dan rmem_default juga menentukan jumlah maksimum koneksi bersamaan.</li></ul></td>
<td><code>rmem_default<br>=655360</code><br>
<code>rmem_max<br>=3276800</code></td>
</tr>
<tr>
<td><code>net.core.wmem_default</code><br>
<code>net.core.wmem_max</code><br>
<code>net.ipv4.tcp_wmem</code>
</td>
<td>Parameter ini digunakan untuk mengonfigurasi cache transmisi data. Pengiriman data di Tencent Cloud biasanya tidak mengalami kemacetan, jadi konfigurasi ini bersifat opsional.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_keepalive_intvl</code><br>
<code>net.ipv4.tcp_keepalive_probes</code><br>
<code>net.ipv4.tcp_keepalive_time</code>
</td>
<td>Parameter ini relevan dengan TCP Keepalive, yang defaultnya adalah 75/9/7200. Pengaturan default berarti bahwa kernel akan memulai deteksi ketika koneksi TCP tidak aktif selama 7.200 detik, dan akan mengirim RST setelah 9 deteksi gagal (masing-masing selama 75 detik). Nilai ini terlalu tinggi untuk sebuah server. Anda dapat menyesuaikannya menjadi 30/3/1800 sesuai kebutuhan.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.ip_local_port_range</code></td>
<td>Parameter ini digunakan untuk mengonfigurasi rentang port yang tersedia, yang dapat disesuaikan menurut kebutuhan.</td>
<td>-</td>
</tr>
<tr>
<td><code>tcp_tw_reuse</code></td>
<td>Parameter ini digunakan untuk menggunakan kembali soket dalam status TIME-WAIT untuk koneksi TCP baru. Parameter ini membantu Anda dengan cepat memulai ulang tautan yang menggunakan port tetap, tetapi mungkin melibatkan risiko dalam jaringan berbasis NAT. Versi kernel yang lebih baru mendukung nilai 0, 1, dan 2 dan mengonfigurasinya ke 2.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.ip_forward</code><br>
<code>net.ipv6.conf.all.forwarding</code>
</td>
<td>Parameter ini digunakan untuk menentukan penerusan IP. Anda dapat mengonfigurasinya ke 1 dalam skenario penerusan rute Docker.</td>
<td>0</td>
</tr>
<tr>
<td><code>net.ipv4.conf.default.rp_filter</code></td>
<td>Parameter ini digunakan untuk menentukan aturan validasi jalur balik ENI pada paket data yang diterima. Nilai yang valid mencakup 0, 1 (direkomendasikan oleh RFC3704), dan 2. Konfigurasi yang direkomendasikan adalah mode ketat yang dapat mencegah serangan DDoS dan tindakan spoofing IP.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.conf.default.accept_source_route</code></td>
<td>Parameter ini digunakan untuk menentukan apakah akan menerima paket IP yang berisi rute sumber, yang tidak diizinkan secara default, seperti yang direkomendasikan di situs web CentOS.</td>
<td>0</td>
</tr>
<tr>
<td><code>net.ipv4.conf.all.promote_secondaries</code><br>
<code>net.ipv4.conf.default.promote_secondaries</code></td>
<td>Parameter ini digunakan untuk menentukan apakah alamat IP sekunder akan menjadi IP primer setelah alamat IP primer asli dihapus.</td>
<td>1</td>
</tr>
<tr>
<td><code>net.ipv6.neigh.default.gc_thresh3</code><br>
<code>net.ipv4.neigh.default.gc_thresh3</code>
</td>
<td>Parameter ini digunakan untuk menentukan catatan maksimum yang disimpan dalam cache ARP. Pengumpul sampah segera memulai setelah catatan yang disimpan melebihi nilai yang ditetapkan.</td>
<td>4096</td>
</tr>
</table>



### Terkait memori

<table>
<tr>
<th>Parameter</th><th>Deskripsi</th><th>Konfigurasi Awal</th>
</tr>
<tr>
<td><code>vm.vfs_cache_pressure</code></td>
<td>Ini mengontrol kecenderungan kernel untuk mendapatkan kembali memori. Pada nilai default 100, kernel akan mencoba untuk mengambil kembali dentry untuk dikembalikan ke memori. Layanan berbasis curl biasanya mengakumulasi dentry, yang dapat menghabiskan semua memori kosong dan menyebabkan bug OOM atau kernel. Kami mengonfigurasinya ke 250 untuk menyeimbangkan frekuensi dan performa pengambilan kembali, yang dapat disesuaikan.</td>
<td>250</td>
</tr>
<tr>
<td><code>vm.min_free_kbytes</code></td>
<td>Parameter ini digunakan untuk memaksa MEM Linux untuk menyimpan jumlah minimum kilobyte memori bebas untuk digunakan oleh utas kernel. Nilai secara otomatis dihitung menurut memori fisik bebas (MEM) saat startup dengan: 4*sqrt (MEM). Saat server menerima microbursts paket, server Anda mungkin menjadi rusak secara halus dan menyebabkan OOM. Pada server dengan konfigurasi tinggi, sebaiknya konfigurasikan <code>vm.min_free_kbytes</code> pada sekitar 1% dari total memori secara default.
</td>
<td>-</td>
</tr>
<tr>
<td><code>kernel.printk</code></td>
<td>Hal ini menentukan tingkat untuk fungsi pencetakan printk kernel. Nilai konfigurasi default-nya adalah lima atau lebih. </td>
<td>5 4 1 7</td>
</tr>
<tr>
<td><code>kernel.numa_balancing</code></td>
<td>Hal ini menunjukkan bahwa kernel dapat secara otomatis memindahkan proses ke node NUMA yang sesuai, tetapi sebenarnya tidak efektif dan memengaruhi performa. Anda dapat mencoba mengaktifkannya dalam kasus penggunaan Redis.</td>
<td>0</td>
</tr>
<tr>
<td><code>kernel.shmall</code><br>
<code>kernel.shmmax</code>
</td>
<td><ul><li>shmmax: menentukan ukuran maksimum satu segmen memori bersama (dalam byte) yang dapat dialokasikan oleh proses Linux.</li><li>shmall: menentukan jumlah total halaman memori bersama di seluruh sistem.</li></ul></td>
<td><code>kernel.shmmax<br>=68719476736</code><br>
<code>kernel.shmall<br>=4294967296</code>
</td>
</tr>
</table>

### Terkait proses
<table>
<tr>
<th>Parameter</th><th>Deskripsi</th><th>Konfigurasi Awal</th>
</tr>
<tr>
<td><code>fs.file-max</code><br>
<code>fs.nr_open</code>
</td>
<td>Mereka menunjukkan jumlah maksimum penanganan file yang masing-masing dapat dialokasikan oleh kernel Linux atau proses.<ul><li>file-max: secara otomatis mengonfigurasi kira-kira 100.000/GB saat OS dimulai.</li><li>nr_open: diatur ke nilai tetap 1048576, yang membatasi penanganan file terbuka maksimum dalam lingkungan mode pengguna. Umumnya, jangan ubah nilai ini. Untuk memodifikasi penanganan file terbuka maksimum, konfigurasikan parameter <code>ulimit -n</code> di file konfigurasi /etc/security/limits.conf.</li></ul></td>
<td>
<code>ulimit -n=100001</code><br>
<code>fs.nr_open=1048576</code>
</td>
</tr>
<tr>
<td><code>kernel.pid_max</code></td>
<td>Hal ini menentukan proses maksimum dalam sistem. Citra resmi menggunakan nilai default 32768, yang dapat disesuaikan menurut kebutuhan.</td>
<td>-</td>
</tr>
<tr>
<td><code>kernel.core_uses_pid</code></td>
<td>Hal ini menentukan apakah nama file coredump yang dihasilkan akan berisi .PID.</td>
<td>1</td>
</tr>
<tr>
<td><code>kernel.sysrq</code></td>
<td>Hal ini memungkinkan Anda mengoperasikan /proc/sysrq-trigger nanti.</td>
<td>1</td>
</tr>
<tr>
<td><code>kernel.msgmnb</code><br>
<code>kernel.msgmax</code>
</td>
<td>Nilai ini menentukan ukuran maksimum dalam byte dari antrean pesan tunggal dan ukuran maksimum yang diizinkan dalam byte dari setiap pesan tunggal dalam antrean pesan</td>
<td>65536</td>
</tr>
<tr>
<td><code>kernel.softlockup_panic</code></td>
<td>Hal ini mengontrol apakah kernel akan panik saat terdeteksi adanya soft lockup. Jika diaktifkan, vmcore akan dibuat berdasarkan konfigurasi kdump, yang dapat digunakan untuk menganalisis penyebab soft lockup.</td>
<td>-</td>
</tr>
</table>


### Terkait IO
<table>
<tr>
<th>Parameter</th><th>Deskripsi</th><th>Konfigurasi Awal</th>
</tr>
<tr>
<td><code>vm.dirty_background_bytes</code><br>
<code>vm.dirty_background_ratio</code><br>
<code>vm.dirty_bytes</code><br>
<code>vm.dirty_expire_centisecs</code><br>
<code>vm.dirty_ratio</code><br>
<code>vm.dirty_writeback_centisecs</code>
</td>
<td>Parameter ini terutama digunakan untuk mengonfigurasi kebijakan agar IO ditulis kembali ke disk.<ul><li>dirty_background_bytes/dirty_bytes dan dirty_background_ratio/dirty_ratio mengacu pada jumlah dan persentase memori sistem yang dapat diisi dengan setiap halaman “dirty”. Secara umum, rasio akan ditentukan.</li><li>dirty_background_ratio: mengacu pada persentase halaman dirty pada memori sistem (10% secara default) tempat proses pembersihan kernel latar belakang akan mulai menulis kembali ke disk. </li><li>dirty_ratio: mengacu pada jumlah maksimum absolut memori sistem yang dapat diisi dengan halaman dirty sebelum semuanya harus diterapkan ke disk. Saat sistem mencapai titik ini, semua I/O baru memblokir hingga halaman dirty telah ditulis ke disk, menyebabkan jeda I/O yang lama. Sistem pertama-tama akan mencapai kondisi `vm.dirty_background_ratio` tempat proses pembersihan akan memulai penulisan kembali asinkron, dan aplikasi terus melakukan operasi tulis. Saat sistem mencapai nilai `vm.dirty_ratio` yang ditentukan, OS akan menangani halaman dirty secara sinkron, sehingga memblokir aplikasi.<br>
</li><li>vm.dirty_expire_centisecs: menentukan berapa lama halaman dirty dapat disimpan dalam cache sebelum dirty perlu ditulis. Hal ini dinyatakan dalam waktu seperseratus (1/100) detik. Data yang telah dirty dalam memori lebih lama dari interval ini akan ditulis setiap kali proses pembersihan aktif.</li><li>vm.dirty_writeback_centisecs: menentukan seberapa sering proses flush kernel aktif. Hal ini dinyatakan dalam waktu seperseratus (1/100) detik.</li></ul>
</td>
<td>-</td>
</table>
