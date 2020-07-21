## Process

API key is a common type of key used by client applications to establish trusted connections and data communications with backend servers. The following uses an API key as an example to describe the key protection solution provided by Tencent Cloud.

An API key is used in the following process: 
![](https://main.qcloudimg.com/raw/a5e7bc7248d12ea792a66519b200566f.jpg)

#### Process description

1. The admin logs into the KMS Console to create a white-box key.
2. The admin uses the white-box key management feature to encrypt the text to be encrypted (such as an API key) to get the ciphertext.
3. The admin distributes the decryption key and API key ciphertext generated in the previous two steps to the business developer or OPS engineer.
4. The business developer or OPS engineer deploys the white-box decryption key (ciphertext) on the user business server in the form of a file.
5. The business developer uses the API key ciphertext and initialization vector as input parameters of the business system.
6. The business developer integrates the white-box decryption SDK into the business system and uses the parameters in step 5 to decrypt the API key and dynamically get the API key plaintext in the memory for various operations such as access authentication.

As can be seen in the above process, the API key is not exposed to the open environment. Only the ciphertext of the API key and the required white-box decryption key are stored on the business server. After the white-box decryption algorithm and key are obfuscated, no additional plaintext key is needed for decryption, which ensures the security of the entire linkage. In response to the source code API key leak issue on GitHub, if the white-box key management solution is adopted, the plaintext of API keys will not be exposed in the source code, thereby preventing API keys from being used maliciously.

## Directions

### Step 1. Create a white-box key

The creation of a white-box key pair is achieved by calling the white-box service through the console or API.

The samples below are called with [TCCLI](https://intl.cloud.tencent.com/product/cli), which can also be called with any supported programming languages. Request command:

```plaintext
tccli kms CreateWhiteBoxKey --region ap-guangzhou --Alias test-gz01 --Description 'this is test for gz key' --Algorithm 'SM4'
```

Sample returned result:

```plaintext
{
    "Response": {
        "RequestId": "55f7ca05-17af-4bfb-87a5-80a80a4b0761",
        "EncryptKey": "BA4AADZhzTBr7vmCDyHwQRCKTSCXm8pnGs38mJfA1Pw+VaP8/MW+lSCTYIi/0AUsido39JWw2XkvrnmauXsU3cemHQ+bcpofelLB2nS2ShCINi9MTSS/KgAKhvQPD5jXtbbmUSiBcKLTMXxH6MZXcPyGvEmqe3SrhvqflQk4bL/uUxAW1IC4p7E07pn6RQr2zMZAdkK0IciuwV23+cp25x2G/fEGtZi46YZR48tb2ZciGQ5kzS8se/CJM+lTqdBwAHV6yvPVQaXS16NFp4UhAtGCRZVfMQCp56hkhEryGjtxvIz4qfgCZ4bEo3Xp2DnNtzwBmtRBnCXl2PbLABRfGZ9ZX7uN3IMv3rJ1mRJWJh2eBHR1N+ujO7bGTqYHIb9VxxafQ/D9PHhGO3LeQRrNi1LS31XClvVNqNR8p/gc4GQCs987q0vdXC2PfinEV0fkyAKzis6096Jo7gfK+QvjYgVNRPr0nVuKKMI60zDKHG5jnN5kRKuTYfhl2tppFQO2WpvCLPHQH3DcX2FZGAgmvV1yjMSp79dOgS3tnbHn8fPNIEYdziQgYV0+ce4r****",
        "DecryptKey": "CA4AAEFLh2SUfMm1UIuxgTiD7g/rBKlxShZ/5jxRByvOqgtNyx42vDGACEtPYZwOXIhCn5wnpnisA+ZlDd3oYnmbqO9cG9KzczsHy3x6ymlpsIfw46PB2ostz755947ykzbi71G0osTvqo9rJFrVjQpcfu7/P8iKbJhI5Y/W2CIMuhJdbrQhXl6xyYILnhAV+o4D+c3MgzpkzB/zovcWr7EoDCDcLn4730e96ubN/+BbA9opz11jMymCJsx6PHsrfd6jzis4ZzDV+Uq+jYd5IJHGhmXaaQoeX2Shi+b9lOHuLi/MFqwjoskNMZ17xhc1e7l3lHpQQMIk3dYfnK3UI+6t2D3QoRCz8ytRCfI2uRHtKGZUPYl2586iJ+48lJ7/cWLlRwsypYUv73Oas0KnuRqGCilG2dwpIW7P/0CAqO09hN7ti+IMbiVK4dHF8aJB24A9SAHpN1ZejZbduHACPBDfb5jyMdBegswiip9qdtRzHfP9CU1ozVRXt/8jt0iJdib6nEuvjHuFDauVuZk1ahd9MUqhdK3zKBBHdH9uP+EyiYu8w88+N0XOEMWv****",
        "KeyId": "1c820b96-73bd-11ea-a490-5254006d0810"
    }
}
```

> !
> - Currently, supported encryption algorithms include SM4 and AES_256.
> - The returned `EncryptKey` and `DecryptKey` are the encryption key and decryption key respectively, and they are both Base64-encoded.

### Step 2. Bind device fingerprint (optional)

1. Log in to the device whose fingerprint is to be captured, run the fingerprint capture tool (getDeviceFingerprint), and get a 70-bit string, which is the device fingerprint.
2. Upload the captured device fingerprint list and bind it to a specified white-box key through the [KMS Console](https://console.cloud.tencent.com/kms2/whitebox) or [API](https://intl.cloud.tencent.com/document/product/1030/37086). For more information and detailed directions, please see [Device Binding Guide](https://intl.cloud.tencent.com/document/product/1030/37264).

>? The fingerprint capture tool (getDeviceFingerprint) can be downloaded directly in the [KMS Console](https://console.cloud.tencent.com/kms2/whitebox).

Request command:

```plaintext
tccli kms OverwriteWhiteboxDeviceFingerprints --region ap-guangzhou --KeyId 1c820b96-73bd-11ea-a490-5254006d****  --DeviceFingerprints '[{"Identity":"c19c024c-2ba1-11b2-a85c-96f970f4****","Description":"10.0.0.1 KMS device"}]'
```

Sample returned result:

```plaintext
{
    "Response": {
        "RequestId": "55f7ca05-17af-4bfb-87a5-80a80a4b0761",
     }
}
```

>!`DeviceFingerprints` will completely replace the fingerprint of the specified existing key. If `DeviceFingerprints` is empty, it means to delete all device fingerprints associated with the key.

### Step 3. Base64-encode the plaintext

Prepare the plaintext that needs to be managed with the white-box key and Base64-encode the plaintext. For example, if the plaintext to be encrypted is 1234567890, then the Base64-encoded result generated by running the `openssl` command is `MTIzNDU2Nzg5MAo=`.

```plaintext
echo 1234567890 | openssl base64
```

### Step 4. Encrypt the API key with the white-box key

Request command:

```plaintext
tccli kms EncryptByWhiteBox --region ap-guangzhou --KeyId a1a9376a-7261-11ea-a490-5254006d**** --PlainText MTIzNDU2Nzg5MAo=
```

Returned result:

```plaintext
{
    "Response": {
        "RequestId": "1bf315d1-3b20-4089-b458-51c367967b4b",
        "InitializationVector": "EUi3Vv7DiCf73D6XbVzMYg==",
        "CipherText": "HKyXV1Xoodi1P/sdf/cYLw=="
    }
}
```

> !There are two main fields returned:
> - InitializationVector: randomly generated initialization vector (Iv), which is used to increase the difficulty of cracking the ciphertext.
> - CipherText: Base64-encoded ciphertext after encryption.

### Step 5. Distribute the white-box decryption key and API key ciphertext

The admin distributes the `DecryptKey`, `InitializationVector` and `CipherText` generated in the above steps to the development or OPS personnel of each business system. Among them, `DecryptKey` will be deployed to the file in the corresponding business system, and `InitializationVector` and `CipherText` will be used as the input parameters of the SDK.

Here:

1. The decryption key (DecryptKey) needs to be saved in the form of a binary file for read when the system is started. The operation commands are as follows:
   1. Save the `DecryptKey` to a file.
	```plaintext
	echo "CA4AAEFLh2SUfMm1UIuxgTiD7g/rBKlxShZ/5jxRByvOqgtNyx42vDGACEtPYZwOXIhCn5wnpnisA+ZlDd3oYnmbqO9cG9KzczsHy3x6ymlpsIfw46PB2ostz755947ykzbi71G0osTvqo9rJFrVjQpcfu7/P8iKbJhI5Y/W2CIMuhJdbrQhXl6xyYILnhAV+o4D+c3MgzpkzB/zovcWr7EoDCDcLn4730e96ubN/+BbA9opz11jMymCJsx6PHsrfd6jzis4ZzDV+Uq+jYd5IJHGhmXaaQoeX2Shi+b9lOHuLi/MFqwjoskNMZ17xhc1e7l3lHpQQMIk3dYfnK3UI+6t2D3QoRCz8ytRCfI2uRHtKGZUPYl2586iJ+48lJ7/cWLlRwsypYUv73Oas0KnuRqGCilG2dwpIW7P/0CAqO09hN7ti+IMbiVK4dHF8aJB24A9SAHpN1ZejZbduHACPBDfb5jyMdBegswiip9qdtRzHfP9CU1ozVRXt/8jt0iJdib6nEuvjHuFDauVuZk1ahd9MUqhdK3zKBBHdH9uP+EyiYu8w88+N0XOEMWv****" > decrypt_key.base64
	2. Base64-decode the public key to get its content:
	openssl enc -d -base64 -A -in decrypt_key.base64 -out decrypt_key.bin
	3. Put the generated binary file `decrypt_key.bin` in the specified directory `decrypt_key_bin_dir` on the same server as the business system (with the decryption SDK integrated).
	```
2. Use `InitializationVector`, `CipherText`, `decrypt_key_bin_dir`, and `decrypt_key.bin` in the form of strings as the input parameters of the `whitebox_decrypt` method in the SDK.

### Step 6. Deploy the white-box decryption key

Each business system chooses to download the language-specific decryption SDK in the corresponding programming language and integrates the SDK into the business system.

### Step 7. Use the API key ciphertext

Call the decryption function (whitebox_decrypt) of the SDK in the business logic by passing in the parameters `decrypt_key_bin_dir`, `decrypt_key.bin`, `InitializationVector`, `CipherText`, and `algorithmType` to get the decrypted plaintext. Here, `algorithmType` is the algorithm type used when the key is generated (valid values: 0, 1. 0: AES_256, 1: SM4).

## Sample Code

The following uses Go, Python, C, and Java as examples to provide code samples:

### Sample decryption code for Go

```
package main

import (
   "encoding/base64"
   "fmt"
   "unsafe"
)

/*
#cgo CFLAGS: -I./include
#cgo LDFLAGS: -L./lib -lydwbcrypto
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include "wrp.h"

static int clt_load_key(WRP_KEY_CTX *key_ctx, char *decrypt_key_path, const char *file_name, uint32_t mode, uint32_t algoType) {
   printf("begin to load key in dir: %s\n", decrypt_key_path);
    printf("begin to load key: %s\n", file_name);
    int err;
    const WRP_KEY* keyalg = WRP_KEY_wbaes();
   if (algoType == 1) { keyalg = WRP_KEY_wbsm4(); }

    err = WRP_KEY_init(key_ctx, keyalg, 0);
    if (err) { printf("Err: orig_byte init\n"); goto end; }

    err = WRP_KEY_ctrl(key_ctx, WRP_KEY_CTRL_WB_SET_PATH, decrypt_key_path, strlen(decrypt_key_path));
    if (err) { printf("Err: set path\n"); goto end; }

    err = WRP_KEY_import(key_ctx, file_name, mode);
    if (err) { printf("Err: WRP_KEY_import error: %d, \n", err); goto end; }

end:
    return err;
}


int demo_clt_cbc_dec(char * file_dir, const char * file_name, uint8_t* ciph, uint32_t ciphlen, char* iv, uint32_t algoType, uint8_t* out, uint32_t* outlen) {
    WRP_KEY_CTX *mykey;
    WRP_CIPHER_CTX *myaes = NULL;

    uint32_t bits;
    ERRNO err = ERRNO_OK;

    const WRP_CIPHER* alg = WRP_wbaes_cbc();
   if (algoType == 1) { alg = WRP_wbsm4_cbc(); }

    // IO: load wbkey
    mykey = WRP_KEY_CTX_new();
    err = clt_load_key(mykey, file_dir, file_name, KEYMODE_DECRYPT, algoType);
    if (err) { printf("load whitebox key error: %d\n", err); goto cleanup; }

    printf("load key success\n");
    bits = WRP_KEY_key_len(mykey, KEYLEN_TYPE_BITS);
    printf("key len=%u\n", bits);

    if (bits == 0) { printf("get whitebox key length error\n"); err=-1; goto cleanup; }

    // crypto
    myaes = WRP_CIPHER_CTX_new();

    err = WRP_CIPHER_Decrypt_init(myaes, alg, mykey, iv);
    if (err) { printf("Dec: init Err**\n"); goto cleanup; }
    printf("decrypt init success, begin to decrypt cipher\n");

    err = WRP_CIPHER_Decrypt_doCipher(myaes, ciph, ciphlen, out, outlen);
    if (err) { printf("decrypt error: %.8X\n", err); goto cleanup; }
    //printf("decrypt success\n");
    //printf("output: %s\n", deout);
    //printf("\n");

cleanup:
    WRP_KEY_CTX_free(mykey);
    WRP_CIPHER_CTX_free(myaes);
    return err;
}
*/
import "C"

/**
algorithmType = 0 : AES_256
algorithmType = 1 : SM4
*/
func whitebox_decrypt(decrypt_key_bin_dir string, fileName string, Iv string, CipherText string, algorithmType int) {
   cipher, _ := base64.StdEncoding.DecodeString(CipherText)
   iv, _ := base64.StdEncoding.DecodeString(Iv)

   whitebox_decrypt_key_dir := C.CString(decrypt_key_bin_dir)
   defer C.free(unsafe.Pointer(whitebox_decrypt_key_dir))

   whitebox_decrypt_key := C.CString(fileName)
   defer C.free(unsafe.Pointer(whitebox_decrypt_key))

   //malloc a buffer which size is a little greater than your plaintext
   out_c := C.malloc(C.sizeof_char * 1024)
   defer C.free(unsafe.Pointer(out_c))
   outlen_c := 1024

   err_c := C.demo_clt_cbc_dec(whitebox_decrypt_key_dir, whitebox_decrypt_key,
      (*C.uchar)(unsafe.Pointer(&cipher[0])),
      C.uint(len(cipher)),
      (*C.char)(unsafe.Pointer(&iv[0])),
      C.uint(algorithmType),
      (*C.uchar)(out_c),
      (*C.uint)(unsafe.Pointer(&outlen_c)))
   if err_c != 0 {
      h := fmt.Sprintf("%X", err_c)
      fmt.Printf("decrypt error, error code: %d(hex %s)\n", err_c, h)
   } else {
      //plain := C.GoBytes(out_c, C.int(outlen_c))
      plain := C.GoString((*C.char)(out_c))
      fmt.Println(string(plain))
      fmt.Println("decrypt success")
      fmt.Println("output: ", plain)
      fmt.Println()
   }
}

func main() {
   fmt.Println("--------- test case for AES_256 ---------")
   // Decryption key file directory
   decryptKeyFileDirectoryName := "./data"
   // Decryption key filename
   decryptKeyFileName := "decrypt_key_aes256.bin"
   // Base64-encoded initialization vector
   iv := "EUi3Vv7DiCf73D6XbVzMYg=="
   // Base64-encoded ciphertext encrypted by white-box key
   cipherText := "HKyXV1Xoodi1P/sdf/cYLw=="
   // Encryption algorithm used to create white-box key. 0: AES_256, 1: SM4
   algoType := 0
   fmt.Println(fmt.Sprintf("demo start for decryptKeyFileName=%s, iv=%s, cipherText=%s, algoType=%d", decryptKeyFileName, iv, cipherText, algoType))

   whitebox_decrypt(decryptKeyFileDirectoryName, decryptKeyFileName, iv, cipherText, algoType)

   fmt.Println("--------- test case for SM4 ---------")
   // Decryption key file directory
   decryptKeyFileDirectoryName = "./data"
   // Decryption key filename
   decryptKeyFileName = "decrypt_key_sm4.bin"
   // Base64-encoded initialization vector
   iv = "9+COkyNOrT8mvWN6CgTjKw=="
   // Base64-encoded ciphertext encrypted by white-box key
   cipherText = "83ji4vKFwtVSAN1LSh1aOQ=="
   // Encryption algorithm used to create white-box key. 0: AES_256, 1: SM4
   algoType = 1
   fmt.Println(fmt.Sprintf("demo start for decryptKeyFileName=%s, iv=%s, cipherText=%s, algoType=%d", decryptKeyFileName, iv, cipherText, algoType))

   whitebox_decrypt(decryptKeyFileDirectoryName, decryptKeyFileName, iv, cipherText, algoType)

   fmt.Println("--------- test cases finished ---------")
}
```

### Sample decryption code for Python

```
#!/usr/bin/python

import os
from ctypes import *
import base64

ydwbcrypto = CDLL('../lib/libydwbcrypto.so')
ydwbcrypto.WRP_KEY_CTX_new.restype  = POINTER(c_int)
ydwbcrypto.WRP_KEY_wbsm4.restype  = POINTER(c_int)
ydwbcrypto.WRP_CIPHER_CTX_new.restype = POINTER(c_int)
ydwbcrypto.WRP_wbsm4_cbc.restype = POINTER(c_int)
KEYMODE_ENCRYPT = 4
KEYMODE_DECRYPT = 8
WRP_KEY_CTRL_WB_SET_PATH = 0x0003
KEYLEN_TYPE_BITS = 0

ydwbcrypto.WRP_KEY_wbaes.restype  = POINTER(c_int)
ydwbcrypto.WRP_wbaes_cbc.restype = POINTER(c_int)

def clt_load_key(key_ctx, decrypt_key_path, file_name, mode, algoType):
    print ("begin to load key: %s"%(file_name))
    keyalg = ydwbcrypto.WRP_KEY_wbaes()
    if algoType == 1:
        keyalg = ydwbcrypto.WRP_KEY_wbsm4()

    err = ydwbcrypto.WRP_KEY_init(key_ctx, keyalg, 0)
    if (err):
        raise YdwbCryptoException("Err: orig_byte init")

    err = ydwbcrypto.WRP_KEY_ctrl(key_ctx, WRP_KEY_CTRL_WB_SET_PATH, decrypt_key_path, len(decrypt_key_path))
    if (err):
        raise YdwbCryptoException("Err: set path")

    err = ydwbcrypto.WRP_KEY_import(key_ctx, file_name, mode)
    if (err):
        raise YdwbCryptoException("Err: WRP_KEY_import error: %.08X"%(err))

    pass

def demo_clt_cbc_dec(file_dir, file_name, ciph, iv, algoType):
    
    # IO: load wbkey
    mykey = ydwbcrypto.WRP_KEY_CTX_new()
    err = clt_load_key(mykey, file_dir, file_name, KEYMODE_DECRYPT, algoType)
    if (err):
        ydwbcrypto.WRP_KEY_CTX_free(mykey)
        raise YdwbCryptoException("load whitebox key error: %d"%(err))

    print ("load key success")
    bits = ydwbcrypto.WRP_KEY_key_len(mykey, KEYLEN_TYPE_BITS)
    print ("key len=%u"%(bits))

    if (bits == 0):
        ydwbcrypto.WRP_KEY_CTX_free(mykey)
        raise YdwbCryptoException("get whitebox key length error")

    # crypto
    myaes = ydwbcrypto.WRP_CIPHER_CTX_new()
    alg = ydwbcrypto.WRP_wbaes_cbc()
    if algoType == 1:
        alg = ydwbcrypto.WRP_wbsm4_cbc()
    err = ydwbcrypto.WRP_CIPHER_Decrypt_init(myaes, alg, mykey, iv)
    if (err):
        ydwbcrypto.WRP_KEY_CTX_free(mykey)
        ydwbcrypto.WRP_CIPHER_CTX_free(myaes)
        raise YdwbCryptoException("Dec: init Err**")

    print ("decrypt init success, begin to decrypt cipher")

    outlen = c_int(128)
    outlen_p = pointer(outlen)
    #create a buffer which size is a little greater than your plaintext
    deout = create_string_buffer(128)
    err = ydwbcrypto.WRP_CIPHER_Decrypt_doCipher(myaes, ciph, len(ciph), deout, outlen_p)
    if (err):
        ydwbcrypto.WRP_KEY_CTX_free(mykey)
        ydwbcrypto.WRP_CIPHER_CTX_free(myaes)
        raise YdwbCryptoException("decrypt error: %.8X"%(err))
    #print ("decrypt success")
    #print ("output: %s"%(deout))
    #print sizeof(deout), repr(deout.raw)
    
    ydwbcrypto.WRP_KEY_CTX_free(mykey)
    ydwbcrypto.WRP_CIPHER_CTX_free(myaes)
    return deout.raw

class YdwbCryptoException(Exception):
    def __init__(self, msg):
        self.msg = msg

if __name__ == "__main__":
    print("--------- test case for AES_256 ---------")
    # Decryption key file directory
    decryptKeyFileDirectoryName = "../data";
    # Decryption key filename
    decryptKeyFileName = "decrypt_key_aes256.bin"
    # Base64-encoded initialization vector
    iv = "EUi3Vv7DiCf73D6XbVzMYg=="
    # Base64-encoded ciphertext encrypted by white-box key
    cipherText = "HKyXV1Xoodi1P/sdf/cYLw=="
    # Encryption algorithm used to create white-box key. 0: AES_256, 1: SM4
    algoType = 0
    try:
        print("decryptKeyFileName=%s, iv=%s, cipherText=%s, algoType=%d" % (decryptKeyFileName, iv, cipherText, algoType))
        plain = demo_clt_cbc_dec(decryptKeyFileDirectoryName, decryptKeyFileName, base64.b64decode(cipherText), base64.b64decode(iv), algoType)
        print ("decrypt success")
        print ("plain: %s" % plain)
    except YdwbCryptoException as e:
        print (e.msg)

    print("--------- test case for SM4 ---------")
    # Decryption key file directory
    decryptKeyFileDirectoryName = "../data";
    # Decryption key filename
    decryptKeyFileName = "decrypt_key_sm4.bin"
    # Base64-encoded initialization vector
    iv = "9+COkyNOrT8mvWN6CgTjKw=="
    # Base64-encoded ciphertext encrypted by white-box key
    cipherText = "83ji4vKFwtVSAN1LSh1aOQ=="
    # Encryption algorithm used to create white-box key. 0: AES_256, 1: SM4
    algoType = 1
    try:

        print("decryptKeyFileName=%s, iv=%s, cipherText=%s, algoType=%d" % (decryptKeyFileName, iv, cipherText, algoType))
        plain = demo_clt_cbc_dec(decryptKeyFileDirectoryName, decryptKeyFileName, base64.b64decode(cipherText), base64.b64decode(iv), algoType)
        print ("decrypt success")
        print ("plain: %s" % plain)
    except YdwbCryptoException as e:
        print (e.msg)

    print("--------- test case finished  ---------")

    pass
```

### Sample decryption code for C

The sample code divides into Windows code and Linux code:

- Windows: open `demo.sln` in the `vs` folder. The demo uses VS 2017. There are two demos of static link and dynamic link respectively. Simply compile and run them. Due to path issues, if you use `exe` on the command line, you need to copy the `/data` directory to the upper-level directory.
- Linux: you need to add `lib` to environment variables:

```plaintext
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:../lib 
```

Below is sample code:

```
#include "../include/wrp.h"
#include "base64.h"
#include <stdint.h>
#include <stdio.h>
#include <string.h>

static char *decrypt_key_path = "../../data";

#define ALG_AES     1
#define ALG_SM4     2
#define TEST_BUFF_SIZE 100

static int clt_load_key(int alg_id, WRP_KEY_CTX *key_ctx, const char *key_file_path, uint32_t mode) 
{
    printf("begin to load key: %s\n", key_file_path);
    ERRNO err;

	const WRP_KEY*  myalg = NULL;

	switch (alg_id)
	{
	case ALG_AES:
		myalg = WRP_KEY_wbaes();
		break;
	case ALG_SM4:
		myalg = WRP_KEY_wbsm4();
		break;
	default:
		printf("algorithm not support\n");
		return -1;
	}
	if (myalg == NULL)
	{
		printf("encrypt algorithm invalidate. algorithm:%d.\n", alg_id);
		return -1;
	}

    err = WRP_KEY_init(key_ctx, myalg, 0);
    if (err) 
	{ 
		printf("Err: orig_byte init\n"); 
		goto end; 
	}

    err = WRP_KEY_ctrl(key_ctx, WRP_KEY_CTRL_WB_SET_PATH, decrypt_key_path, (uint32_t)strlen(decrypt_key_path));
    if (err) 
	{ 
		printf("Err: set path\n"); 
		goto end; 
	}

    err = WRP_KEY_import(key_ctx, key_file_path, mode);
    if (err) 
	{ 
		printf("Err: WRP_KEY_import error: %d, \n", err); 
		goto end; 
	}

end:
    return err;
}


void whitebox_decrypt(int alg_id, const char * key_file_path, uint8_t* ciph, uint32_t ciphlen, char* iv) 
{
    WRP_KEY_CTX *mykey;
    WRP_CIPHER_CTX *myaes = NULL;

    uint8_t deout[128] = { 0 };
    uint32_t outlen = sizeof(deout);
    uint32_t bits;
    ERRNO err = ERRNO_OK;

	const WRP_CIPHER* myalg = NULL;

	switch (alg_id)
	{
	case ALG_AES:
		myalg = WRP_wbaes_cbc();
		break;
	case ALG_SM4:
		myalg = WRP_wbsm4_cbc();
		break;
	default:
		printf("algorithm not support\n"); 
		return;
	}
    if (myalg == NULL)
    {
		printf("encrypt algorithm invalidate.algorithm:%d.\n", alg_id);
		return;
    }

    mykey = WRP_KEY_CTX_new();
    err = clt_load_key(alg_id, mykey, key_file_path, KEYMODE_DECRYPT);
    if (err) 
	{ 
		printf("load whitebox key error: %d\n", err); 
		goto cleanup; 
	}

    printf("load key success\n");
    bits = WRP_KEY_key_len(mykey, KEYLEN_TYPE_BITS);
    printf("key len=%u\n", bits);

    if (bits == 0) 
	{ 
		printf("get whitebox key length error\n"); 
		goto cleanup; 
	}

    // crypto
    myaes = WRP_CIPHER_CTX_new();

    err = WRP_CIPHER_Decrypt_init(myaes, myalg, mykey, iv);
    if (err) 
	{ 
		printf("Dec: init Err**\n"); 
		goto cleanup; 
	}
    printf("decrypt init success, begin to decrypt cipher\n");

    err = WRP_CIPHER_Decrypt_doCipher(myaes, ciph, ciphlen, deout, &outlen);
    if (err) 
	{ 
		printf("decrypt error: %.8X\n", err); 
		goto cleanup; 
	}
    printf("decrypt success\n");
    printf("output: %s\n", deout);
    printf("\n");

cleanup:
    WRP_KEY_CTX_free(mykey);
    WRP_CIPHER_CTX_free(myaes);
}

int demo_aes() 
{
	unsigned char cipher_base64[TEST_BUFF_SIZE] = "snPqPZaFN9CQc5WH/Tx5jA==";  //replace as your own cipher
	unsigned char cipher[TEST_BUFF_SIZE] = {0};
	int cipher_len = Base64decode(cipher, cipher_base64);
	if (cipher_len > TEST_BUFF_SIZE)
	{
		printf("base64 decode cipher text failed, memory is not enough.\n");
		return (-1);
	}

	unsigned char iv_base64[TEST_BUFF_SIZE] = "WBbaiNLcEYSbjKxoJt66UQ==";  //replace as your own iv
	unsigned char iv_bin[TEST_BUFF_SIZE] = { 0 };
	int iv_len = Base64decode(iv_bin, iv_base64);

	if (iv_len != 16)
	{
		printf("iv is not invalidate.\n");
		return (-1);
	}


    char * whitebox_decrypt_key = "decrypt_key_aes256.bin";   //replace as your own key
    whitebox_decrypt(ALG_AES, whitebox_decrypt_key, cipher, cipher_len, iv_bin);

    return 0;
}

int demo_sm4() 
{
	unsigned char cipher_base64[TEST_BUFF_SIZE] = "IwNgzruYfHQ6oQz2PLdyRQ=="; //replace as your own cipher
	unsigned char cipher[TEST_BUFF_SIZE] = {0};
    int cipher_len = Base64decode(cipher, cipher_base64);
	if (cipher_len > TEST_BUFF_SIZE)
	{
		printf("base64 decode cipher text failed, memory is not enough.\n");
		return (-1);
	}

	unsigned char iv_base64[TEST_BUFF_SIZE] = "4qaj6cVd8msMVBqNTRG4Pg==";  //replace as your own iv
	unsigned char iv_bin[TEST_BUFF_SIZE] = {0};
	int iv_len = Base64decode(iv_bin, iv_base64);

	if (iv_len != 16)
	{
		printf("iv is not invalidate.\n");
		return (-1);
	}

    char * whitebox_decrypt_key = "decrypt_key_sm4.bin";   //replace as your own key
    whitebox_decrypt(ALG_SM4, whitebox_decrypt_key, cipher, cipher_len, iv_bin);

    return 0;
}

int main(int argc, const char *argv[]) 
{
    demo_aes();
    demo_sm4();
    return 0;
}
```

### Sample decryption code for Java

```
import com.tencent.yunding.lightjce.CipherWhiteBox;
import com.tencent.yunding.lightjce.params.*;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.util.Base64;

public class Main {

    public static void main(String[] args) throws Exception {
        System.out.println("--------- test case for AES_256 ---------");
        // Decryption key file directory
        String decryptKeyFileDirectoryName = "../data";
        // Decryption key filename
        String decryptKeyFileName = "decrypt_key_aes256.bin";
        // Base64-encoded initialization vector
        String iv = "EUi3Vv7DiCf73D6XbVzMYg==";
        // Base64-encoded ciphertext encrypted by white-box key
        String cipherText = "HKyXV1Xoodi1P/sdf/cYLw==";
        // Encryption algorithm used to create white-box key. 0: AES_256, 1: SM4
        int algoType = 0;
        System.out.printf("demo start for decryptKeyFileName=%s, iv=%s, cipherText=%s, algoType=%d \n", decryptKeyFileName, iv, cipherText, algoType);
        whitebox_decrypt(decryptKeyFileDirectoryName, decryptKeyFileName, iv, cipherText, algoType);

        System.out.println("--------- test case for SM4 ---------");
        // Decryption key file directory
        decryptKeyFileDirectoryName = "../data";
        // Decryption key filename
        decryptKeyFileName = "decrypt_key_sm4.bin";
        // Base64-encoded initialization vector
        iv = "9+COkyNOrT8mvWN6CgTjKw==";
        // Base64-encoded ciphertext encrypted by white-box key
        cipherText = "83ji4vKFwtVSAN1LSh1aOQ==";
        // Encryption algorithm used to create white-box key. 0: AES_256, 1: SM4
        algoType = 1;
        System.out.printf("demo start for decryptKeyFileName=%s, iv=%s, cipherText=%s, algoType=%d \n", decryptKeyFileName, iv, cipherText, algoType);

        whitebox_decrypt(decryptKeyFileDirectoryName, decryptKeyFileName, iv, cipherText, algoType);

        System.out.println("--------- test case finished  ---------");

    }

    public static void whitebox_decrypt(String decrypt_key_bin_dir, String fileName, String Iv, String CipherText, int algorithmType) throws Exception {
        byte[] cipher = Base64.getDecoder().decode(CipherText);
        byte[] iv = Base64.getDecoder().decode(Iv);
        String decryptKeyFilePath = decrypt_key_bin_dir + "/" + fileName;

        if (algorithmType == 0) {
            byte[] result1 = decAESData(decryptKeyFilePath, cipher, iv);
            System.out.println("AES decrypted text length: " + result1.length);
            System.out.println("AES decrypted text       : " + new String(result1));
        } else if (algorithmType == 1) {
            byte[] result2 = decSM4Data(decryptKeyFilePath, cipher, iv);
            System.out.println("SM4 decrypted text length: " + result2.length);
            System.out.println("SM4 decrypted text       : " + new String(result2));
        }
    }

    public static byte[] readFile(String fileName) throws Exception {
        File file = new File(fileName);
        FileInputStream fileInputStream = new FileInputStream(file);
        if (file.canRead()) {
            try {
                int available = fileInputStream.available();
                byte[] result = new byte[available];
                int read = fileInputStream.read(result);
                return result;
            } finally {
                if (null != fileInputStream) {
                    fileInputStream.close();
                }
            }
        } else {
            throw new Exception("file can not be read.");
        }
    }

    public static void saveFile(String fileName, byte[] fileStream) throws Exception {
        File file = new File(fileName);
        File parentFile = file.getParentFile();
        if (!parentFile.exists()) {
            boolean mkdirs = parentFile.mkdirs();
        }
        if (!file.exists()) {
            boolean newFile = file.createNewFile();
        }
        if (file.canWrite()) {
            FileOutputStream fileOutputStream = new FileOutputStream(file);
            try {
                fileOutputStream.write(fileStream);
            } finally {
                if (null != fileOutputStream) {
                    fileOutputStream.close();
                }
            }
        } else {
            throw new Exception("file can not be write.");
        }
    }

    public static byte[] decAESData(String keyFilePath, byte[] data, byte[] iv) throws Exception {
        CipherWhiteBox instance = CipherWhiteBox.getInstance(SymAlgType.AES, BlockMode.cbc_mode, PaddingMode.p5padding);
        File file = new File(keyFilePath);
        instance.init(file, iv, CryptMode.decrypt_mode);
        instance.update(data);
        return instance.doFinal();
    }

    public static byte[] decSM4Data(String keyFilePath, byte[] data, byte[] iv) throws Exception {
        CipherWhiteBox instance = CipherWhiteBox.getInstance(SymAlgType.SM4, BlockMode.cbc_mode, PaddingMode.p5padding);
        File file = new File(keyFilePath);
        instance.init(file, iv, CryptMode.decrypt_mode);
        instance.update(data);
        return instance.doFinal();
    }

}
```
