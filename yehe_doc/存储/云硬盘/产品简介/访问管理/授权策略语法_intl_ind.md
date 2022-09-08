
<span id = "celueyufa"></span>
### Sintaks Kebijakan
Kebijakan CAM:
```json
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

- **version** (versi): wajib diisi.Saat ini, satu-satunya nilai yang valid adalah `"2.0"`.
- **statement** (pernyataan): menjelaskan informasi mendetail dari satu atau beberapa izin.Setiap izin terdiri dari satu set elemen termasuk efek, tindakan, sumber daya, dan kondisi.Sebuah kebijakan hanya memiliki satu elemen pernyataan.
1. **action** (tindakan): **wajib diisi**.Ini menjelaskan operasi yang diizinkan atau ditolak, yang dapat berupa API (dijelaskan dengan awalan "name") atau set fitur (satu set API tertentu yang dijelaskan dengan awalan "permid").
2. **resource** (sumber daya): **wajib diisi**.Ini menjelaskan data spesifik yang akan diotorisasi dalam format enam segmen.Definisi sumber daya mendetail berbeda-beda tergantung produk.
3. **condition** (kondisi): opsional.Ini menjelaskan kondisi untuk kebijakan yang akan berlaku.Kondisi terdiri dari operator, kunci operasi, dan nilai operasi.Nilai kondisi dapat berisi informasi seperti waktu dan alamat IP.Beberapa layanan memungkinkan Anda untuk menentukan informasi lain dalam kondisi.
4. **effect** (efek): **wajib diisi.** Ini menjelaskan hasil yang dikembalikan oleh pernyataan, yaitu, apakah izin diizinkan ("allow") atau ditolak ("deny").


## Operasi CBS[](id:caozuo)

Dalam pernyataan kebijakan CAM, Anda dapat menentukan berbagai operasi API dari berbagai layanan yang mendukung CAM.Untuk CBS, gunakan API yang diawali dengan `name/cvm:`, misalnya, `name/cvm:CreateDisks` atau `name/cvm:DescribeDisks`.
Untuk menentukan beberapa operasi dalam satu pernyataan, pisahkan dengan koma, seperti yang ditunjukkan di bawah ini.
```
"action":["name/cvm:action1","name/cvm:action2"]
```
Anda juga dapat menggunakan kartubebas untuk menentukan beberapa operasi.Misalnya, Anda dapat menentukan semua operasi yang namanya dimulai dengan "Describe", seperti yang ditunjukkan di bawah ini.
```
"action":["name/cvm:Describe*"]
```
Untuk menentukan semua operasi di CVM, gunakan kartubebas `*` sebagai berikut.
```
"action":["name/cvm:*"]
```


## Jalur Sumber Daya CBS[](id:ziyuanlujing)
Setiap pernyataan kebijakan CAM berisi sumber daya yang berlaku untuk kebijakan itu sendiri.Format umum jalur sumber daya ditunjukkan di bawah ini.
```
qcs:project_id:service_type:region:account:resource
```
- **project_id** (id_proyek): menunjukkan informasi proyek, yang hanya digunakan untuk mengaktifkan kompatibilitas dengan logika CAM sebelumnya.Elemen ini dapat dibiarkan kosong.
- **service_type** (jenis_layanan): menunjukkan nama pendek suatu produk, misalnya, "CVM".
- **region** (wilayah): menunjukkan informasi wilayah, misalnya, "bj".
- **account** (akun): menunjukkan akun root dari pemilik sumber daya, misalnya, "uin/164256472".
- **resource** (sumber daya): menunjukkan sumber daya tertentu dari suatu produk, misalnya, "volume/diskid1" atau "volume/*".

Anda dapat menentukan sumber daya CBS dalam pernyataan, misalnya, "disk-abcdefg", seperti yang ditunjukkan di bawah ini.
```
"resource":[ "qcs::cvm:bj:uin/164256472:volume/disk-abcdefg"]
```
Anda juga dapat menggunakan kartubebas `*` untuk menentukan semua sumber daya CBS di bawah akun, seperti yang ditunjukkan di bawah ini.
```
"resource":[ "qcs::cvm:bj:uin/164256472:volume/*"]
```

Untuk menentukan semua sumber daya, atau jika operasi API tidak mendukung kontrol izin tingkat sumber daya, Anda dapat menggunakan kartubebas `*` di elemen sumber daya, seperti yang ditunjukkan di bawah ini.
```
"resource": ["*"]
```
Untuk menentukan beberapa sumber daya dalam satu pernyataan, pisahkan dengan koma.Dalam contoh berikut, dua sumber daya ditentukan.
```
"resource":["resource1","resource2"]
```


## Kunci Kondisi CBS[](id:tiaojianmiyue)
Dalam pernyataan kebijakan, Anda dapat memilih untuk menentukan kondisi agar kebijakan diterapkan.Setiap kondisi berisi satu atau beberapa pasangan nilai-kunci.Kunci kondisi tidak peka huruf besar/kecil.

- Jika Anda menentukan beberapa kondisi atau kunci dalam satu kondisi, kondisi dievaluasi dengan operator logika "AND".
- Jika Anda menentukan kunci dengan beberapa nilai dalam satu kondisi, kondisi dievaluasi dengan operator logika "OR".Izin hanya dapat diberikan setelah semua kondisi terpenuhi.
Tabel berikut menjelaskan kunci kondisi CBS yang digunakan untuk layanan tertentu.
<table class="tableblock frame-all grid-all spread">
<colgroup>
<col style="width: 15%;">
<col style="width: 15%;">
<col style="width: 70%;">

</colgroup>
<thead>
<tr>
<th class="tableblock halign-left valign-top">Kunci kondisi</th>
<th class="tableblock halign-left valign-top">Jenis Referensi</th>
<th class="tableblock halign-left valign-top">Pasangan Kunci-Nilai</th>
</tr>
</thead>
<tbody>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:region</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:region=<code>region</code></p>
</div>
<div class="ulist">
<ul>
<li>
dengan <code>region</code> menunjukkan wilayah (misalnya, "ap-guangzhou").</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm_disk_type=<code>disk_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p>di mana <code>disk_type</code> menunjukkan jenis disk (misalnya, "CLOUD_PREMIUM").</p>
</li>
</ul>
</div></div></td>
</tr>
</tbody>
</table>
