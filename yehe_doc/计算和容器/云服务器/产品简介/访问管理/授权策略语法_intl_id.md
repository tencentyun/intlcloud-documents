
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
- **versi** diperlukan. Saat ini, hanya "2.0" yang didukung.
- **pernyataan** menjelaskan detail dari satu atau beberapa izin. Elemen ini berisi izin atau sekumpulan izin yang terdiri dari elemen lain seperti efek, tindakan, sumber daya, dan kondisi. Satu kebijakan hanya memiliki satu pernyataan.
 1. **Tindakan** menjelaskan tindakan yang diizinkan atau ditolak. Suatu tindakan dapat berupa API (dijelaskan menggunakan awalan "name") atau kumpulan fitur (satu kumpulan API tertentu, dijelaskan menggunakan awalan "permit"). Elemen ini diperlukan.
 2. **sumber daya** menjelaskan detail otorisasi. Sumber daya dijelaskan dalam format enam bagian. Definisi sumber daya terperinci berbeda-beda tergantung produk. Untuk informasi selengkapnya tentang cara menentukan sumber daya, lihat dokumentasi untuk produk yang relevan. Elemen ini diperlukan.
 3. **kondisi** menjelaskan kondisi agar kebijakan dapat diterapkan. Kondisi terdiri dari operator, kunci tindakan, dan nilai tindakan. Nilai kondisi dapat berisi informasi seperti waktu dan alamat IP. Beberapa layanan memungkinkan Anda untuk menentukan nilai tambahan dalam suatu kondisi. Elemen ini opsional.
 4. **efek** menjelaskan apakah hasil yang dihasilkan oleh pernyataan tersebut adalah "allowed" (izinkan) atau "denied" (tolak). Elemen ini diperlukan.

<span id = "caozuo"></span>
### Operasi CVM

Kebijakan CAM memungkinkan Anda melakukan operasi API di layanan Tencent Cloud apa pun yang mendukung CAM. Untuk CVM, gunakan awalan `name/cvm:` dengan API apa pun, seperti `name/cvm:RunInstances` atau `name/cvm:ResetInstancesPassword`.
Untuk menentukan beberapa tindakan dalam satu pernyataan, pisahkan dengan koma, seperti yang ditunjukkan di bawah ini:
```
"action":["name/cvm:action1","name/cvm:action2"]
```
Anda juga dapat menentukan beberapa tindakan menggunakan karakter pengganti. Misalnya, Anda dapat menentukan semua API yang namanya dimulai dengan "Describe", seperti yang ditunjukkan di bawah ini:
```
"action":["name/cvm:Describe*"]
```
Untuk menentukan semua operasi CVM, gunakan karakter pengganti "*" sebagai berikut:
```
"action": ["name/cvm:*"]
```

<span id = "ziyuanlujing"></span> 
### Jalur Sumber Daya CVM
Setiap kebijakan CAM mendefinisikan sumber dayanya sendiri.
Format umum jalur sumber daya adalah sebagai berikut:
```
qcs:project_id:service_type:region:account:resource
```
**project_id**: informasi proyek, yang hanya digunakan untuk tujuan kompatibilitas dan dapat dibiarkan kosong.
**service_type**: singkatan dari produk, seperti CVM.
**wilayah**: wilayah sumber daya, seperti bj.
- **akun**: akun dari pemilik sumber daya, seperti uin/164256472.
**sumber daya**: informasi sumber daya terperinci dari setiap produk, seperti instance/instance_id1 atau instance/*.

Misalnya, Anda dapat menentukan instans tertentu (i-15931881scv4) dalam pernyataan sebagai berikut:
```
"resource":[ "qcs::cvm:bj:uin/164256472:instance/i-15931881scv4"]
```
Anda juga dapat menggunakan karakter pengganti "*" untuk menentukan semua instans milik akun tertentu seperti yang ditunjukkan di bawah ini:
```
"resource":[ "qcs::redis:bj:uin/164256472:instance/*"]
```

Jika Anda ingin menentukan semua sumber daya atau jika ada operasi API yang tidak mendukung izin tingkat sumber daya, Anda dapat menggunakan karakter pengganti "*" di `resource` seperti yang ditunjukkan di bawah ini:
```
"resource":["*"]
```
Untuk menentukan beberapa sumber daya dalam satu instruksi, pisahkan dengan koma. Dalam contoh berikut, dua sumber daya ditentukan:
```
"resource":["resource1","resource2"]
```
Tabel berikut menjelaskan sumber daya CVM dan metode deskripsi sumber daya yang sesuai.
<style>
table th:nth-of-type(1){
width:250px;
}
table th:nth-of-type(2){
width:500px;
}
</style>
Dalam tabel berikut, nama dengan awalan $ adalah placeholder.
- $project adalah ID proyek.
- $region adalah wilayah sumber daya.
- $account adalah ID akun.

| Sumber daya | Sintaksis |
|-------|-------|
| Instans | qcs::cvm:$region:$account:instance/$instanceId |
| Kunci | qcs::cvm:$region:$account:keypair/$keyId |
| VPC | qcs::vpc:$region:$account:vpc/$vpcId |
| Subnet | qcs::vpc:$region:$account:subnet/$subnetId |
| Citra | qcs::cvm:$region:$account:image/\* |
| CBS |  qcs::cvm:$region:$account:volume/$diskid|
| Grup keamanan | qcs::cvm:$region:$account:sg/$sgId |
| EIP |  qcs::cvm:$region:$account:eip/*|

 

<span id = "tiaojianmiyue"></span>
### Kunci Kondisi CVM
Anda dapat menggunakan kondisi untuk menentukan kondisi di mana kebijakan berlaku. Setiap kondisi terdiri dari satu atau beberapa pasangan kunci. Ini tidak peka terhadap huruf besar-kecil.

- Jika Anda menentukan beberapa kondisi atau beberapa kunci dalam satu kondisi, itu terhubung dengan operator logika "DAN".
- Jika Anda menentukan kunci dengan beberapa nilai dalam satu kondisi, itu terhubung dengan operator logika "ATAU".
Tabel berikut menjelaskan kunci kondisi CVM untuk layanan tertentu.
<table class="tableblock frame-all grid-all spread">
<colgroup>
<col style="width: 25%;">
<col style="width: 25%;">
<col style="width: 50%;">
</colgroup>
<thead>
<tr>
<th class="tableblock halign-left valign-top">Kunci kondisi</th>
<th class="tableblock halign-left valign-top">Jenis referensi</th>
<th class="tableblock halign-left valign-top">Pasangan kunci</th>
</tr>
</thead>
<tbody>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:instance_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:instance_type=<code>instance_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>instance_type</code> adalah model dari instans CVM, seperti S1.SMALL1.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:image_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:image_type=<code>image_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>image_type</code> adalah jenis citra, seperti IMAGE_PUBLIC.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>vpc:region</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>vpc:region=<code>region</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>region</code> adalah wilayah instans CVM, seperti ap-guangzhou.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_size</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>Integer</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_size=<code>disk_size</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>disk_size</code> adalah ukuran disk, misalnya 500</p>
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
<p><code>disk_type</code> adalah jenis disk, seperti CLOUD_BASIC.</p>
</li>
</ul>
</div></div></td>
</tr>
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
<p><code>region</code> adalah wilayah instans CVM, seperti ap-guangzhou.</p>
</li>
</ul>
</div></div></td>
</tr>
</tbody>
</table>
