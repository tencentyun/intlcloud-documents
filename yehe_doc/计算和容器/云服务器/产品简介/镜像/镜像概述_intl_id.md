## Apa Itu Citra?
Citra adalah salinan serial dari seluruh status sistem komputer yang disimpan sebagai file. Anda dapat menganggap citra sebagai disk penginstalan sistem. Ini berisi semua yang Anda butuhkan untuk meluncurkan instans CVM. Sebuah citra dapat meluncurkan instans CVM sebanyak yang Anda inginkan, dan Anda dapat meluncurkan instans CVM dari sebanyak citra yang Anda inginkan. 

## Jenis Citra
Tencent Cloud menyediakan jenis citra berikut:
- **Citra publik**: tersedia untuk semua pengguna dan mencakup sebagian besar sistem operasi utama.
- **Citra khusus**: hanya tersedia untuk pemilik dan pengguna yang berbagi citra dengannya. Citra kustom dibuat dari instans atau diimpor dari sumber eksternal.
- **Citra yang dibagikan**: dibagikan oleh pengguna lain. Ini hanya dapat digunakan untuk membuat instans.

Untuk informasi selengkapnya tentang jenis citra, lihat [Jenis Citra](https://intl.cloud.tencent.com/document/product/213/4941).

## Kasus Penggunaan
 - **Men-deploy lingkungan perangkat lunak tertentu**
Untuk menyediakan layanan web atau mengembangkan aplikasi, Anda sering kali memerlukan perangkat lunak tertentu yang berjalan dalam lingkungan yang kohesif. Membangun lingkungan seperti itu dan menginstal perangkat lunak memakan waktu dan kompleks, itulah sebabnya Tencent Cloud sangat cocok untuk tugas demikian. Citra khusus dan citra yang dibagikan dapat membantu Anda memenuhi kebutuhan Anda dengan cepat dan mudah.
 - **Men-deploy lingkungan perangkat lunak dalam batch**
Anda dapat membuat citra dari instans dengan lingkungan yang di-deploy, lalu menggunakan citra untuk membuat instans dalam batch. Setelah pembuatan, instans ini akan memiliki lingkungan perangkat lunak yang sama dengan instans asli.
 - **Pencadangan lingkungan runtime server**
Anda dapat membuat citra kustom dari instans CVM untuk mencadangkan lingkungan runtime. Jika lingkungan rusak setelahnya, Anda dapat menggunakan citra untuk memulihkannya. 

## Siklus Pemakaian Citra

Berikut ini mengilustrasikan siklus pemakaian citra kustom. Setelah citra kustom dibuat atau diimpor, Anda dapat menggunakannya untuk meluncurkan instans CVM. Citra khusus dapat disalin ke wilayah lain dengan akun yang sama. Anda juga dapat berbagi citra khusus dengan pengguna lain.
![](http://mc.qcloudimg.com/static/img/b11a8e644fd89ce844c8fb0b69e7044a/image.png)


