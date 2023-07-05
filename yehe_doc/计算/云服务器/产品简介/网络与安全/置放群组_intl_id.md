Grup penempatan adalah kebijakan untuk mendistribusikan instans pada perangkat keras yang mendasarinya. Instans yang Anda buat di grup penempatan menampilkan pemulihan bencana dan ketersediaan tinggi saat diluncurkan. CVM Tencent Cloud menyediakan kebijakan penempatan instans, yang dapat memaksa instans disebarkan dengan kebijakan tertentu dan mengurangi dampak kegagalan perangkat keras/perangkat lunak yang mendasarinya pada layanan CVM. Anda dapat menggunakan grup penempatan untuk menerapkan instans CVM pada server fisik yang berbeda untuk memastikan ketersediaan layanan yang tinggi dan kemampuan pemulihan bencana yang mendasarinya. Saat Anda membuat instans dalam grup penempatan, kami akan meluncurkannya di wilayah tertentu sesuai dengan kebijakan deployment yang Anda konfigurasikan sebelumnya. Jika Anda tidak mengonfigurasi grup penempatan untuk instans, kami akan mencoba meluncurkannya di server fisik yang berbeda untuk memastikan ketersediaan layanan.

## Grup Penempatan Tersebar

Saat ini, grup penempatan yang tersebar didukung. Grup penempatan yang tersebar adalah grup instans yang ditempatkan pada perangkat keras dasar yang berbeda dan memiliki ketersediaan tinggi. Sebaiknya gunakan grup penempatan tersebar untuk aplikasi instans penting yang perlu ditempatkan secara terpisah, seperti database master/slave dan kluster dengan ketersediaan tinggi. Dengan meluncurkan instans dalam grup penempatan tersebar, Anda dapat meminimalkan kegagalan instans secara bersamaan dengan perangkat keras sama yang mendasarinya.
Grup penempatan yang tersebar bersifat spesifik wilayah dan dapat disebarkan di beberapa zona ketersediaan. Ada batasan jumlah instans yang dapat ditempatkan dalam grup. Untuk mengetahui informasi selengkapnya, lihat [Konsol](https://console.cloud.tencent.com/cvm/ps).

> Saat Anda meluncurkan instans dalam grup penempatan yang tersebar, permintaan akan gagal jika Anda memiliki perangkat keras yang tidak memadai. Anda dapat menunggu beberapa saat dan mencoba lagi.

## Aturan dan batasan grup penempatan yang tersebar

Sebelum menggunakan grup penempatan yang tersebar, perhatikan aturan berikut:
-  Grup penempatan tidak dapat digabungkan.
-  Instans tidak dapat ditempatkan di beberapa grup penempatan.
-  Grup penempatan yang tersebar dapat ditempatkan pada mesin fisik, switch, atau rak.
-  Jumlah maksimum instans yang didukung oleh grup penempatan yang tersebar pada mesin fisik, switch, atau rak adalah berbeda. Untuk mengetahui informasi selengkapnya, lihat situs web resmi.
-  Anda akan mengikuti kebijakan grup pemulihan bencana dengan ketat jika Anda menentukan dan menggunakannya. Harap perhatikan bahwa jika perangkat keras tidak memadai untuk mendistribusikan instans, pembuatan beberapa instans akan gagal.
-  Instans pada CDH tidak mendukung grup penempatan yang tersebar.

## Panduan Operasi
Untuk mengetahui informasi selengkapnya tentang operasi, lihat [Grup Penempatan Tersebar](https://intl.cloud.tencent.com/document/product/213/17020).
