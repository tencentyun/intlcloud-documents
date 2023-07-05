[](id:q1)
### Bagaimana data statistik bandwidth dalam pemantauan akses dikumpulkan?
Setiap simpul CDN mengumpulkan data lalu lintas dengan segera dan melaporkannya kepada pusat komputasi, yang menggabungkan data tersebut menjadi total data lalu lintas dan menampilkan data statistik bandwidth dengan membagi total lalu lintas dengan lama penggunaannya.
**Contoh:**
- Jika total lalu lintas yang dihasilkan dalam satu menit adalah 6 MB, bandwidth-nya adalah (6 * 8) / 60 = 0,8 Mbps.
- Karena penggunaan untuk tagih-menurut-bandwidth dihitung berdasarkan data statistik dengan granularitas 5 menit, nilai bandwidth-nya adalah total lalu lintas dalam 5 menit / 300 detik.

[](id:second)
### Mengapa lalu lintas pada informasi pemantauan berbeda dengan lalu lintas pada log?
Lalu lintas yang dihitung berdasarkan byte downstream pada log nama domain akselerasi terbatas pada data pada lapisan aplikasi, sedangkan lalu lintas yang dihasilkan oleh transfer data aktual melalui jaringan adalah sekitar 5-15% lebih besar daripada lalu lintas lapisan-aplikasi.
- Penggunaan oleh header TCP/IP: pada permintaan HTTP berbasis-TCP/IP, setiap paket memiliki ukuran maksimal 1.500 byte dan mencakup header TCP dan IP sebesar 40 byte, yang menghasilkan lalu lintas selama transfer tetapi tidak dapat dihitung oleh lapisan aplikasi.Kelebihan pada bagian ini sekitar 3%.
- Pengiriman kembali TCP: selama transfer data normal melalui jaringan, sekitar 3-10% paket hilang di internet dan dikirim kembali oleh server.Jenis lalu lintas ini tidak dapat dihitung oleh lapisan aplikasi, yang mencapai 3-7% dari total lalu lintas.

Sebagai standar industri, lalu lintas yang dapat ditagih adalah jumlah lalu lintas lapisan-aplikasi dan kelebihan yang diuraikan di atas.Tencent Cloud CDN mengambil 10% sebagai proporsi kelebihan sehingga lalu lintas yang dipantau sekitar 110% dari lalu lintas yang dicatat.

[](id:q3)
### Bagaimana saya menghitung kecepatan perolehan lalu lintas?
Menurut pengaturan default, CDN mengaktifkan cache L2 (lapisan tepi dan lapisan tengah).Selama suatu permintaan memperoleh salah satu lapisan tersebut sebagai respons, permintaan tersebut akan dihitung sebagai satu perolehan simpul CDN.
Kecepatan perolehan lalu lintas = (total lalu lintas downstream - lalu lintas tarik-asal) / total lalu lintas downstream.

[](id:q4)
### Bagaimana saya memperbaiki masalah kecepatan perolehan lalu lintas yang rendah?
- Periksa apakah cache-nya dibersihkan: pembersihan cache menghapus konten yang ditentukan pada simpul sehingga menyebabkan kecepatan perolehan lalu lintas yang rendah sementara.
- Periksa apakah sumber daya baru telah ditambahkan ke server asal: sumber daya baru dalam jumlah besar dapat menyebabkan tarik-asal oleh simpul CDN sehingga menyebabkan kecepatan perolehan lalu lintas yang rendah.
- Periksa apakah server asal bekerja dengan baik: jika terjadi gangguan dengan timbulnya banyak kesalahan 4XX atau 5XX, kecepatan perolehan lalu lintas akan terpengaruh.
- Periksa apakah validitas cache dikonfigurasi dengan benar: periksa konfigurasi validitas cache di tab **Cache Configuration** (Konfigurasi Cache) pada konsol.Aturannya ditampilkan dengan urutan naik menurut prioritas, yaitu suatu aturan lebih penting daripada aturan di atasnya.
- Periksa apakah Range GETs diaktifkan: periksa konfigurasi Range GETs di tab **Tarik-asal Configuration** (Konfigurasi Tarik-asal) pada konsol.Jika konfigurasi tersebut diaktifkan, file akan ditarik secara keseluruhan bukannya dalam beberapa bagian saat diminta selama tarik-asal, yang meningkatkan lalu lintas tarik-asal dan menurunkan kecepatan perolehan.
- Periksa apakah Ignore Query String (Abaikan String Kueri) diaktifkan: centang Ignore Query String (Abaikan String Kueri) di tab **Access Control** (Kontrol Akses) pada konsol.Jika string tersebut dinonaktifkan, penyimpanan akan dilakukan berdasarkan jalur penuh.Dalam hal ini, jika sumber daya yang sama diminta dengan parameter yang berbeda, sumber daya tersebut tidak dapat dicocokkan dan akan di-cache berulang kali sehingga menurunkan kecepatan perolehan lalu lintas.

[](id:q5)
### Apakah data statistik kode status mencakup semua kode status?
Ya.Pada versi baru analisis statistik CDN, kurva pemantauan digambarkan untuk semua kode status yang dihasilkan oleh server asal sehingga lebih memudahkan Anda untuk mengatasi masalahnya.

[](id:q6)
### Bagaimana cara menghitung data statistik wilayah dan ISP?
Data statistik wilayah dan ISP dihitung berdasarkan IP klien pada log akses.Karena perhitungan diselesaikan berdasarkan log, data dapat ditagih yang terkumpul berbeda dengan data yang dapat ditagih jika "all districts" (semua distrik) atau "all ISPs" (semua ISP) dipilih.Untuk informasi selengkapnya, silakan lihat [pertanyaan 2](#second) di atas.

[](id:q7)
### Bagaimana cara menghasilkan lalu lintas tarik-asal CDN?

Lalu lintas tarik-asal CDN dihasilkan selama tiga situasi berikut:
1.Sumber daya yang diminta tidak di-cache di simpul CDN dan ditarik dari server asal.
2.Server asal yang dibersihkan secara manual disinkronkan dengan simpul.
3.Server asal dibersihkan secara otomatis.

[](id:q8)
### Apa yang harus saya lakukan jika lalu lintas CDN saya mengalami kelainan atau mengalami serangan DDoS atau CC?

Jika menurut Anda jumlah permintaan akses ke bisnis Anda sedang, Anda dapat mengunduh log akses, dan berdasarkan itu mengonfigurasi batas akses.CDN tidak mengetahui logika bisnis Anda sehingga tidak ada batas akses yang ditentukan untuk bisnis Anda menurut pengaturan default.Silakan buat konfigurasi sesuai keperluan bisnis Anda.
Untuk menghindari permintaan yang berbahaya atau serangan CC/DDoS ke situs web Anda, kami sangat menyarankan Anda melengkapi konfigurasi berikut:
1.Konfigurasi perlindungan hotlink: Anda dapat mengontrol akses ke sumber daya bisnis Anda.Dengan menetapkan kebijakan kontrol akses pada nilai bidang pengirim di header permintaan HTTP, Anda dapat membatasi sumber akses untuk mencegah hotlinking oleh pengguna yang berbahaya.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Perlindungan Hotlink](https://intl.cloud.tencent.com/document/product/228/6292).
2.Konfigurasi daftar blokir/daftar izin IP: Anda dapat membuat kebijakan pemfilteran untuk IP sumber permintaan pengguna berdasarkan kebutuhan bisnis Anda sehingga membantu mencegah hotlinking dan serangan dari IP yang berbahaya.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Daftar Blokir/Daftar Izin IP](https://intl.cloud.tencent.com/document/product/228/6298).
3.Konfigurasi batas akses IP: Anda dapat bertahan terhadap serangan CC dengan membatasi jumlah permintaan akses per detik ke suatu simpul yang diizinkan untuk IP klien.Setelah konfigurasi tersebut diaktifkan, kesalahan 514 akan dikembalikan untuk permintaan yang melebihi batas QPS.Penetapan batas frekuensi yang lebih rendah dapat memengaruhi penggunaan bisnis Anda oleh pengguna normal frekuensi tinggi.Karena itu, silakan tetapkan ambang batas sesuai dengan kondisi dan penggunaan aktual bisnis Anda.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Batas Akses IP](https://intl.cloud.tencent.com/document/product/228/6420).
4.Konfigurasi batas bandwidth: Anda dapat mengonfigurasi batas bandwidth untuk suatu nama domain.Jika bandwidth yang digunakan oleh nama domain tersebut melebihi batas ini dalam satu siklus statistik (5 menit), semua permintaan akses akan diteruskan ke server asal atau layanan CDN akan dimatikan tergantung pada konfigurasi Anda (dalam kedua kasus, kesalahan 404 akan dikembalikan untuk semua permintaan akses).Untuk informasi selengkapnya, silakan lihat [Konfigurasi Batas Bandwidth](https://intl.cloud.tencent.com/document/product/228/7541).


[](id:q9)
### Apakah ada penundaan dalam menggunakan API untuk mengueri data?Berapa lama penundaan tersebut?
Ada penundaan tertentu dalam menggunakan API untuk mengueri data.Kueri data real-time, seperti data akses dan data penagihan, mengalami penundaan sekitar 5-10 menit, sedangkan kueri data analitik, seperti peringkat, akan mengalami penundaan sekitar setengah jam.Data tersebut dikalibrasi di backend sekitar pukul 3 pagi Waktu Beijing.



