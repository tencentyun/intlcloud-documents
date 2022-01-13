CLB mengarahkan permintaan ke instance server asli yang berjalan dengan normal.Dokumen ini menjelaskan cara menambah atau menghapus server asli sesuai kebutuhan atau saat Anda menggunakan CLB untuk pertama kalinya.

## Prasyarat
Anda telah membuat instance CLB dan mengonfigurasi satu pendengar.Untuk informasi selengkapnya, silakan lihat [Memulai CLB](https://intl.cloud.tencent.com/document/product/214/8975).
## Petunjuk
### Menambahkan server asli ke instance CLB
>?
>- Jika instance CLB diasosiasikan dengan grup penskalaan otomatis, instance CVM di grup itu akan ditambahkan secara otomatis ke server asli instance CLB.Jika instance CVM dihapus dari grup penskalaan otomatis, instance itu akan dihapus secara otomatis dari server asli instance CLB.
>- Jika Anda perlu menggunakan API untuk menambahkan server asli, silakan lihat [RegisterInstancesWithLoadBalancer](https://intl.cloud.tencent.com/document/api/214/1265) API.
>
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance).
2.Pada tab "Penyeimbang Beban Cloud" di halaman "Manajemen Instance", klik **Configure Listener** (Konfigurasikan Pendengar) di kolom "Operasi" di sebelah kanan instance CLB target.
4.Pada modul konfigurasi pendengar, pilih pendengar yang akan diikat pada server asli.
<span id="http"></span>
- **HTTP/HTTPS Listener** (Pendengar HTTP/HTTPS)
1.Di area pendengar HTTP/HTTPS, klik "+" di sebelah kiri pendengar target.
![](https://main.qcloudimg.com/raw/561cc0f6ee3c0bce9e051fb20b4ec7bd.png)
2.Klik "+" di sebelah kiri nama domain yang diperluas.
![](https://main.qcloudimg.com/raw/c4bb770736b9e185a3ecaddb9591331d.png)
3.Pilih jalur URL yang diperluas dan klik **Bind** (Ikat).
![](https://main.qcloudimg.com/raw/05f2041acaced53d2ae8bc24a2f0662b.png)
-**TCP/UDP/TCP SSL listener** (Pendengar TCP/UDP/TCP SSL)
Pada daftar di sebelah kiri modul pendengar TCP/UDP/TCP SSL, pilih pendengar yang akan diikat ke server asli dan klik **Bind** (Ikat).
![](https://main.qcloudimg.com/raw/7dc44fc32104e533b512ab6c0b616e21.png)
<span id="CLB"></span>
5.Ikat server asli ke instance CLB.
- **Method 1** (Metode 1).Di jendela pop-up "Ikat Server Asli", klik **CVM**, pilih satu atau beberapa instance CVM untuk berasosiasi, masukkan port dan beban, dan klik **OK**.Untuk informasi selengkapnya, silakan lihat [Port Server Umum](https://intl.cloud.tencent.com/document/product/213/12451).
>?
>- Jendela pop-up "Ikat Server Asli" hanya menampilkan instance CVM yang tersedia di satu wilayah dan satu lingkungan jaringan yang tidak terisolasi dan belum kedaluwarsa dengan batas bandwidth lebih dari 0.
>- Jika beberapa server asli terikat, CLB akan meneruskan lalu lintas sesuai dengan algoritme hash untuk menyeimbangkan beban.
>- Makin besar bobot server, makin banyak permintaan yang diteruskan ke sana.Nilai defaultnya 10, dan rentang nilai yang bisa dikonfigurasi adalah 0-100.Jika bobot diatur ke 0, server tidak akan menerima permintaan baru.Jika persistensi sesi diaktifkan, distribusi permintaan yang tidak merata di antara server asli bisa terjadi.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Algoritme dan Bobot](https://intl.cloud.tencent.com/document/product/214/5371).
>
![](https://main.qcloudimg.com/raw/a7f71557ff1812f777c9e989b916049f.png)
- **Method 2** (Metode 2).Jika Anda perlu mengikat server dalam beberapa batch dengan nilai port praatur yang sama, Anda bisa mengeklik **CVM** di jendela pop-up "Ikat Server Asli", masukkan nilai port default (untuk informasi selengkapnya mengenai pemilihan port, silakan lihat [Port Server Biasa](https://intl.cloud.tencent.com/document/product/213/12451)), periksa server target, atur nilai bobot, dan klik **OK**.
![](https://main.qcloudimg.com/raw/118bfbab842d72e990d9ffe08c6379ff.png)

### Memodifikasi bobot server asli untuk instance CLB
Bobot server asli menentukan jumlah permintaan CVM yang akan diteruskan.Saat mengikat server asli, Anda harus mengatur bobotnya terlebih dahulu.Berikut ini adalah penjelasan cara memodifikasi bobot server asli dengan "pendengar HTTP/HTTPS" sebagai contoh (yang bisa dimodifikasi untuk pendengar TCP/UDP/TCP SSL dengan cara yang sama).
>?
>- Jika Anda perlu menggunakan API untuk memodifikasi bobot server asli, silakan lihat [ModifyLoadBalancerBackends](https://intl.cloud.tencent.com/document/api/214/1264) API.
>- Untuk informasi selengkapnya mengenai bobot server asli CLB, silakan lihat [Metode Polling CLB](/doc/product/214/6153).
>
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance).
2.Pada tab "Penyeimbang Beban Cloud" di halaman "Manajemen Instance", klik **Configure Listener** (Konfigurasikan Pendengar) di kolom "Operasi" di sebelah kanan instance CLB target.
4.Pada daftar di sebelah kiri modul pendengar HTTP/HTTPS, perluas instance dan aturan pendengar, dan pilih jalur URL.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
5.Pada daftar server di sebelah kanan modul pendengar HTTP/HTTPS, modifikasi bobot server yang relevan.
>?Makin besar bobot server, makin banyak permintaan yang diteruskan ke sana.Nilai defaultnya 10, dan rentang nilai yang bisa dikonfigurasi adalah 0-100.Jika bobot diatur ke 0, server tidak akan menerima permintaan baru.Jika persistensi sesi diaktifkan, distribusi permintaan yang tidak merata di antara server asli bisa terjadi.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Algoritme dan Bobot](https://intl.cloud.tencent.com/document/product/214/5371).
>
- **Method 1** (Metode 1).Modifikasi bobot satu server tunggal.
1.Temukan server yang bobotnya perlu dimodifikasi, arahkan kursor di bobot yang sesuai, dan klik <img src="https://main.qcloudimg.com/raw/4aae0dbec227f8fc18b4a35acf560f62.png" style="margin:0;">.
![](https://main.qcloudimg.com/raw/519a69a1fab550879e92cdfc159a8fa1.png)
2.Di jendela pop-up "Modifikasi Bobot", masukkan nilai bobot yang baru dan klik **Submit** (Kirim).
- **Method 2** (Metode 2).Modifikasi bobot beberapa server dalam beberapa batch.
>?Setelah modifikasi batch, server akan memiliki bobot yang sama.
		>
1.Klik kotak di depan server, pilih beberapa server, dan klik **Modify Weight** (Modifikasi Bobot) di bagian atas daftar.
![](https://main.qcloudimg.com/raw/09fdd5cb7a49f80bdc088632d7249f1e.png)
2.Di jendela pop-up "Modifikasi Bobot", masukkan nilai bobot yang baru dan klik **Submit** (Kirim).



### Memodifikasi port server asli untuk instance CLB
Anda bisa memodifikasi port server asli di Konsol CLB.Berikut ini adalah penjelasan cara memodifikasi bobot server asli dengan "pendengar HTTP/HTTPS" sebagai contoh (yang bisa dimodifikasi untuk pendengar TCP/UDP/TCP SSL dengan cara yang sama).
>?Jika Anda perlu menggunakan API untuk memodifikasi port server asli, silakan lihat [ModifyTargetPort](https://intl.cloud.tencent.com/document/product/214/33812) API.
>
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance).
2.Pada tab "Penyeimbang Beban Cloud" di halaman "Manajemen Instance", klik **Configure Listener** (Konfigurasikan Pendengar) di kolom "Operasi" di sebelah kanan instance CLB target.
4.Pada daftar di sebelah kiri modul pendengar HTTP/HTTPS, perluas instance dan aturan pendengar, dan pilih jalur URL.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
5.Pada daftar server di sebelah kanan modul pendengar HTTP/HTTPS, modifikasi port server yang relevan.Untuk informasi selengkapnya mengenai pemilihan port, silakan lihat [Port Server Umum](https://intl.cloud.tencent.com/document/product/213/12451).
- **Method 1** (Metode 1).Modifikasi port satu server tunggal.
1.Temukan server yang portnya perlu dimodifikasi, arahkan kursor di port yang sesuai, dan klik <img src="https://main.qcloudimg.com/raw/4aae0dbec227f8fc18b4a35acf560f62.png" style="margin:0;">.
![](https://main.qcloudimg.com/raw/923c439bedc4af2e6129d8ada459a1c5.png)
2.Di jendela pop-up "Modifikasi Port", masukkan nilai port yang baru dan klik **Submit** (Kirim).
- **Method 2** (Metode 2).Modifikasi port beberapa server dalam beberapa batch.
>?Setelah modifikasi batch, server akan memiliki port yang sama.
		>
1.Klik kotak di depan server, pilih beberapa server, dan klik **Modify Port** (Modifikasi Port) di bagian atas daftar.
![](https://main.qcloudimg.com/raw/07d40e5fcf1111a9141be83e41f67797.png)
2.Di jendela pop-up "Modifikasi Port", masukkan nilai port yang baru dan klik **Submit** (Kirim).



### Melepas ikatan server asli dari instance CLB
Anda bisa melepas ikatan server asli di Konsol CLB.Berikut ini adalah penjelasan cara melepas ikatan server asli dengan "pendengar HTTP/HTTPS" sebagai contoh (yang bisa dilepas dari pendengar TCP/UDP/TCP SSL dengan cara yang sama).
>?
>- Melepas ikatan server asli akan melepas ikatan instance CLB dari instance CVM, dan CLB akan langsung berhenti meneruskan permintaan ke sana.
>- Melepas ikatan server asli tidak akan memengaruhi siklus pemakaian instance CVM Anda, yang bisa ditambahkan lagi ke kluster server asli saat dibutuhkan.
>Jika Anda perlu menggunakan API untuk melepas ikatan server asli, silakan lihat [DeregisterTargets](https://intl.cloud.tencent.com/document/product/214/33832) API.
>
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance).
2.Pada tab "Penyeimbang Beban Cloud" di halaman "Manajemen Instance", klik **Configure Listener** (Konfigurasikan Pendengar) di kolom "Operasi" di sebelah kanan instance CLB target.
4.Pada daftar di sebelah kiri modul pendengar HTTP/HTTPS, perluas instance dan aturan pendengar, dan pilih jalur URL.
![](https://main.qcloudimg.com/raw/06d500104032de3edda51bdc368b0c4b.png)
5.Pada server di sebelah kanan modul pendengar HTTP/HTTPS, lepas ikatan server asli.
- **Method 1** (Metode 1).Lepas ikatan satu server tunggal.
1.Temukan server yang perlu dilepas ikatannya dan klik **Unbind** (Lepas Ikatan) di kolom **Operation** (Operasi) di sebelah kanan.
![](https://main.qcloudimg.com/raw/c995daabbf0b6a710b21389b17b7760b.png)
2.Di jendela pop-up "Lepas Ikatan", konfirmasi server yang akan dilepas ikatannya dan klik **Submit** (Kirim).
- **Method 2** (Metode 2).Lepas ikatan beberapa server dalam beberapa batch.
1.Klik kotak di depan server, pilih beberapa server, dan klik **Unbind** (Lepas Ikatan) di bagian atas daftar.
![](https://main.qcloudimg.com/raw/b397ef434ce42cfaa9a48b9f4f08f09f.png)
2.Di jendela pop-up "Lepas Ikatan", konfirmasi server-server yang akan dilepas ikatannya dan klik **Submit** (Kirim).

