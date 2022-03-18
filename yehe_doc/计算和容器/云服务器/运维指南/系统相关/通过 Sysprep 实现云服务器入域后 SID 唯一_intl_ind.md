## Ikhtisar
Untuk menggabungkan instans ke domain dan login ke Windows CVM dengan akun domain, Anda harus menjalankan Sysprep sebelum membuat citra kustom untuk memastikan SID unik. Jika tidak, instans tidak dapat digabungkan ke domain karena CVM yang dibuat dengan citra kustom dan instans asli berisi informasi yang identik, seperti SID duplikat. Lewati operasi ini jika Anda tidak perlu menggabungkan CVM Windows Anda ke domain.

Dokumen ini menjelaskan cara menjalankan Sysprep di sistem operasi Windows Server 2012 R2 64-bit untuk memastikan bahwa CVM Windows di domain ini sudah memiliki SID unik.

Untuk informasi selengkapnya tentang Sysprep, lihat `https://technet.microsoft.com/zh-cn/library/cc721940(v=ws.10).aspx`


## Catatan

- Windows CVM harus merupakan sistem operasi Windows asli dan aktif.
- Jika CVM Windows Anda dibuat dengan citra non-publik, Anda harus selalu menjalankan versi Sysprep yang disediakan dalam citra asli pada direktori `%WINDIR%\system32\sysprep`.
- Jumlah pengaturan ulang Windows yang tersisa harus lebih besar dari 1, jika tidak maka Sysprep tidak dapat dienkapsulasi.
Untuk memeriksa sisa jumlah pengaturan ulang Windows, jalankan perintah `slmgr.vbs /dlv`.
- Akun Cloudbase-Init menangani tindakan inisialisasi saat instans CVM diluncurkan. Jika Anda mengubah/menghapus akun ini atau menghapus penginstalan Couldbase-Init, Anda mungkin kehilangan informasi kustom saat menyediakan CVM baru dari citra kustom. Dengan demikian, kami tidak menyarankan untuk mengubah atau menghapus akun Cloudbase-init.   

## Prasyarat

1. [Login ke Windows CVM](https://intl.cloud.tencent.com/document/product/213/5435) sebagai Administrator.
- [Instal Cloudbase-Init di Windows CVM](https://intl.cloud.tencent.com/document/product/213/32364).

## Petunjuk

1. Di desktop, klik<img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png"></img> untuk membuka jendela Windows PowerShell.
2. Jalankan perintah berikut di jendela Windows PowerShell untuk masuk ke direktori instalasi alat Cloudbase-init.
> Asumsikan bahwa Cloudbase-init diinstal di `C:\Program Files\Cloudbase Solutions\`.
>
```
cd 'C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf'
```
3. Jalankan perintah berikut untuk mengenkapsulasi sistem Windows.
> 
> - Sertakan `/unattend:Unattend.xml` dalam perintah berikut, jika tidak, nama pengguna, kata sandi, dan konfigurasi CVM Anda saat ini akan diatur ulang. Jika Anda memilih **Follow image** (Ikuti citra) untuk login, Anda perlu mengatur ulang nama pengguna dan akun secara manual setelah peluncuran.
> - Setelah perintah berikut dijalankan, CVM otomatis dimatikan. Untuk memastikan bahwa CVM yang dibuat dari citra ini memiliki SID unik, jangan luncurkan instans CVM sebelum membuat citra kustom, atau tindakan ini hanya akan efektif untuk CVM saat ini.  
> - Setelah Anda menjalankan perintah berikut pada sistem operasi Windows Server 2012 atau Windows Server 2012 R2, Administrator akun dan kata sandi CVM-nya akan dihapus. Atur ulang akun dan kata sandi Anda setelah memulai ulang CVM seperti yang dijelaskan di [Atur Ulang Kata Sandi Instans](https://intl.cloud.tencent.com/document/product/213/16566).
> 
```
C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /unattend:Unattend.xml
```
4. Buat citra kustom dari instans CVM tempat eksekusi Sysprep, dan mulai instans CVM baru dengan citra tersebut. Lihat [Membuat Citra Kustom](https://intl.cloud.tencent.com/document/product/213/4942).
Dan sekarang, setiap instans CVM baru akan memiliki SID unik saat bergabung dengan domain.
> Untuk memeriksa CVM SID, jalankan perintah `whoami /user`.
>


