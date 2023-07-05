### Apa tujuan penggunaan EIP?
ElP berlaku untuk skenario berikut:
- Pemulihan bencana. Kami sangat menyarankan Anda menggunakan EIP untuk pemulihan bencana. Misalnya, ketika salah satu server gagal, Anda bisa melepaskan ikatan EIP dari server ini lalu mengikatnya ke server yang sehat untuk melanjutkan layanan dengan cepat.
- Mempertahankan IP publik tertentu. Jika perlu mempertahankan IP publik tertentu di bawah akun Anda, Anda bisa mengonversinya menjadi EIP, yang bisa diikat atau dilepaskan dari perangkat dan digunakan untuk mengakses jaringan publik. EIP ini akan disimpan pada akun Anda hingga Anda "melepaskannya".
- Kasus khusus lainnya. Jika perlu mengubah IP dalam beberapa kasus, Anda bisa mengonversi IP publik menjadi EIP, kemudian mengikat EIP ke atau melepaskan ikatannya dari perangkat Anda. Namun, sumber daya EIP pada akun terbatas di setiap wilayah, harap rencanakan dan gunakan EIP yang sesuai.

### Bagaimana cara EIP ditagih?

1. Biaya yang ditampilkan di konsol berlaku untuk EIP yang tidak digunakan selama lebih dari 1 jam. EIP dapat ditagih secara akurat hingga dalam pemakaian detik. EIP yang sudah terikat/tidak terikat beberapa kali akan ditagih berdasarkan total durasinya (dalam detik) saat tidak terikat.
2. EIP yang sudah tidak dipakai selama kurang dari 1 jam akan ditagih untuk biaya penggunaan sumber dayanya secara pro rata.

### Kapan EIP ditagih?
Anda bisa mengajukan, mengikat, melepaskan ikatan, atau melepaskan EIP. Dengan sumber daya EIP terbatas yang tersedia, EIP ditagih untuk biaya penggunaan sumber daya dalam jumlah kecil hanya jika EIP tersebut tidak terikat.

### Bagaimana cara menghentikan penagihan EIP?
- Jika Anda tidak membutuhkan EIP lagi, Anda bisa melepaskannya untuk menghentikan penagihan.
Untuk informasi selengkapnya tentang operasi tertentu, lihat [Melepaskan EIP](https://intl.cloud.tencent.com/document/product/213/16586).
- Jika Anda perlu mempertahankan EIP tapi ingin menghentikan penagihan, ikat ke perangkat (seperti CVM atau NAT). EIP terikat tidak akan ditagih.

### Apakah EIP bisa dikonversi kembali menjadi IP publik?

EIP tidak bisa dikonversi kembali ke IP publik.

### Apakah EIP bisa diambil?
Anda bisa mengambil IP publik yang belum ditetapkan ke pengguna lain. Untuk detail selengkapnya, lihat [Mengambil Alamat IP Publik](https://intl.cloud.tencent.com/document/product/213/32719).

