Tidak Ada Biaya Saat Pematian berarti Anda tidak akan dikenakan biaya untuk instans (CPU, memori) setelah Anda **memilih opsi Tidak Ada Biaya Saat Pematian** untuk menerapkan **shut down** (matikan) pada instans bayar sesuai pemakaian. Komponen seperti [disk cloud](https://intl.cloud.tencent.com/document/product/213/2255) (disk sistem dan disk data), bandwidth jaringan publik (tagihan per bandwidth) dan citra akan tetap dibebankan.

## Batasan Penggunaan

**Tidak Ada Biaya Saat Pematian** hanya berlaku untuk instans bayar sesuai pemakaian yang menggunakan disk cloud sebagai disk sistem dan disk data.
Fitur ini tidak tersedia untuk skenario berikut:
- Anda melakukan pematian instans setelah login alih-alih melakukan pematian di konsol.
- Memasang instans disk lokal.
- Instans spot.
- Instans yang menjalankan pematian karena akun yang melewati jatuh tempo: saat instans menjalankan pematian karena pembayaran yang melewati jatuh tempo, penagihan untuk instans dan sumber daya terkaitnya berhenti. Sumber daya komputasi dan IP publik dilepaskan. Penagihan dilanjutkan setelah Anda membayar pembayaran yang melewati jatuh tempo.

Jika operasi pematian batch mencakup instans yang memenuhi syarat untuk Tidak Ada Biaya Saat Pematian dan lainnya yang tidak memenuhi syarat, maka:
- Untuk instans yang memenuhi syarat, **CPU dan memori tidak akan dikenakan biaya** setelah pematian;
- Instans yang tidak memenuhi syarat akan **akan tetap dikenakan biaya** setelah pematian.

## Dampak

Ketika fitur Tanpa Biaya Saat Pematian diaktifkan, ini akan menyebabkan dampak berikut setelah instans menjalankan pematian.
1. Setelah pematian, CPU dan memori instans **will not be retained** (tidak akan disimpan) sehingga **mungkin gagal** saat dimulai ulang. Jika demikian, cobalah memulai ulang sekali lagi atau tunggu beberapa saat sebelum mencoba lagi.
2. Jika alamat IP publik instans ditetapkan, alamat IP publik akan **dilepaskan secara otomatis** setelah pematian. IP publik baru akan ditetapkan saat Anda memulai ulang instans. IP pribadi tetap sama. 
 **Untuk mempertahankan IP publik, Anda dapat mengonversi IP publik menjadi EIP sebelum instans menjalankan pematian**. EIP akan dipertahankan setelah pematian instans serta selama dimulai ulang, dan tidak ada biaya waktu jeda yang akan dikenakan.
3. Saat instans menjalankan pematian, sebagian besar operasi **kecuali untuk instans startup** tidak akan tersedia, termasuk menyesuaikan konfigurasi, disk, dan jaringan; menginstal ulang sistem; memulai ulang instans, mengatur ulang kata sandi; mengganti nama, dll. **Anda harus memulai instans untuk melakukan operasi tersebut**.
4. Tidak Ada Biaya Saat Pematian **tidak berlaku untuk** pematian instans sebagai akibat dari memulai ulang instans untuk konfigurasi/penyesuaian disk, penginstalan ulang sistem, dan operasi OPS lainnya.

## Panduan Operasi

Harap lihat [Tidak Ada Biaya Saat Pematian untuk Detail Instans Bayar Sesuai Pemakaian](https://intl.cloud.tencent.com/document/product/213/19922).
