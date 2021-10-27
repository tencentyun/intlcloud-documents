### Bagaimana data statistik bandwidth dalam pemantauan akses dikumpulkan?
Setiap simpul CDN mengumpulkan data lalu lintas secara real-time dan melaporkannya ke pusat komputasi, yang mengagregasi data menjadi total data lalu lintas dan menampilkan statistik bandwidth dengan membagi total lalu lintas dengan durasi penggunaannya.
**Contoh:**
- Jika total lalu lintas yang dihasilkan dalam satu menit adalah 6 MB, bandwidth-nya adalah (6 * 8) / 60 = 0,8 Mbps.
- Karena penggunaan untuk tagihan per bandwidth dihitung berdasarkan statistik pada perincian 5 menit, nilai bandwidth yang sesuai adalah total lalu lintas dalam 5 menit / 300 detik.

### Mengapa lalu lintas pada informasi pemantauan berbeda dengan lalu lintas pada log?
Lalu lintas yang dihitung berdasarkan byte downstream dalam log nama domain yang diakselerasi terbatas pada data di lapisan aplikasi, sedangkan lalu lintas yang dihasilkan oleh transfer data aktual melalui jaringan adalah sekitar 5–15% lebih besar daripada lalu lintas lapisan aplikasi.
- Penggunaan oleh header TCP/IP: pada permintaan HTTP berbasis-TCP/IP, setiap paket memiliki ukuran maksimal 1.500 byte dan mencakup header TCP dan IP sebesar 40 byte, yang menghasilkan lalu lintas selama transfer tetapi tidak dapat dihitung oleh lapisan aplikasi.Overhead bagian ini adalah sekitar 3%.
- Transmisi ulang TCP: selama transfer data normal melalui jaringan, sekitar 3–10% paket hilang di internet dan ditransmisikan ulang oleh server.Jenis lalu lintas ini tidak dapat dihitung oleh lapisan aplikasi, yang berjumlah 3-7% dari total lalu lintas.

Sesuai standar industri, lalu lintas yang dapat ditagih adalah jumlah lalu lintas lapisan aplikasi dan biaya overhead yang dijelaskan di atas.CDN Tencent Cloud mengambil 10% sebagai proporsi overhead sehingga lalu lintas yang dipantau adalah sekitar 110% dari lalu lintas yang dicatat.

### Bagaimana saya menghitung hit rate lalu lintas?
Secara default, CDN mengaktifkan cache L2 (lapisan edge dan lapisan perantara).Selama permintaan mengenai salah satu lapisan untuk mendapatkan respons, permintaan tersebut akan dihitung sebagai hit simpul CDN.
Hit rate lalu lintas = (total lalu lintas downstream - lalu lintas tarik-asal) / total lalu lintas downstream.

### Bagaimana saya memperbaiki masalah hit rate lalu lintas yang rendah?
- Periksa apakah cache-nya dibersihkan: pembersihan cache menghapus konten yang ditentukan pada simpul sehingga menyebabkan hit rate lalu lintas yang rendah untuk sementara.
- Periksa apakah sumber daya baru telah dimasukkan ke server asal: jumlah sumber daya baru yang tinggi dapat menyebabkan tarik-asal oleh simpul CDN sehingga menyebabkan hit rate lalu lintas yang rendah.
- Periksa apakah server asal berfungsi dengan baik: jika terjadi gangguan fungsi dengan beberapa kesalahan 4XX atau 5XX, hit rate lalu lintas akan terpengaruh.
- Periksa apakah kebijakan kedaluwarsa cache dikonfigurasi dengan benar: periksa bagian "Cache Rules" (Aturan Cache) pada tab Cache Configuration (Konfigurasi Cache) di konsol.Kebijakan kedaluwarsa cache ditampilkan dalam urutan naik berdasarkan prioritas, yaitu, suatu kebijakan lebih penting dari kebijakan yang ada di atasnya.
- Periksa apakah Range GETs diaktifkan: periksa bagian "Range GETs Configuration" (Konfigurasi Range GETs) pada tab Origin Configuration (Konfigurasi Asal) di konsol.Jika konfigurasi tersebut dinonaktifkan, file akan ditarik secara keseluruhan, bukan beberapa bagian seperti yang diminta selama tarik-asal, yang meningkatkan lalu lintas tarik-asal dan menurunkan hit rate.
- Periksa apakah Ignore Query String (Abaikan String Kueri) diaktifkan: centang bagian “Ignore Query String” (Abaikan String Kueri) pada tab Access Control (Kontrol Akses) di konsol.Jika dinonaktifkan, penyimpanan cache akan dilakukan berdasarkan jalur lengkap.Dalam hal ini, jika sumber daya yang sama diminta oleh parameter yang berbeda, sumber daya tersebut tidak dapat dicocokkan dan akan di-cache beberapa kali sehingga menurunkan lalu lintas hit rate.

### Apakah statistik kode status mencakup semua kode status?

Ya.Dalam versi baru analisis statistik CDN, kurva pemantauan digambarkan untuk semua kode status yang dihasilkan oleh server asal sehingga memudahkan Anda untuk menyelesaikan masalah.

### Bagaimana cara menghitung data statistik distrik dan ISP?
Data statistik distrik dan ISP dihitung berdasarkan IP klien pada log akses.Karena perhitungan diselesaikan berdasarkan log, akumulasi data yang dapat ditagih berbeda dari data yang dapat ditagih jika "all districts" (semua distrik) atau "all ISPs" (semua ISP) dipilih.Untuk informasi selengkapnya, silakan lihat pertanyaan #2 di atas.


### Bagaimana lalu lintas tarik-asal CDN dihasilkan?

Lalu lintas tarik-asal CDN dihasilkan selama tiga situasi berikut:
1.Sumber daya yang diminta tidak di-cache pada simpul CDN dan ditarik dari server asal.
2.Server asal yang dibersihkan secara manual disinkronkan dengan simpul.
3.Server asal dibersihkan secara otomatis.

### Apa yang harus saya lakukan jika lalu lintas CDN saya memiliki pengecualian atau berada di bawah serangan DDoS atau CC?

Jika Anda yakin bahwa lalu lintas bisnis Anda sangat tinggi, Anda dapat mengunduh log untuk memeriksa kondisi akses bisnis Anda dan mengatur batasan akses yang sesuai.CDN tidak mengetahui logika bisnis Anda sehingga tidak akan membatasi permintaan akses secara default.Oleh karena itu, Anda perlu mengonfigurasi batasan tersebut berdasarkan kondisi bisnis Anda.Untuk informasi selengkapnya, silakan lihat [Unduhan Log](https://intl.cloud.tencent.com/document/product/228/6316).

Untuk menghindari permintaan berbahaya atau serangan CC/DDoS ke situs web Anda, kami sangat menyarankan Anda untuk menyelesaikan konfigurasi berikut:
1.Konfigurasi perlindungan hotlink: Anda dapat mengontrol akses ke sumber daya bisnis Anda.Dengan mengatur kebijakan kontrol akses pada nilai bidang referer di header permintaan HTTP, Anda dapat membatasi sumber akses untuk mencegah terjadinya hotlink oleh pengguna yang berniat buruk.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Perlindungan Hotlink](https://intl.cloud.tencent.com/document/product/228/6292).
2.Konfigurasi daftar blokir/daftar izin IP: Anda dapat membuat kebijakan pemfilteran untuk IP sumber permintaan pengguna berdasarkan kebutuhan bisnis Anda, membantu mencegah terjadinya hotlink dan serangan dari IP yang berbahaya.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Daftar Blokir/Daftar Izin IP](https://intl.cloud.tencent.com/document/product/228/6298).
3.Konfigurasi batas akses IP: Anda dapat mempertahankan diri dari serangan CC dengan membatasi jumlah permintaan akses per detik ke simpul yang diizinkan untuk IP klien.Setelah konfigurasi diaktifkan, kesalahan 514 akan ditampilkan untuk permintaan yang melebihi batas QPS.Mengatur batas frekuensi yang lebih rendah dapat memengaruhi penggunaan bisnis Anda oleh pengguna frekuensi tinggi biasa.Oleh karena itu, silakan tetapkan ambang batas sesuai dengan kondisi dan penggunaan bisnis aktual Anda.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Batas Akses IP](https://intl.cloud.tencent.com/document/product/228/6420).
4.Konfigurasi batas pemakaian bandwidth: Anda dapat mengonfigurasi batas pemakaian bandwidth untuk nama domain.Saat bandwidth yang digunakan oleh nama domain melebihi batas pemakaian ini dalam siklus statistik (5 menit), semua permintaan akses akan diteruskan ke server asal atau layanan CDN akan dinonaktifkan tergantung pada konfigurasi Anda (dalam kedua kasus tersebut, kesalahan 404 akan dikembalikan untuk semua permintaan akses).Untuk informasi selengkapnya, silakan lihat [Konfigurasi Batas Pemakaian Bandwidth](https://intl.cloud.tencent.com/document/product/228/7541).

### Apakah ada penundaan dalam menggunakan API untuk mengueri data?Berapa lama penundaan tersebut terjadi?
Ada penundaan tertentu dalam menggunakan API untuk mengueri data.Kueri data real-time seperti data akses dan data penagihan memiliki penundaan sekitar 5-10 menit, sedangkan kueri data analitik seperti peringkat akan mengalami penundaan sekitar setengah jam.Data tersebut dikalibrasi di backend sekitar jam 3 pagi Waktu Beijing.



