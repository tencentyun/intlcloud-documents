## Kustomisasi Kernel
Berdasarkan Kernel Linux stabil jangka panjang versi 4.14.105, TencentOS Server memperkenalkan fitur-fitur baru yang berlaku untuk skenario cloud dan meningkatkan performa kernel serta mengatasi kecacatan besar.

## Pengoptimalan Performa untuk Skenario Kontainer
TencentOS Server mengoptimalkan skenario kontainer dengan menyediakan isolasi yang ditingkatkan dan performa yang dioptimalkan:
- meminfo, vmstat, cpuinfo, stat, dan isolasi loadavg.
- Isolasi Sysctl, seperti tcp_no_delay_ack, tcp_max_orphans.
- Memperbaiki bug di sistem file dan jaringan.
- Memperbaiki pengecualian yang disebabkan oleh penggunaan kembali koneksi dalam skenario konkurensi tinggi dalam mode IPVS.
- Memperbaiki gangguan jaringan yang disebabkan oleh aturan IPVS yang berlebihan di bawah node spesifikasi tinggi (dengan sejumlah besar core CPU) dalam mode IPVS.
- Memperbaiki gangguan jaringan yang disebabkan ketika cAdvisor terjebak dalam status kernel terlalu lama saat membaca memcg dalam skenario kontainer kepadatan tinggi (kontainer dalam jumlah besar pada satu node).
- Memperbaiki gangguan jaringan yang disebabkan oleh penyeimbangan beban CPU dalam skenario node spesifikasi tinggi (dengan sejumlah besar core CPU) dan pod besar (menempati banyak core dengan penggunaan per core yang tinggi).
- Memperbaiki masalah gangguan jaringan berkala yang disebabkan oleh pemantauan koneksi TCP (misalnya, konfigurasi cAdvisor di-deploy secara terpisah untuk memantau koneksi TCP) dalam skenario konkurensi tinggi.
- Mengoptimalkan interupsi lunak untuk menerima paket jaringan untuk meningkatkan performa jaringan.

## Fitur Kontainer yang Disesuaikan
### Tampilan sumber daya kontainer yang terisolasi
- Menambahkan switch tingkat host: TencentOS Server menempatkan fitur seperti LXCFS di kernelnya. Alih-alih men-deploy node dalam sistem file LXCFS atau memodifikasi spesifikasi POD, Anda hanya perlu menjalankan perintah `sysctl -w kernel.stats_isolated=1` untuk mengaktifkan switch global pada node, dan kemudian file seperti `/proc/cpuinfo` dan `/proc/meminfo` yang diperoleh akan diisolasi oleh kontainer.
- Menambahkan switch tingkat kontainer: TencentOS Server menambahkan switch level kontainer `kernel.container_stats_isolated` untuk kontainer khusus seperti komponen pemantauan node. Ketika switch tingkat host diaktifkan, Anda hanya perlu menjalankan perintah `sysctl -w kernel.container_stats_isolated=0` dalam skrip startup kontainer untuk menonaktifkan switch tingkat kontainer, dan kemudian informasi host akan diperoleh dengan membaca file seperti `/proc/cpuinfo` dan `/proc/meminfo` dalam kontainer.

### Isolasi parameter kernel
TencentOS Server mengisolasi parameter kernel berikut berdasarkan namespace:
- `net.ipv4.tcp_max_orphans`
- `net.ipv4.tcp_workaround_signed_windows`
- `net.ipv4.tcp_rmem`
- `net.ipv4.tcp_wmem`
- `vm.max_map_count`

### Pengoptimalan parameter kernel kontainer default
TencentOS Server meningkatkan nilai default `net.core.somaxconn` di namespace jaringan kontainer menjadi 4096, sehingga mencegah kehilangan paket yang disebabkan oleh antrean SYN penuh dalam situasi konkurensi tinggi.

## Pengoptimalan Performa
- TencentOS Server mengoptimalkan subsistem komputasi, penyimpanan, dan jaringan:
- Mengoptimalkan alokasi memori XFS untuk mengatasi alarm kegagalan kmem_alloc XFS.
- Mengoptimalkan alokasi memori untuk paket jaringan yang diterima untuk mengatasi penggunaan memori yang berlebihan ketika sejumlah besar paket UDP diterima.
- Membatasi penggunaan memori dari cache halaman sistem untuk mempertahankan performa layanan yang optimal dan mencegah kesalahan kehabisan memori (out-of-memory/OOM).

## Paket Perangkat Lunak
- Disesuaikan berdasarkan paket perangkat lunak CentOS 7.
- Paket perangkat lunak mode pengguna kompatibel dengan CentOS 7 dan bisa digunakan langsung di TencentOS Server.
- Diupdate dan diinstal melalui Yellowdog Updater, Modified (YUM).
- Paket perangkat lunak dalam repositori Extra Packages for Enterprise Linux (EPEL) bisa digunakan setelah paket epel-release diinstal melalui YUM.

## Perbaikan Kecacatan
- Fitur Kdump disediakan jika terjadi kerusakan sistem operasi.
- Mendukung penambalan langsung kernel.

## Pembaruan Keamanan
TencentOS Server menawarkan pembaruan rutin untuk meningkatkan keamanan dan fitur-fiturnya.
