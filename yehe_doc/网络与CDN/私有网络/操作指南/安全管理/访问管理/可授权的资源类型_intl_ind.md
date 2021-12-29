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

- **version** (versi) diperlukan. Saat ini, hanya nilai "2.0" yang diizinkan.
- **statement** (pernyataan) menjelaskan detail dari satu atau beberapa izin. Elemen ini berisi izin atau sekumpulan izin yang terdiri dari elemen lain seperti efek, tindakan, sumber daya, dan ketentuan. Setiap kebijakan memiliki satu elemen pernyataan.
 1. **action** (tindakan) menjelaskan tindakan yang diizinkan atau ditolak. Suatu tindakan dapat berupa API (dijelaskan menggunakan awalan "name") atau kumpulan fitur (satu kumpulan API tertentu, dijelaskan menggunakan awalan "permid"). Elemen ini diperlukan.
 2. **resource** (sumber daya) menjelaskan detail otorisasi. Sumber daya dijelaskan dalam format enam bagian. Definisi sumber daya terperinci berbeda-beda tergantung produk. Untuk informasi selengkapnya tentang cara menentukan sumber daya, lihat dokumentasi untuk produk dengan sumber daya yang pernyataannya ditulis. Elemen ini diperlukan.
 3. **condition** (kondisi) menjelaskan kondisi agar kebijakan diterapkan. Kondisi terdiri dari operator, kunci tindakan, dan nilai tindakan. Nilai kondisi dapat berisi informasi seperti waktu dan alamat IP. Beberapa layanan mengizinkan Anda untuk menentukan nilai tambahan dalam suatu kondisi. Elemen ini opsional.
 4. **effect** (efek) menjelaskan apakah hasil yang dibuat oleh pernyataan tersebut "allowed" (diizinkan) atau "denied" (ditolak). Elemen ini diperlukan.

## Operasi VPC
Dalam pernyataan kebijakan CAM, Anda dapat menentukan tindakan API apa pun dari layanan yang mendukung CAM. Untuk VPC, gunakan API dengan awalan "name/vpc:", misalnya name/vpc:Describe atau name/vpc:CreateRoute.
Untuk menentukan beberapa tindakan dalam satu pernyataan, pisahkan dengan koma, seperti yang ditunjukkan di bawah ini:
```
"action":["name/cvm:action1","name/cvm:action2"]
```

2. Anda juga dapat menentukan beberapa tindakan menggunakan karakter wildcard. Misalnya, Anda dapat menentukan semua API yang namanya dimulai dengan "Describe", seperti yang ditunjukkan di bawah ini:
```
"action":["name/cvm:Describe*"]
```

Untuk menentukan semua tindakan di VPC, gunakan karakter wildcard "*" sebagai berikut:
```
"action": ["name/cvm:*"]
```

## Jalur Sumber Daya VPC
Setiap pernyataan kebijakan CAM memiliki sumber dayanya sendiri.
Format umum jalur sumber daya adalah sebagai berikut:
```
****qcs**:project_id:service_type:region:account:resource**
```

- **project_id**: informasi proyek. Elemen ini hanya digunakan untuk mengaktifkan kompatibilitas dengan logika CAM lama dan dapat dibiarkan kosong.
**service_type**: singkatan dari produk, seperti CVM.
- **region** (wilayah): informasi wilayah, seperti bj.
- **account** (akun): akun dari pemilik sumber daya, seperti uin/164256472.
- **resource** (sumber daya): detail sumber daya setiap produk, seperti vpc/vpc_id1 atau vpc/*.

Misalnya, Anda dapat menentukan instans (vpc-d08sl2zr dalam kasus ini) dalam pernyataan, seperti yang ditunjukkan di bawah ini:
```
"resource":[ "qcs::vpc:bj:uin/164256472:instance/vpc-d08sl2zr"]
```

Anda juga dapat menggunakan karakter wildcard "*" untuk menentukan semua instans milik akun tertentu seperti yang ditunjukkan di bawah ini:
```
"resource":[ "qcs::redis:bj:uin/164256472:instance/*"]
```

Untuk menentukan semua sumber daya atau jika operasi API yang tidak mendukung izin tingkat sumber daya, Anda dapat menggunakan karakter wildcard "*" di `resource` seperti yang ditunjukkan di bawah ini:
```
"resource":["*"]
```

Untuk menentukan beberapa sumber daya dalam satu instruksi, pisahkan dengan koma. Dalam contoh berikut, dua sumber daya ditentukan:
```
"resource":["resource1","resource2"]
```


Tabel berikut menjelaskan sumber daya yang bisa digunakan VPC dan metode terkait untuk mendeskripsikan sumber daya ini.

Dalam tabel berikut, kata-kata berawalan "$" adalah semua nama alternatif.
- `project` menunjukkan ID proyek.
- `region` menunjukkan wilayah.
- `account` menunjukkan ID akun.

| Sumber Daya | Metode Deskripsi Sumber Daya dalam Kebijakan Otorisasi |
| ------ | ------------------------------------------ |
| VPC | qcs::vpc:$region:$account:vpc/$vpcId |
| Subnet | qcs::vpc:$region:$account:subnet/$subnetId |
| Grup keamanan | qcs::cvm:$region:$account:sg/$sgId |
| EIP | qcs::cvm:$region:$account:eip/*|
