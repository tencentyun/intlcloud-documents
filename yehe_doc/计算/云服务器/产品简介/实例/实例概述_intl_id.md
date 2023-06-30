## Ringkasan Instans CVM
**Instans** adalah Cloud Virtual Machine (CVM). Ini berisi komponen komputasi dasar seperti CPU, memori, sistem operasi, jaringan, dan disk.

Instans CVM menyediakan layanan komputasi elastis di cloud dengan cara yang aman dan andal untuk memenuhi persyaratan komputasi. Seiring perubahan tuntutan bisnis, sumber daya komputasi dapat diskalakan secara real-time untuk menurunkan biaya perangkat lunak dan perangkat keras Anda serta menyederhanakan pekerjaan OPS TI.

Setiap jenis instans menawarkan kemampuan komputasi dan penyimpanan yang berbeda, sehingga cocok untuk kasus penggunaan yang berbeda. Anda dapat memilih kapasitas komputasi, penyimpanan, dan metode akses jaringan instans berdasarkan lingkup layanan yang perlu Anda sediakan. Untuk informasi selengkapnya tentang jenis instans dan kasus penggunaan, lihat [Jenis Instans](https://intl.cloud.tencent.com/document/product/213/11518). Setelah meluncurkan instans, Anda dapat menggunakannya seperti yang Anda lakukan pada komputer biasa. Anda juga akan memiliki kontrol penuh atas instans Anda.

## Citra Instans
**Citra** adalah templat yang berisi konfigurasi perangkat lunak (sistem operasi, program pra-penginstalan, dll.) yang diperlukan untuk meluncurkan instans CVM. Anda dapat menggunakan citra untuk meluncurkan instans atau beberapa instans berulang kali. Dengan kata lain, citra adalah "disk terinstal" dari CVM.

Tencent Cloud menyediakan jenis citra berikut:
 - Citra publik: tersedia untuk semua pengguna dan cocok untuk sistem operasi utama.
 - Citra kustom: hanya tersedia untuk pembuat dan pengguna yang saling berbagi citra. Citra kustom dibuat dari menjalankan instans atau diimpor dari sumber eksternal.
 - Citra yang dibagikan: dibagikan oleh pengguna lain. Citra tersebut hanya dapat digunakan untuk membuat instans.

Untuk informasi selengkapnya tentang citra, lihat [Ringkasan](https://intl.cloud.tencent.com/document/product/213/4940) atau [Ringkasan Jenis Citra](https://intl.cloud.tencent.com/document/product/213/4941).

## Penyimpanan Instans
Mirip dengan CVM normal, instans dapat disimpan di **disk sistem** dan **disk data**:
Disk sistem: mirip dengan drive C di sistem Windows. Disk sistem berisi salinan lengkap citra yang digunakan untuk meluncurkan instans dan lingkungan yang berjalan untuk instans. Disk sistem yang lebih besar dari citra yang digunakan diperlukan saat instans diluncurkan.
Disk data: mirip dengan drive D dan E di sistem Windows. Disk data menyimpan data pengguna dan mendukung perluasan, pemasangan, dan pelepasan yang fleksibel.

Disk sistem dan disk data mendukung berbagai jenis penyimpanan yang disediakan oleh Tencent Cloud. Untuk informasi selengkapnya, lihat [Ringkasan Penyimpanan](https://intl.cloud.tencent.com/document/product/213/4952).

## Keamanan Instans

Tencent Cloud menyediakan metode perlindungan keamanan instans berikut:
- [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601): ketika akun yang berbeda perlu mengontrol serangkaian sumber daya cloud yang sama, Anda dapat menggunakan kebijakan untuk mengontrol aksesnya ke sumber daya cloud.
- [Grup keamanan](https://intl.cloud.tencent.com/document/product/213/12452): Anda dapat menggunakan grup keamanan untuk mengontrol akses alamat tepercaya ke instans.
- Kontrol login: login ke instans Linux Anda menggunakan [kunci SSH](https://intl.cloud.tencent.com/document/product/213/6092) sebanyak mungkin. Jika Anda login ke instans Linux menggunakan [kata sandi login](https://intl.cloud.tencent.com/document/product/213/6093), ubah kata sandi Anda secara berkala.

