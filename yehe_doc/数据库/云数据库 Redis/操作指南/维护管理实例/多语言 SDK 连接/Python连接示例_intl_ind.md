**Persiapan sebelum menjalankan**:
Unduh dan instal [redis-py](https://github.com/andymccurdy/redis-py?spm=5176.730001.3.11.WvETSA).

**Kode Sampel**:

```
#!/usr/bin/env python 
#-*- coding: utf-8 -*- 
impor redis 

#Ganti dengan host dan port instans yang terhubung di sini 
host = '192.168.0.195' 
port = 6379 

#Ganti dengan ID instans dan kata sandi instans di sini 
user='username' 
pwd='password' 

#Saat menghubungkan, tentukan informasi AUTH melalui parameter kata sandi dalam format user+'@'+pwd 
r = redis.StrictRedis(host=host, port=port, password=user+'@'+pwd) 

#Operasi database dapat dilakukan setelah koneksi dibuat. Untuk informasi selengkapnya, lihat https://github.com/andymccurdy/redis-py 
r.set('name', 'python_test'); 
print r.get('name')
```

**Hasil eksekusi**:
![](https://main.qcloudimg.com/raw/b819ac84617439c8dcb107b0d7f4c641.png)
