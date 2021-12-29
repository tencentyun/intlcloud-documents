## Membuat Grup Koneksi

Jika Anda perlu mempercepat akses di beberapa wilayah dengan wilayah server asal dan konfigurasi pendengar yang sama, Anda dapat mengonfigurasi dan mengelola koneksi dalam kumpulan melalui grup koneksi, yang mengurangi pekerjaan berulang yang terlibat dalam mengelola koneksi individual.

1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap), masuk ke halaman **Connection Group Management** (Manajemen Grup Koneksi), dan klik **Create** (Buat).
2. Di jendela pop-up, masukkan informasi grup koneksi.
   ![](https://qcloudimg.tencent-cloud.cn/raw/42ea117befdea84bafafd6af6a9e2e09.png)
   
   - Proyek: proyek milik tempat grup koneksi yang dapat diubah.
   - Nama Grup Koneksi: dapat berisi hingga 30 karakter.
   - Versi IP: pilih IPv4 atau IPv6 sesuai kebutuhan. Saat ini, IPv6 hanya didukung untuk node akses di daratan Tiongkok.
   - Node Akses: pilih satu atau beberapa node di wilayah klien atau wilayah terdekat dengan klien.
   <blockquote class="d-mod-notice">
<div class="d-mod-title d-explain-title">
 <i class="d-icon-notice"></i>Catatan:
</div>
<li>Jaringan BGP premium tersedia di Hong Kong (Tiongkok). Jika Anda membutuhkannya, <a href="https://console.cloud.tencent.com/workorder/category">kirim tiket</a> untuk menghubungi kami.</li>
<li>Jaringan node non-BGP tersedia di daratan Tiongkok. Jika Anda membutuhkannya, <a href="https://console.cloud.tencent.com/workorder/category">kirim tiket</a> untuk menghubungi kami.</li>
</blockquote>
- Wilayah Server Asal: pilih node di wilayah server tujuan atau wilayah terdekat dengan server tujuan.
   <blockquote class="d-mod-notice">
                   <div class="d-mod-title d-explain-title">
                       <i class="d-icon-notice"></i>Catatan:
                   </div>
      <p>Tidak ada koneksi langsung yang dapat dibuat antara Taiwan (Tiongkok) dan daratan Tiongkok.</p>
               </blockquote>
- Spesifikasi Koneksi: pilih batas bandwidth dan jumlah maksimum koneksi bersamaan untuk setiap koneksi.
- Batas Bandwidth: batas atas bandwidth koneksi adalah 10.000 Mbps (atau 1.000 Mbps untuk koneksi tertentu).
- Koneksi Bersamaan Maksimum: jumlah maksimum koneksi bersamaan yang didukung oleh koneksi adalah 1 juta (atau 300.000 untuk koneksi tertentu).
   <blockquote class="d-mod-notice">
                   <div class="d-mod-title d-explain-title">
                       <i class="d-icon-notice"></i>Catatan:
                   </div>
      <p>Grup koneksi dapat berisi hingga 20 koneksi.</p>
               </blockquote>
- Tag: Anda dapat secara opsional mengatur tag untuk mengelompokkan koneksi untuk manajemen.
- Biaya: biaya koneksi dan biaya bandwidth yang sesuai akan ditampilkan di bawah ini sesuai dengan bandwidth dan kebersamaan yang Anda pilih.
  </a> Biaya koneksi: ditagih per hari hingga koneksi dihapus. Perhatikan bahwa biaya koneksi akan tetap dikenakan untuk satu hari meskipun koneksi dihapus kurang dari satu hari setelah pembuatan.
  ## B Biaya bandwidth: ditagih berdasarkan puncak bandwidth keluar/masuk harian.
3. Klik **OK** (OKE).
4. Pada halaman [Manajemen Grup Koneksi](https://console.cloud.tencent.com/gaap/group), lihat informasi daftar grup koneksi. Anda dapat mengelola koneksi yang berbeda dalam grup koneksi berdasarkan kebutuhan aktual Anda dan memantau status berjalannya secara real-time.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b6828c4086edaa1b1cf84986c1379036.png)
   - Nama Grup ID/Koneksi: ID dan nama (dapat disesuaikan) dari grup koneksi.
   - VIP: Alamat IP yang diakses oleh klien.
   - Nama Domain: nama domain yang diakses oleh klien, yang ditetapkan oleh sistem dan secara otomatis terikat ke VIP.
   - Status: hanya koneksi akselerasi dalam status **Running** (Berjalan) yang dapat bekerja secara normal.

## Melihat Informasi Grup Koneksi

1. Login ke [GAAP console](https://console.cloud.tencent.com/gaap), masuk ke halaman **Connection Group Management** (Manajemen Grup Koneksi), dan klik **ID/Connection Name** (ID/Nama Koneksi) dari grup koneksi yang ditentukan.
   ![](https://qcloudimg.tencent-cloud.cn/raw/a61839822d556c1dc21f0fc07d3f4df0.png)
2. Pada tab **Connection Group Info** (Info Grup Koneksi), Anda dapat melihat detail setiap koneksi. **Forwarding server IP** (IP server penerusan) mengacu pada IP node penerusan di akhir koneksi akselerasi yang bertanggung jawab untuk meneruskan data koneksi ke server asal melalui jaringan publik. Jika ingin beberapa koneksi menggunakan nama domain yang sama, klik **Unified Domain Name** (Nama Domain Terpadu) untuk mengalihkan ke halaman [Nama Domain Terpadu](https://console.cloud.tencent.com/gaap/domain) untuk konfigurasi. **unified domain name** (nama domain terpadu) dapat dikonfigurasi secara terpisah untuk koneksi berbeda dalam grup koneksi yang sama.
   ![](https://qcloudimg.tencent-cloud.cn/raw/7ff4c01ffd322dd8577d426e6a3ce3fa.jpg)

## Manajemen Pendengar TCP/UDP

### Membuat pendengar TCP/UDP

Untuk petunjuk, lihat [Manajemen Pendengar TCP/UDP](https://intl.cloud.tencent.com/document/product/608/13764).

### Mengatur pendengar TCP/UDP

Untuk petunjuk, lihat [Manajemen Pendengar TCP/UDP](https://intl.cloud.tencent.com/document/product/608/13764).

## Manajemen Pendengar HTTP/HTTPS

### Membuat pendengar HTTP/HTTPS

Untuk petunjuk, lihat [Manajemen Pendengar HTTP/HTTPS](https://intl.cloud.tencent.com/document/product/608/17539).

### Mengatur pendengar HTTP/HTTPS

Untuk petunjuk, lihat [Manajemen Pendengar HTTP/HTTPS](https://intl.cloud.tencent.com/document/product/608/17539).

## Perlindungan keamanan

Untuk informasi selengkapnya, lihat [Manajemen Pendengar HTTP/HTTPS](https://intl.cloud.tencent.com/document/product/608/42338).
