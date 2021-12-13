### Dalam skenario apa saya perlu menambahkan aturan grup keamanan?
Untuk memastikan aksesibilitas instans CVM, Anda perlu menambahkan aturan grup keamanan dalam skenario berikut:
- Tidak ada aturan grup keamanan (ditambahkan atau default) untuk instans CVM. Jika instans CVM Anda perlu mengakses jaringan publik atau berkomunikasi dengan instans CVM yang berkaitan dengan grup keamanan lain di wilayah yang sama, Anda perlu menambahkan aturan keamanan.
- Aplikasi yang Anda buat menggunakan port kustom atau jarak port, bukan port default. Dalam hal ini, Anda perlu membuka port kustom atau jarak port sebelum menguji konektivitas aplikasi. Misalnya, jika Anda menyiapkan layanan Nginx di instans CVM yang terdengar di port komunikasi TCP 1800 tapi grup keamanan Anda hanya membuka port 80, maka Anda perlu menambahkan aturan grup keamanan untuk memastikan aksesibilitas layanan Nginx.
- Untuk skenario lain, lihat [Kasus Penggunaan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/32369).

### Apa dampak kesalahan dalam mengonfigurasi aturan grup keamanan?
Jika ada aturan grup keamanan yang tidak dikonfigurasi dengan benar, instans CVM akan gagal mengakses perangkat lain melalui jaringan pribadi atau jaringan publik. Contohnya:
- Anda mungkin gagal terhubung dalam jarak jauh ke instans Linux melalui SSH atau instans Windows melalui desktop jarak jauh.
- Anda mungkin gagal melakukan ping IP publik dari instans CVM jarak jauh.
- Anda mungkin gagal mengakses layanan Web yang disediakan oleh instans CVM melalui protokol HTTP atau HTTPS.
- Anda mungkin gagal mengakses instans CVM lain melalui jaringan pribadi.


### Apakah aturan masuk dan aturan keluar grup keamanan dihitung secara terpisah?
Maksimal 100 aturan masuk dan 100 aturan keluar yang bisa ditetapkan untuk grup keamanan.


### Dapatkah saya menyesuaikan jumlah maksimal aturan grup keamanan yang diizinkan?
Setiap grup keamanan dapat mengonfigurasi hingga 200 aturan grup keamanan, termasuk 100 aturan masuk dan 100 aturan keluar. Satu instans CVM dapat dihubungkan dengan hingga 5 grup keamanan dan karenanya dapat mengadopsi hingga 1.000 aturan grup keamanan, yang cukup untuk memenuhi kebutuhan sebagian besar skenario.
Jika penggunaan Anda melampaui batas atas ini, periksa apakah ada aturan yang berlebihan.
- Jika demikian, hapus aturan tersebut.
- Jika tidak, buat lebih banyak grup keamanan.

Selain itu, Anda bisa [mengirimkan tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) untuk meningkatkan batas atas aturan grup keamanan.
