
## Overview

KMS provides the following SM2 and RSA asymmetric key-based decryption APIs:

| API Name | Description | Remarks |
|---------|---------|---------|
| AsymmetricSm2Decrypt | SM2 decryption | For more information, please see [AsymmetricSm2Decrypt](https://intl.cloud.tencent.com/document/product/1030/35180) |
| AsymmetricRsaDecrypt |	RSA decryption | 	For more information, please see [AsymmetricRsaDecrypt](https://intl.cloud.tencent.com/document/product/1030/35181) |


The samples below are called with [TCCLI](https://intl.cloud.tencent.com/product/cli), and you can also use any supported programming languages.

## Asymmetric Decryption


### RSA decryption

#### Input
```shell
tccli kms AsymmetricRsaDecrypt --KeyId 22d79428-61d9-11ea-a3c8-525400****** --Algorithm RSAES_OAEP_SHA_256 --Ciphertext "DEb/JBmuhVkYS34r0pR7Gv1WTc4khkxqf7S1WIr7/GXsAs/tfP/v/2+1SwsIG7BqW7kUZqr38/FGkaIEqYeewot37t3+Jx0t5w7/yXkUnyUfyfPpXlHXf94g3wFOjijEWWsjWWzaXTkTr8uWOfRBenq+bcaY783FIy03XjJW/Y0wKWjD3tULvKndCJO/3bkb65kn1Fbsfm20xrUUwqV/p2DVLXBdG1ymr0DjsbG7R0tb3ytc2LmH33YPAQE32eP27ciKzSml+w2tdUM3dw3nEZcTGMs1wFDGk0O1WB052jZ7TitUD9zCftFv2dKlZD3LRx1+vHqpNVgPhLmL******=="
```

#### Output
```shell
{
    "Response": {
        "RequestId": "6758cbf5-5e21-4c37-a2cf-8d47f5******",
        "KeyId": "22d79428-61d9-11ea-a3c8-525400******",
        "Plaintext": "dGVzdAo="
    }
}
```

### SM2 decryption

#### Input
```shell
tccli kms AsymmetricSm2Decrypt --KeyId 22d79428-61d9-11ea-a3c8-525400****** --Ciphertext "DEb/JBmuhVkYS34r0pR7Gv1WTc4khkxqf7S1WIr7/GXsAs/tfP/v/2+1SwsIG7BqW7kUZqr38/FGkaIEqYeewot37t3+Jx0t5w7/yXkUnyUfyfPpXlHXf94g3wFOjijEWWsjWWzaXTkTr8uWOfRBenq+bcaY783FIy03XjJW/Y0wKWjD3tULvKndCJO/3bkb65kn1Fbsfm20xrUUwqV/p2DVLXBdG1ymr0DjsbG7R0tb3ytc2LmH33YPAQE32eP27ciKzSml+w2tdUM3dw3nEZcTGMs1wFDGk0O1WB052jZ7TitUD9zCftFv2dKlZD3LRx1+vHqpNVgPhLmL******=="
```

#### Output
```shell
{
    "Response": {
        "RequestId": "6758cbf5-5e21-4c37-a2cf-8d47f5******",
        "KeyId": "22d79428-61d9-11ea-a3c8-525400******",
        "Plaintext": "dGVzdAo="
    }
}
```

## Viewing Public Key
#### Overview

This API is used to get the information of the public key with the specified `KeyId`. For the API documentation, please see [GetPublicKey](https://intl.cloud.tencent.com/document/product/1030/35179).

The sample below is called with [TCCLI](https://intl.cloud.tencent.com/product/cli), and you can also use any supported programming languages.

#### Sample

#### Input
```shell
tccli kms GetPublicKey  --KeyId 22d79428-61d9-11ea-a3c8-525400******
```


#### Output
```shell
{
    "Response": {
        "RequestId": "408fa858-cd6d-4011-b8a0-653805******",
        "KeyId": "22d79428-61d9-11ea-a3c8-525400******",
        "PublicKey": "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzQk7x7ladgVFEEGYDbeUc5aO9TfiDplIO4WovBOVpIFoDS31n46YiCGiqj67qmYslZ2KMGCd3Nt+a+jdzwFiTx3O87wdKWcF2vHL9Ja+95VuCmKYeK1uhPyqqj4t9Ch/cyvxb0xaLBzztTQ9dXCxDhwj08b24T+/FYB9a4icuqQypCvjY1X9j8ivAsPEdHZoc9Di7JXBTZdVeZC1igCVgl6mwzdHTJCRydE2976zyjC7l6QsRT6pRsMF3696N07WnaKgGv3K/Zr/6RbxebLqtmNypNERIR7jTCt9L+fgYOX7anmuF5v7z0GfFsen9Tqb1LsZuQR0vgqCauOjL2CL1Q******",
        "PublicKeyPem": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzQk7x7ladgVFEEGYDbeU\nc5aO9TfiDplIO4WovBOVpIFoDS31n46YiCGiqj67qmYslZ2KMGCd3Nt+a+jdzwFi\nTx3O87wdKWcF2vHL9Ja+95VuCmKYeK1uhPyqqj4t9Ch/cyvxb0xaLBzztTQ9dXCx\nDhwj08b24T+/FYB9a4icuqQypCvjY1X9j8ivAsPEdHZoc9Di7JXBTZdVeZC1igCV\ngl6mwzdHTJCRydE2976zyjC7l6QsRT6pRsMF3696N07WnaKgGv3K/Zr/6RbxebLq\ntmNypNERIR7jTCt9L+fgYOX7anmuF5v7z0GfFsen9Tqb1LsZuQR0vgqCau******\n1QIDAQAB\n-----END PUBLIC KEY-----\n"
    }
}
```

