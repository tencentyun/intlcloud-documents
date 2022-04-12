## Pertanyaan umum terkait port
### Port mana yang harus dibuka ke Internet sebelum saya login ke instans?
Biasanya, Anda perlu membuka port 22 untuk instans Linux, atau port 3389 untuk instans Windows. Untuk informasi selengkapnya, lihat [Kasus Aplikasi Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35519).

### Mengapa saya harus membuka port, dan bagaimana caranya?
Anda harus membuka port di grup keamanan untuk menggunakan layanan terkait. 
Misalnya, jika Anda ingin mengakses halaman web menggunakan port 8080, Anda harus membuka port ini di grup keamanan.
Langkah-langkah untuk membuka port: 
1. Masuk ke [Konsol Grup Keamanan](https://console.cloud.tencent.com/vpc/securitygroup), dan klik ID/nama grup keamanan yang terikat dengan instans ini untuk masuk ke halaman detailnya.
2. Pilih **Inbound/Outbound rule** (Aturan Masuk/Keluar) dan klik **Add a Rule** (Tambahkan Aturan).
3. Masukkan alamat IP (rentang) dan port yang akan dibuka, lalu pilih **Allow** (Izinkan) untuk membuka port.
Untuk informasi selengkapnya, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35513).

### Bisnis saya tidak dapat diakses setelah saya mengubah port.
Setelah mengubah port layanan, Anda juga perlu membuka port yang sesuai dalam grup keamanan.

### Port mana yang tidak didukung oleh Tencent Cloud?
Port berikut tidak diizinkan karena memiliki risiko keamanan dan kemungkinan besar akan diblokir oleh ISP.

| Protokol   | Port yang tidak didukung                            |
| ---- | ---------------------------------------- |
| TCP  | 42, 135, 137, 138, 139, 445, 593, 1025, 1434, 1068, 3127, 3128, 3129, 3130, 4444, 5554, 5800, 5900 dan 9996 |
| UDP  | 1026, 1027, 1434, 1068, 5554, 9996, 1028, 1433 dan 135 - 139 |

## Saya tidak dapat terhubung ke alamat eksternal melalui port TCP 25.
- Untuk meningkatkan kualitas pengiriman email melalui alamat IP Tencent Cloud, CVM diblokir agar tidak menggunakan port TCP 25 untuk terhubung ke alamat eksternal secara default. Untuk membuka blokir port ini, Anda dapat login ke [konsol](https://console.cloud.tencent.com/), arahkan kursor ke area navigasi akun di bagian atas, dan klik **Security Control** (Kontrol Keamanan) guna melihat tautan untuk membuka blokir port 25.
- Setiap akun mendukung pembukaan blokiran CVM sebanyak 5 kali. Perhatikan bahwa CVM bayar sesuai pemakaian tidak didukung.

Untuk informasi selengkapnya, lihat [Port Server Umum](https://intl.cloud.tencent.com/document/product/215/35520).

## Pertanyaan Umum terkait Grup Keamanan
### Mengapa ada aturan penolakan yang ditetapkan secara default di grup keamanan?
Aturan grup keamanan dipilih untuk berlaku berdasarkan urutannya dari atas ke bawah, jadi setelah aturan izinkan yang pertama kali ditetapkan divalidasi, maka aturan lainnya akan ditolak secara default. Jika aturan membuka semua port ke Internet, maka aturan penolakan akhir akan menjadi tidak valid. Kami menyediakan pengaturan default ini karena masalah keamanan.

### Jika saya mengikat grup keamanan yang salah dengan sebuah instans, apa pengaruhnya terhadap instans tersebut? Bagaimana memperbaikinya?
**Potential problems** (Potensi masalah)
 - Anda mungkin gagal terhubung dalam jarak jauh ke instans Linux melalui SSH atau instans Windows melalui desktop jarak jauh.
 - Anda mungkin gagal melakukan ping ke IP publik dan alamat IP pribadi dari instans CVM dalam jarak jauh di grup keamanan ini.
 - Anda mungkin gagal mengakses melalui HTTP layanan web yang diekspos oleh instans CVM dalam grup keamanan ini.
 - Anda mungkin gagal mengakses Internet dengan instans di bawah grup keamanan ini.
- **Solutions** (Solusi)
 - Jika salah satu masalah di atas terjadi, Anda dapat membuka "Security Group Management" (Manajemen Grup Keamanan) di konsol dan mengatur ulang aturan untuk grup keamanan, misalnya ke "only bind all-pass security groups by default" (hanya mengikat grup keamanan all-pass secara default).
 - Untuk detail pengaturan aturan grup keamanan, lihat [Grup Keamanan - Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/12452).

### Apa yang dimaksud dengan arah dan kebijakan grup keamanan?
- Kebijakan grup keamanan bekerja dalam arah keluar dan masuk. Yang pertama adalah untuk memfilter lalu lintas keluar dari CVM, dan yang terakhir adalah untuk memfilter lalu lintas masuk dari CVM.
Kebijakan grup keamanan dibagi menjadi lalu lintas **allow** (izinkan) dan **refuse** (tolak).

### Bagaimana urutan penerapan kebijakan grup keamanan?
Urutan penerapan kebijakan grup keamanan adalah dari atas ke bawah. Lalu lintas melewati urutan pencocokan grup keamanan dari atas ke bawah, dan kebijakan tersebut berlaku segera setelah ada kecocokan yang berhasil.

### Mengapa port yang dibuka ke Internet oleh grup keamanan tidak dapat mengakses instans CVM?
- CVM terikat dengan beberapa grup keamanan, dan port ini ditolak oleh grup keamanan lain dengan prioritas lebih tinggi.
- ACL jaringan atau firewall telah dikonfigurasi.

### Mengapa IP yang tidak diizinkan oleh grup keamanan masih dapat mengakses CVM?
Kemungkinan alasan: 
- CVM terikat ke beberapa grup keamanan, dan IP ini diizinkan oleh grup keamanan lain.
- Alamat IP ini milik layanan publik Tencent Cloud yang disetujui.

### Bisakah iptable digunakan bersama dengan grup keamanan?
Ya, iptable dan grup keamanan dapat digunakan secara bersamaan. Lalu lintas Anda akan difilter dua kali sebagai berikut:
- Keluar: proses dalam instans Anda > iptable > grup keamanan.
- Masuk: grup keamanan > iptable > proses di instans Anda.

### Semua CVM yang dikaitkan dengan grup keamanan telah ditampilkan. Namun, saya masih tidak bisa menghapus grup keamanan.
Selain CVM, grup keamanan juga dapat diikat dengan instans database CLB, ENI dan cloud. Harap pastikan bahwa semua instans yang terikat dengan grup keamanan yang akan dihapus telah dibatalkan pengaitannya. 

### Bisakah nama grup keamanan kloning sama dengan nama grup keamanan di wilayah target?
Ya.

### Dapatkah saya mengkloning grup keamanan ke proyek atau wilayah lain menggunakan API?
Ya. Untuk informasi selengkapnya, lihat [CloneSecurityGroup](https://intl.cloud.tencent.com/document/product/215/39444).

### Ketika saya mengkloning grup keamanan ke proyek atau wilayah lain, apakah CVM yang dikaitkan dengan grup keamanan juga akan dikloning?
Tidak. Hanya aturan masuk dan keluar grup keamanan yang dikloning. Anda perlu mengaitkan CVM lagi setelah kloning.
