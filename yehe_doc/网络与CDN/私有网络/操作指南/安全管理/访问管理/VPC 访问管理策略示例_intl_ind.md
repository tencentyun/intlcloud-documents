## Kebijakan Izin Baca-tulis Penuh untuk VPC
Kebijakan berikut mengizinkan Anda membuat dan mengelola instans VPC. Anda dapat menghubungkan kebijakan ini dengan sekelompok admin jaringan. Elemen `Action` menentukan semua API terkait VPC.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/vpc:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
## Kebijakan Izin Baca Saja untuk VPC
Kebijakan berikut mengizinkan Anda mengkueri VPC Anda dan sumber daya yang relevan. Namun, Anda tidak dapat membuat, memperbarui, atau menghapusnya dengan kebijakan ini.
Sebaiknya berikan izin baca-saja VPC untuk pengguna, karena pengguna harus dapat melihat sumber daya untuk mengoperasikannya di konsol.

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/vpc:Describe*",
                "name/vpc:Inquiry*",
                "name/vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

## Mengizinkan Sub-Akun untuk Mengelola VPC Tunggal Saja
Kebijakan berikut mengizinkan pengguna untuk melihat semua instans VPC tetapi hanya dapat mengoperasikan VPC A (misalnya, VPC A dengan ID vpc-d08sl2zr) dan sumber daya jaringan di VPC A (seperti subnet dan tabel rute, tetapi tidak termasuk komputer virtual cloud (CVM) dan database). Dengan kata lain, pengguna tidak diizinkan untuk mengelola instans VPC lainnya.
Versi ini tidak mendukung **allowing the user to view VPC A only** (mengizinkan pengguna melihat VPC A saja) yang akan didukung di versi mendatang.

```
{
    "version": "2.0",
    "statement": [
        {
            "action": "name/vpc:*",
            "resource": "*",
            "effect": "allow",
            "condition": {
                "string_equal_if_exist": {  //Conditional judgment: hanya instans yang memenuhi syarat yang dapat dikelola
                    "vpc:vpc": [
                    "vpc-d08sl2zr"
                    ],
                    "vpc:accepter_vpc": [
                     "vpc-d08sl2zr"
                    ],
                     "vpc:requester_vpc": [
                     "vpc-d08sl2zr"
                    ]
                }
            }
        }
    ]
}
```

## Mengizinkan Pengguna Mengelola Instans VPC tetapi Tidak Mengoperasikan Tabel Rute
Kebijakan berikut mengizinkan pengguna untuk membaca dan menulis instans VPC dan sumber daya yang relevan, tetapi tidak mengizinkan pengguna untuk mengoperasikan tabel rute.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/vpc:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/vpc:AssociateRouteTable",
                "name/vpc:CreateRoute",
                "name/vpc:CreateRouteTable",
                "name/vpc:DeleteRoute",
                "name/vpc:DeleteRouteTable",
                "name/vpc:ModifyRouteTableAttribute"
            ],
            "resource": "*",
            "effect": "deny"
        }
    ]
}
```

## Mengizinkan Pengguna Mengelola Sumber Daya VPN
Kebijakan berikut mengizinkan pengguna untuk melihat semua sumber daya VPC dan hanya mengizinkan pengguna untuk membuat, membaca, memperbarui, dan menghapus (CRUD) sumber daya VPN.

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/vpc:Describe*",
                "name/vpc:Inquiry*",
                "name/vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/vpc:*Vpn*",
                "name/vpc:*UserGw*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
