Des encryption prevents a plaintext HTTP request from being maliciously tampered with during transmission. To use the encryption function, you need to apply for the enterprise edition. The specific usage is as follows:

## 1. Activating the Enterprise Edition
Only the enterprise edition of HttpDNS can use the encryption function. You will receive the authorization ID and key. Please keep them private and avoid disclosure

## 2. Basic Steps

Step 1: Check your email to get the authorization ID and corresponding key;
Step 2: Encrypt the queried domain name (if the client specifies using IP, the IP needs to be encrypted) with the authorization ID and key in Des ECB mode. The padding method is PKCS5Padding.
Step 3: Send the encrypted request;
Step 4: Accept the encrypted response;
Step 5: Decrypt the result and obtain the resolution result corresponding to the queried domain name.

Take Android as an example below:

## 3. Examples for Android
### 3.1 Encrypting the Request

First, encrypt the queried domain name with the authorization ID and key sent to your mailbox in Des ECB mode. The padding method is PKCS5Padding. If you need to specify an IP parameter, it needs to be encrypted in the same way too.
```
try {
// Initialize the key
SecretKeySpec keySpec = new SecretKeySpec(encKey.getBytes("utf-8"), "DES");
// Select to use DES algorithm and ECB mode with PKCS5Padding as the padding method
Cipher cipher = Cipher.getInstance("DES/ECB/PKCS5Padding");
// Initialization
cipher.init(Cipher.ENCRYPT_MODE, keySpec);
/ / Get the encrypted string
encryptedString = bytesToHex(cipher.doFinal(hostName.getBytes("utf-8")));
} catch (Exception e) {
e.printStackTrace();
}

```

### 3.2 Sending the Request
After the domain name is encrypted, a request is initiated to the HttpDNS server:
```
// The dn parameter corresponds to the encrypted string, and the id corresponds to your key ID.
dn=ac7875d400dacdf09954edd788887719&ip=30958d601665478905668b8556976250&id=1&ttl=1

```

### 3.3 Accepting the Encrypted Response
After you send the encrypted request to HttpDNS, the client will receive a string of encrypted result:
```
`60a111ecb44008ac1b32d1fdfb42aa8a96bade20444421dcf83362072c84cf2ad8f870dfb0a1e448`
```
### 3.4 Decrypting the Result
```
try {
// Initialize the key
SecretKeySpec keySpec = new SecretKeySpec(encKey.getBytes("utf-8"), "DES");
// Select to use DES algorithm and ECB mode with PKCS5Padding as the padding method
Cipher cipher = Cipher.getInstance("DES/ECB/PKCS5Padding");
// Initialization
cipher.init(Cipher.DECRYPT_MODE, keySpec);
// Get the decrypted string
decryptedString = cipher.doFinal(hexToBytes(s));
} catch (Exception e) {
e.printStackTrace();
}
```
At this point, you have obtained the decrypted domain name resolution result.

## 4. Encryption and Decryption Tests
If you need to test, you can use the following encryption and decryption test function (only available to users who have applied for the enterprise edition):

Encryption:
```
http://119.29.29.29/en?v=www.google.com&k=weijianliao 
```
![Encryption test](http://mccdn.qcloud.com/static/img/0b2c48b03efef60980b937c85d035921/image.png)
Decryption:
```
http://119.29.29.29/de?v=cd52888ecabcac455a14ddbac7f03d97&k=weijianliao
```
![Decryption test](http://mccdn.qcloud.com/static/img/100404ddcd725edd7933d6b7af7b7139/image.png)

### Annex: Examples for iOS
#### MSDKDnsInfoTool.h

```
//
//  MSDKDnsInfoTool.h
//  MSDKDns
//
//  Created by Mike on 3/25/16.
//  Copyright © 2016 Tencent. All rights reserved.
//

#import <Foundation/Foundation.h>

@interface MSDKDnsInfoTool : NSObject

+ (NSString *) encryptUseDES:(NSString *)plainText key:(NSString *)key;
+ (NSString *) decryptUseDES:(NSString *)cipherString key:(NSString*)key;

@end
```

#### MSDKDnsInfoTool.m

```
//
//  MSDKDnsInfoTool.m
//  MSDKDns
//
//  Created by Mike on 3/25/16.
//  Copyright © 2016 Tencent. All rights reserved.
//

#import "MSDKDnsInfoTool.h"
#import <CommonCrypto/CommonDigest.h>
#import <CommonCrypto/CommonCrypto.h>

@implementation MSDKDnsInfoTool

char MSDKDnsByteToHexByte(char byte) {
    if (byte < 10) {
        return byte + '0';
    }
    return byte - 10 + 'a';
}

void MSDKDnsByteToHexChar(char byte, char *hex) {
    hex[0] = MSDKDnsByteToHexByte((byte >> 4) & 0x0F);
    hex[1] = MSDKDnsByteToHexByte(byte & 0x0F);
}

NSString * MSDKDnsDataToHexString(NSData *data) {
    char hex[data.length * 2 + 1];
    const char *bytes = (const char *)data.bytes;
    for (NSUInteger i = 0; i < data.length; ++i) {
        MSDKDnsByteToHexChar(bytes[i], &hex[i * 2]);
    }
    hex[data.length * 2] = 0;
    return [NSString stringWithUTF8String:hex];
}

char MSDKDnsHexByteToChar(char hex) {
    if (hex >= '0' && hex <= '9') {
        return hex - '0';
    }
    if (hex >= 'a' && hex <= 'f') {
        return hex - 'a' + 10;
    }
    if (hex >= 'A' && hex <= 'F') {
        return hex - 'A' + 10;
    }
    return 0;
}

char MSDKDnsHexCharToChar(char high, char low) {
    high = MSDKDnsHexByteToChar(high);
    low = MSDKDnsHexByteToChar(low);
    return (high << 4) | low;
}

+ (NSString *) encryptUseDES:(NSString *)plainText key:(NSString *)key {
    NSData *srcData = [plainText dataUsingEncoding:NSUTF8StringEncoding];
    size_t dataOutAvilable = ([srcData length] + kCCBlockSizeDES) & ~(kCCBlockSizeDES - 1);
    unsigned char dataOut[dataOutAvilable];
    memset(dataOut, 0x0, dataOutAvilable);
    size_t dataOutMoved = 0;

    char encryptKey[kCCKeySizeDES] = {0};
    strncpy(encryptKey, [key UTF8String], kCCKeySizeDES);

    CCCryptorStatus ccStatus = CCCrypt(kCCEncrypt,
                                       kCCAlgorithmDES,
                                       kCCOptionPKCS7Padding | kCCOptionECBMode,
                                       encryptKey,
                                       kCCKeySizeDES,
                                       NULL,
                                       srcData.bytes,
                                       srcData.length,
                                       dataOut,
                                       dataOutAvilable,
                                       &dataOutMoved);
    if (ccStatus == kCCSuccess) {
        NSData * resultData = [NSData dataWithBytes:dataOut length:(NSUInteger)dataOutMoved];
        return MSDKDnsDataToHexString(resultData);
    }
    return nil;
}

+ (NSString *) decryptUseDES:(NSString *)cipherString key:(NSString *)key {
    if (cipherString && key) {
        const char *tempBytes = [cipherString UTF8String];
        NSUInteger tempLength = [cipherString length];
        if (tempLength > 0) {
            NSUInteger dataLength = tempLength / 2;
            char textBytes[dataLength];
            for (int i  = 0; i < tempLength - 1; i = i + 2)
            {
                char high = tempBytes[i];
                char low = tempBytes[i + 1];
                char hex = MSDKDnsHexCharToChar(high, low);
                textBytes[i / 2] = hex;
            }

            size_t dataOutAvilable = (dataLength + kCCBlockSizeDES) & ~(kCCBlockSizeDES - 1);
            unsigned char dataOut[dataOutAvilable];
            memset(dataOut, 0x0, dataOutAvilable);
            size_t dataOutMoved = 0;

            char decryptKey[kCCKeySizeDES] = {0};
            strncpy(decryptKey, [key UTF8String], kCCKeySizeDES);
            CCCryptorStatus ccStatus = CCCrypt(kCCDecrypt,
                                               kCCAlgorithmDES,
                                               kCCOptionPKCS7Padding | kCCOptionECBMode,
                                               decryptKey,
                                               kCCKeySizeDES,
                                               NULL,
                                               textBytes,
                                               dataLength,
                                               dataOut,
                                               dataOutAvilable,
                                               &dataOutMoved);

            NSString *plainText = nil;
            if (ccStatus == kCCSuccess) {
                NSData *data = [NSData dataWithBytes:dataOut length:(NSUInteger)dataOutMoved];
                if (data) {
                    plainText = [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
                }
            }
            return plainText;
        }
    }
    return nil;
}

@end

```
