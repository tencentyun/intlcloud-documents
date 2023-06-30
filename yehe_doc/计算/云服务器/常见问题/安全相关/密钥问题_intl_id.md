### Apa perbedaan antara login kunci SSH dan login kata sandi?
Kunci SSH memungkinkan Anda untuk login ke server Linux dari jarak jauh. Ini menggunakan generator kunci untuk membuat pasangan kunci (publik dan pribadi). Kunci publik ditambahkan ke server, dan klien bisa menggunakan kunci pribadi untuk menyelesaikan autentikasi dan login. Dibandingkan dengan login kata sandi, login kunci SSH lebih aman dan efisien.
Saat ini, instans Linux mendukung login kata sandi dan kunci SSH, sedangkan instans Windows hanya mendukung login kata sandi. Untuk dokumentasi terkait hal ini, lihat:
- [Login ke Instans Linux](https://intl.cloud.tencent.com/document/product/213/5436)
- [Login ke Instans Windows](https://intl.cloud.tencent.com/document/product/213/5435)

### Mengapa saya tidak bisa menggunakan kata sandi untuk login ke instans Linux yang terkait dengan kunci SSH?
Setelah CVM dihubungkan dengan kunci SSH, login kata sandi **disabled by default** (dinonaktifkan secara default). Silakan [login ke instans Linux melalui kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501). 

### Bisakah saya menggunakan kunci SSH bersama dengan login kata sandi?
Saat Anda [login ke instans Linux melalui kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501), login kata sandi dinonaktifkan secara default untuk meningkatkan keamanan.

### Bagaimana cara membuat kunci SSH dan bagaimana jika saya kehilangan kunci tersebut?
Untuk informasi selengkapnya tentang pembuatan kunci, lihat [Mengelola kunci SSH](https://intl.cloud.tencent.com/document/product/213/16691).
Jika Anda kehilangan kunci, pecahkan masalah dengan metode berikut:
 - Buat kunci baru melalui [Kunci SSH](https://console.cloud.tencent.com/cvm/sshkey) di konsol dan ikat dengan instans asli.
  1. [Buat kunci SSH](https://intl.cloud.tencent.com/document/product/213/16691).
  2. Setelah kunci berhasil dibuat, login ke [Konsol CVM](https://console.cloud.tencent.com/cvm).
  3. Pilih instans asli yang ingin Anda ikat kuncinya, klik **More** (Selengkapnya) -> **Password/key** (Kata sandi/kunci) -> **Load a key** (Muat kunci). Selanjutnya, Anda bisa menggunakan kunci baru untuk login ke instans.
 - Atur ulang kata sandi Anda melalui Konsol CVM dan login ke instans menggunakan kata sandi baru Anda. Untuk informasi selengkapnya, lihat [Mengatur Ulang Kata Sandi Instans](https://intl.cloud.tencent.com/document/product/213/16566).

### Bagaimana cara mengikat/melepas kunci SSH ke atau dari server?

Untuk informasi selengkapnya, lihat bagian **Binding/Unbinding a key to or from a CVM** (Mengikat/Melepas kunci ke atau dari CVM) di [Mengelola kunci SSH](https://intl.cloud.tencent.com/document/product/213/16691).

### Bagaimana cara mengubah nama/deskripsi kunci SSH?

Untuk informasi selengkapnya, lihat bagian **Modifying the SSH key name and description** (Memodifikasi nama dan deskripsi kunci SSH) di [Mengelola kunci SSH](https://intl.cloud.tencent.com/document/product/213/16691).

### Bagaimana cara menghapus kunci SSH?

Untuk informasi selengkapnya, lihat bagian **Deleting SSH keys** (Menghapus kunci SSH) di [Mengelola kunci SSH](https://intl.cloud.tencent.com/document/product/213/16691).

### Berapa batas penggunaan kunci SSH?

Untuk informasi selengkapnya, lihat bagian **Use Limits** (Batas Penggunaan) di [SSH Keys](https://intl.cloud.tencent.com/document/product/213/6092).

### Bagaimana cara memecahkan masalah jika gagal login ke instans Linux menggunakan kunci SSH?

Untuk informasi selengkapnya, lihat [Tidak Bisa Login ke Instans Linux melalui SSH](https://intl.cloud.tencent.com/document/product/213/32486).

### Mengapa saya tidak bisa mengunduh kunci?
Kunci hanya bisa diunduh satu kali. Jika Anda kehilangan kunci, sebaiknya buat kunci baru, unduh, dan simpan.

### Bagaimana saya bisa menanyakan kunci mana yang digunakan oleh instans CVM?
Anda bisa login ke Konsol CVM dan membuka halaman detail instans untuk melihat kunci yang digunakan oleh CVM.
