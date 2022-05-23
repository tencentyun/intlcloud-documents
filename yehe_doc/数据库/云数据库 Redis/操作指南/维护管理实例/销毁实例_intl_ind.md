## Ikhtisar
Berdasarkan kebutuhan bisnis yang Anda miliki, Anda dapat menghentikan instans bayar sesuai pemakaian secara manual.
- Setelah instans bayar sesuai pemakaian dihentikan, instans tersebut akan dipindahkan ke keranjang sampah TencentDB dan disimpan selama 24 jam. Selama periode penyimpanan, instans tidak dapat diakses tetapi dapat dipulihkan.

Setelah instans dihentikan, setelah statusnya berubah menjadi **Diisolasi** atau **Untuk dihapus**, instans tersebut tidak akan dikenakan biaya lagi.
>!
>- Setelah instans tersebut dihentikan, semua datanya akan dihapus dan tidak dapat dipulihkan. Pastikan untuk mencadangkan data Anda terlebih dahulu sebelum mengirimkan tugas penghentian.
>- Saat instans dihentikan, sumber daya IP-nya akan dirilis secara bersamaan.


## Petunjuk
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), cari instans yang diinginkan dalam daftar instans, dan pilih **More** (Lainnya) > **Terminate** (Hentikan) di kolom **Operation** (Operasi).
2. Di jendela pop-up, konfirmasikan bahwa semuanya sudah benar dan klik **Terminate** (Hentikan).
3. Setelah penghentian, Anda akan diarahkan ke [keranjang sampah instans](https://console.cloud.tencent.com/redis/recycle), selanjutnya Anda dapat *Mulai** atau **Hilangkan** instans yang terisolasi.

