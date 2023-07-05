## Pemberkasan ICP untuk Nama Domain di Tiongkok Daratan
Ketika menghubungkan nama domain Anda ke Tencent Cloud CDN untuk mendapatkan akselerasi, jika Anda memilih daratan Tiongkok atau global sebagai wilayah akselerasi, pemberkasan ICP untuk layanan di Tiongkok Daratan harus diperoleh dari MIIT untuk nama domain Anda.

## Pemeriksaan Kredibilitas
1. Tencent Cloud CDN akan melakukan **account credibility check** (pemeriksaan kredibilitas akun) ketika Anda mengaktifkan layanan CDN. Jika akun Tencent Cloud Anda memiliki rekaman pelanggaran yang terlalu banyak, akun tersebut akan rendah kredibilitasnya dan akan diblokir. Tencent Cloud CDN akan melarang pengaktifan layanan untuk akun tersebut.

2. Tencent Cloud CDN akan melakukan **domain name credibility check** (pemeriksaan kredibilitas nama domain) ketika Anda menghubungkan nama domain Anda setelah mengaktifkan layanan CDN. Jika ada rekaman perilaku akun Anda berikut ini, akun Anda akan rendah kredibilitasnya dan akan diblokir. Tencent Cloud CDN tidak akan mengizinkan koneksi nama domain untuk akun tersebut.
 - Nama domain akselerasi telah memublikasikan konten melalui Tencent Cloud CDN yang melakukan pelanggaran berat terhadap regulasi.
 - Akun yang menjadi induk dari nama domain akselerasi memiliki tunggakan biaya dalam jumlah besar.
 - Nama domain akselerasi tercatat sebagai nama domain berbahaya oleh Manajer Tencent PC.

## Pemeriksaan Konten
Ketika menggunakan layanan Tencent Cloud CDN di Tiongkok daratan, Anda wajib untuk tetap mematuhi hukum, peraturan, dan kebijakan yang berlaku bagi konten, kualifikasi, kemampuan, dan perilaku Anda.

Jika ada dari konten-konten berikut yang sepertinya berada dalam nama domain Anda, kami akan memblokir konten yang tidak patuh dan menghentikan layanan akselerasi untuk kasus-kasus berat.
- Server game tidak resmi 
- Situs web game/perangkat lunak/video bajakan
- Situs web rumah sakit dan farmasi tidak resmi
- Konten pornografi
- Konten terkait obat-obatan keras
- Iklan dan game judi

## Layanan Akselerasi
| Jenis | Batas |
| -------- | ------------------------------------------------ |
| Nama domain akselerasi | Nama domain kartubebas dapat dihubungkan <br/>Hingga 100 nama didukung |
| Statistik data | Statistik yang dihasilkan dalam 90 hari terakhir dapat dikueri secara default |
| Pembersihan konten | Pembersihan URL: 10.000 per hari <br/>Pembersihan direktori: 100 per hari |
| Log akses | Log akses dipertahankan selama 30 hari secara default |

## Kepemilikan Kembali Nama Domain
Jika nama domain Anda tidak menghasilkan lalu lintas akses situs web dalam tiga bulan setelah koneksi, CDN akan otomatis menutup layanan akselerasi. Jika Anda ingin menggunakan layanan kembali, masuk ke Konsol CDN untuk mengaktifkannya secara manual.
