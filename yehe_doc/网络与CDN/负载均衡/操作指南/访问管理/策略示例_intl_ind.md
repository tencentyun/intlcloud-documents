## Kebijakan Akses Penuh untuk Seluruh Instance CLB
- Beri subakun akses penuh ke layanan CLB (membuat, mengelola, dll.).
- Nama kebijakan:CLBResourceFullAccess
```
{
"version":"2.0",
"statement": [{
"action": [
"name/clb:*"
		],
"resource": "*",
"effect": "allow"
	}]
}
```

## Kebijakan Baca-Saja untuk Seluruh Instance CLB
- Beri subakun akses baca-saja ke CLB (contoh: izin untuk menampilkan tetapi tidak dapat membuat, memperbarui, atau menghapus semua sumber daya CLB).Di konsol, prasyarat untuk memanipulasi sumber daya adalah kemampuan untuk menampilkan sumber daya sehingga sebaiknya Anda memberi subakun izin akses baca penuh ke CLB.
- Nama kebijakan:CLBResourceReadOnlyAccess
```
{
"version":"2.0",
"statement": [{
"action": [
"name/clb:Describe*"
		],
"resource": "*",
"effect": "allow"
	}]
}
```

## Kebijakan Akses Penuh untuk Layanan CLB Dengan Tag Tertentu
- Beri subakun akses penuh ke layanan CLB (membuat instance, mengelola pendengar, dll.) dengan tag tertentu (kunci tag: tagkey; nilai tag: tagvalue).
- Instance CLB mendukung konfigurasi tag dan menggunakan tag untuk autentikasi.

```
{
"version":"2.0",
"statement":[
        {
"effect":"allow",
"action":"*",
"resource":"*",
"condition":{
"for_any_value:string_equal":{
"qcs:tag":[
"tagkey&tagvalue"
                    ]
                }
            }
        }
    ]
}  
```
   
