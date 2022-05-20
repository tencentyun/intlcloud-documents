<span id = "celueyufa"></span>
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
- **statement** (pernyataan) menjelaskan detail dari satu atau beberapa izin. Elemen ini berisi izin atau sekumpulan izin yang terdiri dari elemen lain seperti efek, tindakan, sumber daya, dan ketentuan. Satu kebijakan hanya memiliki satu pernyataan.
4. **efek** menjelaskan apakah hasil yang dihasilkan oleh pernyataan tersebut adalah "allowed" (izinkan) atau "denied" (tolak). Elemen ini diperlukan.
- **action** (tindakan) menjelaskan tindakan (operasi) yang diizinkan atau ditolak. Operasi dapat berupa API (diawali dengan "sqlserver:"). Elemen ini diperlukan.
- **resource** (sumber daya) menjelaskan detail otorisasi. Sumber daya dijelaskan dalam format enam segmen. Definisi sumber daya mendetail berbeda-beda tergantung produk. Elemen ini diperlukan.
- **condition** (kondisi) menjelaskan kondisi agar kebijakan dapat diterapkan. Kondisi terdiri dari operator, kunci tindakan, dan nilai tindakan. Nilai kondisi dapat berisi informasi seperti waktu dan alamat IP. Beberapa layanan mengizinkan Anda untuk menentukan nilai tambahan dalam suatu kondisi. Elemen ini diperlukan.

<span id = "caozuo"></span>
## Operasi di TencentDB for SQL Server
Dalam pernyataan kebijakan TencentDB for SQL Server, Anda dapat menentukan operasi API apa pun dari setiap layanan yang mendukung TencentDB for SQL Server. API yang diawali dengan `sqlserver:` harus digunakan untuk TencentDB for SQL Server, seperti `sqlserver:DescribeDBInstances` atau `sqlserver:CreateAccount`.

Untuk menentukan beberapa operasi dalam satu pernyataan, pisahkan dengan koma seperti yang ditunjukkan di bawah ini:
```
"action":["sqlserver:action1","sqlserver:action2"]
```

Anda juga dapat menentukan beberapa operasi menggunakan wildcard. Misalnya, Anda dapat menentukan semua operasi yang dimulai dengan nama "Describe", seperti yang ditunjukkan di bawah ini:
```
"action":["sqlserver:Describe*"]
```

Jika Anda ingin menentukan semua operasi di TencentDB for SQL Server, gunakan wildcard seperti yang ditampilkan di bawah ini:
```
"action"：["sqlserver:*"]
```

<span id = "ziyuanlujing"></span> 
## Sumber Daya TencentDB for SQL Server
Setiap pernyataan kebijakan CAM memiliki sumber dayanya sendiri.
Sumber daya umumnya dalam format berikut:
```
qcs:project_id:service_type:region:account:resource
```

- **project_id** (project_id) menjelaskan informasi proyek, yang hanya digunakan untuk mengaktifkan kompatibilitas dengan logika CAM lama dan dapat dibiarkan kosong.
**service_type** (service_type) menjelaskan singkatan produk seperti sqlserver.
- **wilayah** menjelaskan informasi wilayah, seperti ap-guangzhou.
- **akun** adalah akun akar dari pemilik sumber daya, seperti uin/653339763.
- **sumber daya**: menjelaskan informasi sumber daya terperinci dari setiap produk, seperti instance/instance_id1 or instance/*.

Misalnya, Anda dapat menentukan sumber daya untuk instans tertentu (mssql-m8oh024t) dalam pernyataan seperti yang ditunjukkan di bawah ini:
```
"resource":[ "qcs::sqlserver:ap-guangzhou:uin/653339763:instance/mssql-m8oh024t"]
```

Anda juga dapat menggunakan wildcard "*" untuk menentukannya untuk semua instans yang dimiliki oleh akun tertentu seperti yang ditunjukkan di bawah ini:
```
"resource":[ "qcs::sqlserver:ap-guangzhou:uin/653339763:instance/*"]
```

Jika Anda ingin menentukan semua sumber daya atau operasi API tertentu tidak mendukung kontrol izin tingkat sumber daya, Anda dapat menggunakan Wildcard "*" di elemen "sumber daya" seperti yang ditunjukkan di bawah ini:
```
"resource": ["*"]
```

Untuk menentukan beberapa sumber daya dalam satu perintah, pisahkan dengan koma. Di bawah ini adalah contoh di mana dua sumber daya ditentukan:
```
"resource":["resource1","resource2"]
```

Tabel di bawah menjelaskan sumber daya yang dapat digunakan oleh TencentDB for SQL Server dan metode deskripsi sumber daya terkait, di mana kata-kata yang diawali dengan $ adalah placeholder, `project` mengacu pada ID proyek, `region` mengacu pada suatu wilayah, dan `account` mengacu pada ID akun.

| Sumber daya | Metode Deskripsi Sumber Daya dalam Kebijakan Otorisasi |
| :----- | :----------------------------------------------------------- |
| Instans   | ```qcs::sqlserver:$region:$account:instance/$instanceId``` |
| VPC    | ```qcs::vpc:$region:$account:vpc/$vpcId```                   |
| Grup keamanan | ```qcs::cvm:$region:$account:sg/$sgId```                     |
