## Menambahkan Koneksi

1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap), masuk ke halaman **Access Management** (Manajemen Akses), dan klik **Create** (Buat).
2. Di jendela pop-up, masukkan informasi koneksi.
![](https://main.qcloudimg.com/raw/d30c08d1cf9dedb12ed805bf731e073f.png)
   
   - Proyek: proyek yang memiliki koneksi, yang dapat diubah.
   - Nama Koneksi: dapat berisi hingga 30 huruf dan simbol biasa.
   - Versi IP: pilih IPv4 atau IPv6 sesuai kebutuhan. Saat ini, IPv6 hanya didukung untuk wilayah di daratan Tiongkok.
   - Akses Node: pilih node di wilayah klien atau wilayah terdekat dengan klien.
   <blockquote class="d-mod-notice">
   						<div class="d-mod-title d-explain-title">
   							<i class="d-icon-notice"></i>Catatan:
   						</div>
               <p>Jaringan BGP premium tersedia di Hong Kong (Tiongkok). Jika Anda membutuhkannya, kirim tiket untuk menghubungi kami.</p>
               <p>Jaringan node non-BGP tersedia di daratan Tiongkok. Jika Anda membutuhkannya, kirim tiket untuk menghubungi kami.</p>
   					</blockquote>
   - Node Origin-Pull: pilih node di wilayah server tujuan atau wilayah terdekat dengan server tujuan.
   <blockquote class="d-mod-notice">
   						<div class="d-mod-title d-explain-title">
   							<i class="d-icon-notice"></i>Catatan:
   						</div>
               <p>Tidak ada koneksi langsung yang dapat dibuat antara Taiwan (Tiongkok) dan daratan Tiongkok.</p>
   					</blockquote>
   - Batas Bandwidth: batas atas bandwidth koneksi adalah 10.000 Mbps (atau 1.000 Mbps untuk koneksi tertentu).
   - Koneksi Bersamaan Maksimum: jumlah maksimum koneksi bersamaan yang didukung oleh koneksi adalah 1 juta (atau 300.000 untuk koneksi tertentu).
   - Tag: Anda dapat secara opsional mengatur tag untuk mengelompokkan koneksi untuk manajemen.
   - Biaya: biaya koneksi dan biaya bandwidth yang sesuai akan ditampilkan di bawah ini sesuai dengan bandwidth dan kebersamaan yang Anda pilih.
     a. Biaya koneksi: ditagih per hari hingga koneksi dihapus. Perhatikan bahwa biaya koneksi akan tetap dikenakan untuk satu hari meskipun koneksi dihapus kurang dari satu hari setelah pembuatan.
     b. Biaya bandwidth: ditagih berdasarkan puncak bandwidth keluar/masuk harian.
3. Klik **OK** (OKE).
4. Pada halaman **Access Management** (Manajemen Akses), lihat informasi daftar koneksi.
![](https://main.qcloudimg.com/raw/b326c683b47321704d0269a0eb047f2d.png)
   
   - ID/nama koneksi: ID dan nama koneksi. Nama koneksi dapat diubah.
   - VIP: Alamat IP yang diakses oleh klien.
   - Nama domain: nama domain yang diakses oleh klien, yang ditetapkan oleh sistem dan secara otomatis terikat ke VIP.
   - Status: hanya koneksi akselerasi dalam status **Running** (Berjalan) yang dapat bekerja secara normal.

## Melihat Informasi Koneksi

1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap), masuk ke halaman **Access Management** (Manajemen Akses), dan klik **ID/Connection Name** (ID/Nama Koneksi) dari koneksi yang ditentukan.
![](https://qcloudimg.tencent-cloud.cn/raw/dba1d1cb841d8575a1b653c9d47f640b.png)
2. Pada tab **Connection Info** (Info Koneksi), Anda dapat melihat detail koneksi. **Forwarding server IP** (IP server penerusan) mengacu pada IP node penerusan di akhir koneksi akselerasi yang bertanggung jawab untuk meneruskan data koneksi ke server asal melalui jaringan publik. Jika Anda ingin beberapa koneksi menggunakan nama domain yang sama, klik **Not Associated** (Tidak Terhubung) untuk mengalihkan ke halaman [Nama Domain Terpadu](https://console.cloud.tencent.com/gaap/domain) untuk konfigurasi.<br>
<img src="https://main.qcloudimg.com/raw/f611bf8653bce37ace29e99ebbb75f7b.png" width=70%>
