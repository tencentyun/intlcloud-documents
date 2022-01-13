## Aliran Proses
Aliran proses CLB lapisan 7 dan lapisan 4 (sebelumnya aplikasi CLB) ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/9c30c679e6a5fd70f9dd9273f8784d6d.jpg)
Jika CLB lapisan 7 digunakan untuk meneruskan protokol HTTP/HTTPS, Anda bisa menambahkan nama domain yang sesuai saat membuat aturan penerusan di pendengar CLB.
- Jika hanya ada satu aturan penerusan yang dibuat, Anda bisa mengakses aturan penerusan dan layanan yang sesuai melalui VIP+URL.
- Jika ada beberapa aturan penerusan yang dibuat, penggunaan VIP+URL tidak menjamin akses ke name+URL domain tertentu.Anda harus mengakses name+URL domain secara langsung untuk memastikan aturan penerusan sudah aktif.Dengan kata lain, saat Anda mengonfigurasi beberapa aturan penerusan, satu VIP mungkin sesuai dengan beberapa nama domain.Dalam hal ini, kami sarankan Anda mengakses layanan melalui name+URL domain tertentu alih-alih VIP+URL.

## Konfigurasi Penerusan Lapisan 7
### Konfigurasi penerusan domain
CLB lapisan 7 bisa meneruskan permintaan dari nama dan URL domain berbeda ke server-server berbeda.Pendengar lapisan 7 bisa dikonfigurasikan dengan beberapa nama domain, yang masing-masing bisa dikonfigurasikan dengan beberapa jalur penerusan.
- Batas panjang nama domain yang diteruskan: 1 hingga 80 karakter.
- Tidak bisa diawali dengan `_`.
- Mendukung satu domain pasti, seperti `www.example.com`.
- Mendukung nama domain kartubebas, tetapi saat ini, hanya yang berupa `*.example.com` atau `www.example.*`, yaitu, nama domain kartubebas yang diawali atau diakhiri dengan `*`, yang hanya muncul satu kali.
- Untuk nama domain non-ekspresi reguler yang diteruskan, set karakter yang valid mencakup `a-z`, `0-9`, `.`, ` -` dan `_`.
- Nama domain yang diteruskan mendukung ekspresi reguler.Nama domain ekspresi reguler:
- Set karakter yang didukung mencakup `a-z`, `0-9`, `.`, `-`, `?`, `=`, `~`, `_`, `-`, `+`, `<code>\\</code>`, `^`, `*`, `!`, `$`, `&`, `|`, `(`, `)`, `[`, dan `]`.
- Harus diawali dengan `~`, yang hanya bisa muncul satu kali.
- Satu contoh nama domain yang didukung oleh CLB mungkin `~^www\d+\.example\.com$`.

### Pencocokan nama domain yang diteruskan
#### Kebijakan pencocokan umum
1.Jika Anda memasukkan alamat IP alih-alih nama domain di aturan penerusan dan mengonfigurasikan beberapa URL di kelompok penerusan, VIP+URL akan digunakan untuk mengakses layanan.
2.Jika Anda mengonfigurasikan satu nama domain lengkap di aturan penerusan dan beberapa URL di kelompok penerusan, name+URL domain akan digunakan untuk mengakses layanan.
3.Jika Anda mengonfigurasikan satu nama domain kartubebas di aturan penerusan dan beberapa URL di kelompok penerusan, Anda akan mengakses layanan melalui pencocokan nama domain dan URL yang diminta.Agar nama domain yang berbeda mengarah ke URL yang sama, Anda bisa menggunakan metode ini untuk konfigurasi.Dengan menggunakan `example.qcould.com` sebagai contoh, formatnya adalah sebagai berikut:
- Pencocokan persis: mencocokkan nama domain yang benar-benar cocok dengan domain yang dimasukkan
- Kartubebas awalan: mencocokkan semua nama domain dengan domain level dua dan teratas tertentu, seperti `*.qcloud.com`.
- Kartubebas akhiran: mencocokkan semua nama domain dengan domain level tiga dan dua tertentu, seperti `example.qcloud.*`.
- Pencocokan ekspresi reguler:  `~^www\d+\.example\.com$`
- Prioritas:**Exact match** (Pencocokan persis) > **Prefix wildcard** (Kartubebas awalan) > **Suffix wildcard** (Kartubebas akhiran) > **Regex match** (Pencocokan ekspresi reguler).Anda sebaiknya menggunakan nama domain yang lebih tepat untuk mencegah aktivasi beberapa aturan pencocokan.Jika tidak, Anda mungkin mendapat hasil pencocokan yang tidak akurat saat beberapa nama domain pada level yang sama dimasukkan sekaligus.
4.Jika Anda mengonfigurasikan satu nama domain di aturan penerusan dan satu URL untuk pencocokan fuzzy di kelompok penerusan, Anda bisa memulai pencocokan lengkap dengan menggunakan pencocokan awalan dan menambahkan satu kartubebas akhiran `$`.
Contohnya, jika Anda memasukkan `URL ~*.(gif|jpg|bmp)$`, hasilnya akan mencocokkan file .gif, .jpg, dan .bmp.

#### Kebijakan nama domain default[](id:default)
Jika nama domain yang diminta tidak cocok dengan aturan mana pun, CLB akan meneruskan permintaan itu ke nama domain default (Server Default).Satu pendengar hanya bisa memiliki satu nama domain default.
Contohnya, pendengar `HTTP:80` dari instance CLB 1 dikonfigurasikan dengan dua nama domain: `www.test1.com` dan `www.test2.com`, dan `www.test1.com` adalah nama domain defaultnya.Saat pengguna membuka `www.example.com`, karena tidak ada nama domain yang cocok, CLB akan meneruskan permintaan ke nama domain default `www.test1.com`.

>?
>  - Jika pendengar lapisan 7 Anda sudah mengonfigurasikan nama domain default, permintaan klien yang tidak cocok dengan aturan lainnya akan diteruskan padanya.
>  - Jika pendengar lapisan 7 Anda belum mengonfigurasikan nama domain default, permintaan klien yang tidak cocok dengan aturan lainnya akan diteruskan ke nama domain pertama yang dimuat oleh CLB (urutan pemuatannya bisa berbeda dengan yang dikonfigurasikan di konsol, karenanya, ini mungkin bukan yang pertama dikonfigurasikan di konsol).
>- Dimulai dari 18 Mei 2020:
>  - Semua pendengar lapisan 7 baru harus memiliki nama domain default: aturan pertama pendengar lapisan 7 akan diatur sebagai nama domain default.Saat Anda membuat satu aturan lapisan 7 melalui API, bidang `DefaultServer` diatur ke `true`.
>  - Untuk semua pendengar yang sudah mengonfigurasikan nama domain default, Anda harus menentukan nama domain default baru saat memodifikasi atau menghapus nama domain default yang ada: saat Anda melakukan operasi di konsol, Anda harus menentukan nama domain default baru; saat Anda melakukan operasi dengan memanggil API, jika Anda tidak mengatur nama domain default baru, CLB akan mengatur nama yang paling awal dibuat di antara nama-nama domain tersisa sebagai nama domain default baru.
>  - Untuk aturan tanpa nama domain default yang ada, Anda bisa mengonfigurasikan nama domain default secara langsung sesuai kebutuhan bisnis Anda seperti yang diinstruksikan di [operasi 4](#step4) di bawah ini.Jika Anda tidak melakukannya, Tencent Cloud akan mengatur nama domain pertama yang dimuat oleh CLB sebagai nama domain default.Semua pendengar yang ada akan diproses sebelum 19 Juni 2020.
>
Kebijakan di atas akan diimplementasikan secara bertahap mulai dari 18 Mei 2020, dan tanggal berlaku untuk setiap instance mungkin sedikit berbeda.Mulai 20 Juni 2020, semua pendengar lapisan 7 yang telah meneruskan nama domain akan memiliki nama domain default.

Empat operasi berikut ini bisa dilakukan dengan nama domain default:
- **Operation 1** (Operasi 1): saat mengonfigurasi aturan penerusan yang pertama untuk pendengar lapisan 7, nama domain default harus berstatus “aktif”.
- **Operation 2** (Operasi 2): menonaktifkan nama domain default saat ini.
- Jika di bawah satu pendengar ada beberapa nama domain, saat menonaktifkan nama domain saat ini, Anda harus menentukan nama domain default baru.
- Jika satu pendengar hanya memiliki satu nama domain dan nama domainnya adalah nama domain default, nama domain itu tidak bisa dinonaktifkan.
- **Operation 3** (Operasi 3): menghapus nama domain default.
- Jika di bawah satu pendengar ada beberapa nama domain, saat Anda menghapus satu aturan di bawah nama domain default:
- Jika aturan itu bukan aturan terakhir pada nama domain default, Anda bisa langsung menghapusnya.
- Jika aturan itu adalah aturan terakhir pada nama domain default, Anda harus mengatur nama domain default baru.
- Jika di bawah satu pendengar hanya ada satu nama domain default, Anda bisa langsung menghapus semua aturan tanpa mengatur nama domain default baru.
- <span id = "step4"></span>**Operation 4** (Operasi 4): Anda bisa dengan cepat memodifikasi nama domain default di daftar pendengar..

### Aturan konfigurasi jalur URL yang diteruskan
CLB lapisan 7 bisa meneruskan permintaan dari URL berbeda ke server-server berbeda untuk pemrosesan, dan beberapa jalur URL yang diteruskan bisa dikonfigurasikan untuk satu nama domain tunggal.
- Batas panjang URL yang diteruskan: 1–200 karakter.
- URL non-ekspresi reguler yang diteruskan harus dimulai dengan `/`., dengan set karakter yang valid termasuk `a-z`, `A-Z`, `0-9`, `.`, `-`, `_`, `/`, `=`, `?`, dan `:`.
- URL yang diteruskan mendukung ekspresi reguler:
- URL ekspresi reguler harus diawali dengan `~`, yang hanya bisa muncul satu kali.
- Untuk URL ekspresi reguler, set karakter yang valid mencakup `a-z`, `A-Z`, `0-9`, `.`, `-`, `_`, `/`, `=`, `?`, `~`, `^`, `*`, `$`, `:`, `(`, `)`, `[`, `]`, `+`, dan `|`.
- Satu contoh URL ekspresi reguler mungkin `~* .png$`.
- Aturan pencocokan untuk URL yang diteruskan adalah sebagai berikut:
- Diawali dengan `=` menunjukkan pencocokan persis.
- Diawali dengan `^~` menunjukkan URL dimulai dengan string reguler dan tidak untuk pencocokan ekspresi reguler.
- Diawali dengan `~` menunjukkan pencocokan ekspresi reguler yang peka huruf besar/kecil.
- Diawali dengan `~*` menunjukkan pencocokan ekspresi reguler yang tidak peka huruf besar/kecil.
- ` /` menunjukkan pencocokan generik, artinya permintaan apa pun akan dicocokkan jika tidak ada yang cocok lainnya.

### Deskripsi pencocokan jalur ULR yang diteruskan
![](https://main.qcloudimg.com/raw/6399b39845c9f23adccb90089e10bade.jpg)
1.Aturan pencocokan: berdasarkan pencocokan awalan, pencocokan persis dilakukan dahulu, diikuti dengan pencocokan fuzzy.
Contohnya, setelah Anda mengonfigurasikan aturan penerusan dan kelompok penerusan seperti yang ditunjukkan di atas, permintaan-permintaan berikut ini akan dicocokkan dalam aturan penerusan berbeda secara berurutan.
1.Karena `example.qloud.com/test1/image/index1.html` benar-benar cocok dengan aturan URL yang dikonfigurasikan dengan kelompok penerusan 1, permintaannya akan diteruskan ke server asli yang terkait dengan kelompok penerusan 1, yaitu, port 80 dari CVM1 dan CVM2 dalam gambar.
2.Karena tidak ada pencocokan persis untuk `example.qloud.com/test1/image/hello.html`, ini akan dicocokkan dengan aturan penerusan 2 berdasarkan pencocokan awalan terpanjang; karenanya, permintaan itu akan diteruskan ke server asli yang terkait dengan aturan penerusan 2, yaitu, port 81 dari CVM2 dan CVM3 dalam gambar.
3.Karena tidak ada pencocokan persis untuk `example.qloud.com/test2/video/mp4/`, ini akan dicocokkan dengan aturan penerusan 3 berdasarkan pencocokan awalan terpanjang; karenanya, permintaan itu akan diteruskan ke server asli yang terkait dengan aturan penerusan 3, yaitu, port 90 dari CVM4 dalam gambar.
4.Karena tidak ada pencocokan persis untuk `example.qloud.com/test3/hello/index.html`, ini akan dicocokkan dengan URL default direktori root `example.qloud.com/` dengan pencocokan awalan terpanjang.Dalam hal ini, Nginx akan meneruskan permintaan ke server asli seperti FastCGI (php) atau Tomcat (jsp), sementara Nginx akan berperan sebagai server proksi terbalik.
5.Karena tidak ada pencocokan persis untuk `example.qloud.com/test2/`, ini akan dicocokkan dengan URL default direktori root `example.qloud.com/` dengan pencocokan awalan terpanjang.
2.Jika layanan tidak berfungsi dengan baik dalam aturan URL yang ditetapkan, ini tidak akan dialihkan ke halaman lain setelah pencocokan berhasil.
Contohnya, klien meminta `example.qloud.com/test1/image/index1.html` dan mencocokkannya dengan kelompok penerusan 1.Namun, ada satu pengecualian di server asli kelompok penerusan 1 dan halaman kesalahan 404 muncul.Anda akan melihat halaman kesalahan 404, tetapi tidak dialihkan ke halaman lain.
3.Anda sebaiknya mengarahkan URL default ini ke halaman stabil (seperti halaman statis atau beranda) dan mengikatnya ke semua server asli.Jika tidak ada aturan yang cocok, sistem akan mengarahkan permintaan ke halaman URL default; jika tidak, mungkin muncul kesalahan 404.
4.Jika Anda tidak mengatur URL default, dan tidak ada aturan penerusan yang cocok, kesalahan 404 akan dikembalikan saat Anda mengakses layanan.
5.Perhatikan garis miring di akhir jalur URL lapisan 7: URL yang Anda atur diakhiri `/`, tetapi permintaan akses dari klien tidak mengandung `/`, permintaan akan dialihkan ke aturan yang diakhiri `/` (pengalihan 301).
Contohnya, di bawah pendengar `HTTP:80`, nama domain yang dikonfigurasi adalah `www.test.com`:
1.Jika URL yang diatur di bawah nama domain ini adalah `/abc/`:
- Saat klien mengakses `www.test.com/abc`, ini akan dialihkan ke `www.test.com/abc/`.
- Saat klien mengakses `www.test.com/abc/`, ini akan cocok dengan `www.test.com/abc/`.
2.Jika URL yang diatur di bawah nama domain ini adalah `/abc`:
- Saat klien mengakses `www.test.com/abc`, ini akan cocok dengan `www.test.com/abc`.
- Saat klien mengakses `www.test.com/abc/`, ini juga akan cocok dengan `www.test.com/abc`.

## Deskripsi Konfigurasi Pemeriksaan Kesehatan Lapisan 7
### Aturan konfigurasi nama domain pemeriksaan kesehatan
Nama domain pemeriksaan kesehatan adalah nama domain yang digunakan oleh CLB lapisan 7 untuk mendeteksi status kesehatan server asli.
- Batas panjang: 1-80 karakter.
- Default: nama domain yang diteruskan.
- Ekspresi reguler tidak didukung.Jika nama domain yang Anda teruskan adalah nama domain kartubebas, Anda harus menentukan nama yang tetap (non-ekspresi reguler).
- Set karakter yang valid mencakup `a-z`, `0-9`, `.`, `-`, dan `_`.Contohnya, `www.example.qcould.com`.

### Aturan konfigurasi jalur pemeriksaan kesehatan
Jalur pemeriksaan kesehatan adalah jalur URL yang digunakan oleh CLB lapisan 7 untuk mendeteksi status kesehatan server asli.
- Batas panjang: 1-200 karakter.
- Default:`/`. Anda bisa memasuki jalur khusus berawalan /.
- Ekspresi reguler tidak didukung.Anda sebaiknya menentukan URL tetap (halaman statis) untuk pemeriksaan kesehatan.
- Set karakter yang valid mencakup `a-z`, `A-Z`, `0-9`, `.`, `-`, `_`, `/`, `=`, `?`, dan `:`.Contohnya, `/index`.
