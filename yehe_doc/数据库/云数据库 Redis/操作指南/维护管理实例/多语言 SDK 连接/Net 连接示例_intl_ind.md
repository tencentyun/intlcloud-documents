
**Persiapan sebelum menjalankan**:
Unduh dan instal [ServiceStack.Redis](https://github.com/ServiceStack/ServiceStack.Redis).

**Kode sampel**:

- Jangan gunakan kumpulan koneksi

```
using System.Collections.Generic; 
using System.Linq; 
using System.Text; 
using ServiceStack.Redis; 
using System;

namespace ConsoleApplication1 
{ 
    class Program 
    { 
        static void Main(string[] args) 
       { 
           string host = "10.xx.xx.46";// Alamat host untuk mengakses instans 
           int port = 6379;// Informasi port 
           string instanceId = "bd87dadc-8xx1-4xx1-86dd-021xxxcde96";// ID Instans 
           string pass = "1234567q";// Kata sandi 

           RedisClient redisClient = new RedisClient(host, port, instanceId + ":" + pass); 
           string key = "name"; 
           string value = "QcloudV5!"; 
           redisClient.Set(key, value); // Atur nilai 
           System.Console.WriteLine("set key:[" + key + "]value:[" + value + "]"); 
           string getValue = System.Text.Encoding.Default.GetString(redisClient.Get(key)); // Baca nilai 
           System.Console.WriteLine("value:" + getValue); 
           System.Console.Read(); 
          } 
     } 
}
```

- Menggunakan kumpulan koneksi ServiceStack 4.0

```
using System.Collections.Generic; 
using System.Linq; 
using System.Text; 
using ServiceStack.Redis; 
using System;

namespace ConsoleApplication2 
{ 
    class Program 
    { 
        static void Main(string[] args) 
        { 
             string[] testReadWriteHosts = new[] {
             "redis://:fb92bxxxabf11e5:1234xx8a1A@10.x.x.1:6379"/*redis://:instance ID:password@access address:port*/
             };
             RedisConfig.VerifyMasterConnections = false;// Perlu diatur
             PooledRedisClientManager redisPoolManager = new PooledRedisClientManager(10/*connection pool quantity*/, 
             10/*connection pool timeout period*/, testReadWriteHosts);
             for (int i = 0; i < 100; i++)
            {
                 IRedisClient redisClient = redisPoolManager.GetClient();// Dapatkan koneksi
                 RedisNativeClient redisNativeClient = (RedisNativeClient)redisClient;
                 redisNativeClient.Client = null;// Perlu diatur
                 try
                {
                   string key = "test1111";
                   string value = "test1111";
                   redisClient.Set(key, value);
                   redisClient.Dispose();//
                }
                catch (Exception e)
                {
                    System.Console.WriteLine(e.Message);
                }
            }
            System.Console.Read();
         } 
     } 
}
```


- Gunakan kumpulan koneksi ServiceStack 3.0

```
using System.Collections.Generic; 
using System.Linq; 
using System.Text; 
using ServiceStack.Redis; 
using System;

namespace ConsoleApplication3 
{ 
  class Program 
  { 
     static void Main(string[] args) 
    { 
           string[] testReadWriteHosts = new[] {
               "fb92bfxxbf11e5:123456xx1A@10.x.x.1:6379" /*instance ID:password@access address:port*/
               };
               PooledRedisClientManager redisPoolManager = new PooledRedisClientManager(10/*connection pool
               quantity*/, 10/*connection pool timeout period*/, testReadWriteHosts);
               for (int i = 0; i < 100; i++)
              {
               IRedisClient redisClient = redisPoolManager.GetClient();// Dapatkan koneksi
               try
              {
                  string key = "test1111";
                  string value = "test1111";
                  redisClient.Set(key, value);
                  redisClient.Dispose();//
              } 
              catch (Exception e)
             {
                   System.Console.WriteLine(e.Message);
             }
          }
          System.Console.Read();
      } 
   } 
}
```

*Hasil eksekusi**:
![](https://main.qcloudimg.com/raw/c13571e24bd7818f4d678c1c13571502.jpg)

