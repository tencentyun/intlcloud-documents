<span id="yufa"></span>

## Sintaksis Kebijakan CAM

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

- **version** (versi): wajib diisi. Saat ini, hanya versi "2.0" yang diizinkan.
- **pernyataan**: menjelaskan detail satu atau beberapa izin. Elemen ini berisi hak istimewa atau sekumpulan hak istimewa yang terdiri dari elemen lain seperti efek, tindakan, sumber daya, dan ketentuan. Satu kebijakan hanya memiliki satu pernyataan.
 - **efek**: menjelaskan apakah hasil yang dihasilkan oleh pernyataan tersebut adalah "izinkan" atau "tolak". Elemen ini diperlukan.
 - **tindakan**: menjelaskan tindakan (operasi) yang diizinkan atau ditolak. Operasi dapat berupa API atau kumpulan fitur (kumpulan API tertentu yang diawali dengan "permid"). Elemen ini diperlukan.
 - **sumber daya**: menjelaskan detail otorisasi. Sumber daya dijelaskan dalam format enam bagian. Definisi sumber daya mendetail berbeda-beda tergantung produk. Elemen ini diperlukan.
 - **kondisi**: menjelaskan kondisi agar kebijakan dapat diterapkan. Kondisi terdiri dari operator, kunci tindakan, dan nilai tindakan. Nilai kondisi dapat berisi informasi seperti waktu dan alamat IP. Beberapa layanan memungkinkan Anda untuk menentukan nilai tambahan dalam suatu kondisi. Elemen ini opsional.

<span id="caozuo"></span>

## Operasi Redis

Dalam pernyataan kebijakan CAM, Anda dapat menentukan berbagai operasi API dari berbagai layanan yang mendukung CAM. API yang diawali dengan "redis:" harus digunakan untuk Redis, seperti redis:CreateRedis atau redis:DeleteInstance.
Untuk menentukan beberapa tindakan dalam satu pernyataan, pisahkan dengan koma, seperti yang ditunjukkan di bawah ini:

```
"action":["redis:action1","redis:action2"]
```

Anda juga dapat menentukan beberapa tindakan menggunakan karakter pengganti. Misalnya, Anda dapat menentukan semua API yang namanya dimulai dengan "Describe", seperti yang ditunjukkan di bawah ini:

```
"action":["redis:Describe*"]
```

Jika Anda ingin menentukan semua operasi di Redis, gunakan wildcard "*" seperti yang ditunjukkan di bawah ini:

```
"action"：["redis:*"]
```

<span id="lujing"></span>

## Jalur Sumber Daya Redis

Setiap pernyataan kebijakan CAM memiliki sumber dayanya sendiri.
Format umum jalur sumber daya adalah sebagai berikut:

```
qcs:project_id:service_type:region:account:resource
```

- **project_id**: menjelaskan informasi proyek, yang hanya digunakan untuk mengaktifkan kompatibilitas dengan logika CAM lama dan dapat dibiarkan kosong.
**service_type**: menjelaskan singkatan produk seperti Redis.
  - **wilayah**: informasi wilayah, misalnya, bj.
- **akun**: akun dari pemilik sumber daya, seperti uin/653339763.
- **sumber daya**: menjelaskan informasi sumber daya terperinci dari setiap produk, seperti instance/instance_id1 atau instance/*.

Misalnya, Anda dapat menentukan sumber daya untuk instans tertentu (crs-psllioc8) dalam pernyataan seperti yang ditunjukkan di bawah ini:

```
"resource":[ "qcs::redis:bj:uin/12345678:instance/crs-psllioc8"]
```

Anda juga dapat menggunakan karakter pengganti "*" untuk menentukan semua instans milik akun tertentu seperti yang ditunjukkan di bawah ini:

```
"resource":[ "qcs::redis:bj:uin/12345678:instance/*"]
```

Jika Anda ingin menentukan semua sumber daya jika operasi API tertentu tidak mendukung kontrol izin tingkat sumber daya, Anda dapat menggunakan wildcard "*" di elemen "resource" seperti yang ditunjukkan di bawah ini:

```
"resource":["*"]
```

Untuk menentukan beberapa sumber daya dalam satu perintah, pisahkan dengan koma. Di bawah ini adalah contoh di mana dua sumber daya ditentukan:

```
"resource":["resource1","resource2"]

```

Tabel di bawah menjelaskan sumber daya yang dapat digunakan oleh Redis dan metode deskripsi sumber daya terkait, di mana kata-kata yang diawali dengan $ adalah placeholder, "region" meruju pada wilayah, dan "account" merujuk pada ID akun.

| Sumber daya       | Metode Deskripsi Sumber Daya dalam Kebijakan Otorisasi |
| -------------- | --------------------------------------------------- |
| Instans       | `qcs::redis:$region:$account:instance/$instanceId`  |
| VPC            | `qcs::vpc:$region:$account:vpc/$vpcId`              |
| Grup keamanan | `qcs::cvm:$region:$account:sg/$sgId`                |
