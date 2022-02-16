<span id = "clyf"></span>
### Sintaksis Kebijakan
Kebijakan CAM:
```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"], 
               "condition": {"key":{"value"}} 
           } 
       ] 
} 
```

- **version** (versi) diperlukan. Saat ini, hanya versi "2.0" yang diizinkan.
- **statement** (pernyataan) menjelaskan detail berisi satu atau beberapa izin. Pernyataan ini berisi izin atau kumpulan izin dari beberapa elemen lain seperti `effect`, `action`, `resource`, dan `condition`. Satu kebijakan hanya memiliki satu `statement`.
 - **effect** (efek) menjelaskan apakah hasil pernyataan adalah "allow" (izinkan) atau "explicitly deny" (tolak secara eksplisit). Elemen ini diperlukan.
 - **action** (tindakan) menjelaskan tindakan (operasi) yang diizinkan atau ditolak. Operasi dapat berupa API atau kumpulan fitur (kumpulan API tertentu yang diawali dengan `permid`). Elemen ini diperlukan.
 - **resource** (sumber daya) menjelaskan objek yang dicakup oleh pernyataan. Sumber daya dijelaskan dalam format enam segmen. Definisi sumber daya terperinci bervariasi berdasarkan produk. Elemen ini diperlukan.
 - **condition** (kondisi) menjelaskan kondisi agar kebijakan dapat diterapkan. Kondisi terdiri dari operator, kunci tindakan, dan nilai tindakan. TcaplusDB saat ini tidak mendukung kondisi khusus, jadi item ini tidak dapat dikonfigurasi. Elemen ini diperlukan.

<span id = "cz"></span>
### Operasi TcaplusDB
Dalam pernyataan kebijakan CAM, Anda dapat menentukan operasi API apa pun dari layanan apa pun yang mendukung CAM. API yang diawali dengan `name/tcaplusdb:` harus digunakan untuk TcaplusDB, seperti `name/tcaplusdb:DescribeClusters` atau `name/tcaplusdb:DeleteCluster`.
Untuk menentukan beberapa operasi dalam satu pernyataan, pisahkan dengan koma seperti yang ditunjukkan di bawah ini:
```
"action":["name/tcaplusdb:action1","name/tcaplusdb:action2"]
```

Anda juga dapat menentukan beberapa operasi dengan menggunakan wildcard. Misalnya, Anda dapat menentukan semua operasi yang dimulai dengan "Jelaskan" pada nama seperti yang ditunjukkan di bawah ini:
```
"action":["name/tcaplusdb:Describe*"]
```

Jika Anda ingin menentukan semua operasi di TcaplusDB, gunakan wildcard "*" seperti yang ditunjukkan di bawah ini:
```
"action":["name/tcaplusdb:*"]
```

<span id = "zylj"></span> 
### Jalur Sumber Daya TcaplusDB

Setiap pernyataan kebijakan TcaplusDB memiliki sumber dayanya sendiri.
Jalur sumber daya umumnya dalam format berikut:

```
qcs:project_id:service_type:region:account:resource
```

**project_id** (project_id) menjelaskan informasi proyek, yang hanya digunakan untuk mengaktifkan kompatibilitas dengan logika CAM lama dan dapat dibiarkan kosong.
**service_type** (service_type) menjelaskan singkatan produk seperti `tcaplusdb`.
**region** (wilayah) menjelaskan [informasi wilayah](https://intl.cloud.tencent.com/document/product/213/6091), seperti ap-shanghai. Jika sumber daya tertentu ditentukan, tidak perlu memasukkan `region`.
**account** (akun) adalah akun akar dari pemilik sumber daya, seperti `uin/164xxx472`.
**resource** (sumber daya) menjelaskan informasi resource mendetail dari setiap produk, seperti cluster/19168929215 atau cluster/\* untuk sumber daya kluster, tempat kluster, grup tabel, dan tabel tidak dapat diautentikasi secara berjenjang. Jika Anda ingin mengontrol akses ke semua tabel atau grup tabel di kluster tertentu, Anda perlu mengonfigurasi autentikasi untuk tabel atau grup tabel selain kluster. Tabel di bawah ini menjelaskan sumber daya yang dapat digunakan oleh TcaplusDB dan metode deskripsi sumber daya yang sesuai.


| Sumber Daya   | Metode Deskripsi Sumber Daya dalam Kebijakan Otorisasi                                     |
| ------ | ------------------------------------------------------------ |
| Kluster    | qcs::tcaplusdb:$region:$account:cluster/$clusterId           |
| Grup tabel | qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId |
| Tabel    | qcs::tcaplusdb:$region:$account:table/$tableId |

Misalnya, Anda dapat menentukan sumber daya untuk kluster tertentu (ID kluster: 19168929215) dalam pernyataan seperti yang ditunjukkan di bawah ini:
```
"resource":[ "qcs::tcaplusdb:ap-shanghai:uin/164xxx472:cluster/19168929215"]
```

Anda juga dapat menggunakan wildcard "*" untuk menentukannya untuk semua kluster di wilayah Shanghai yang dimiliki oleh akun tertentu seperti yang ditunjukkan di bawah ini:
```
"resource":[ "qcs::tcaplusdb:ap-shanghai:uin/164xxx472:cluster/*"]
```

Jika Anda ingin menentukan semua sumber daya atau jika operasi API tertentu tidak mendukung kontrol izin tingkat sumber daya, Anda dapat menggunakan karakter pengganti "*" dalam elemen `resource` seperti yang ditunjukkan di bawah ini:
```
"resource": ["*"]
```

Untuk menentukan beberapa sumber daya dalam satu perintah, pisahkan dengan koma. Di bawah ini adalah contoh dengan dua kluster ditentukan:
```
"resource":["qcs::tcaplusdb::uin/164xxx472:cluster/19168929215","qcs::tcaplusdb::uin/164xxx472:cluster/21168929215"]
```
