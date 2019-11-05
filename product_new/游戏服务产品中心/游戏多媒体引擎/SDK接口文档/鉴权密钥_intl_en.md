This document describes the authentication keys for all platforms to make it easy for developers to debug and integrate GME.


## Backend Deployment of Voice Key
GME provides authentication keys for voice chat and offline voice. This document describes the backend deployment scheme.
The generation process of the signature used for authentication involves **plaintext**, **secret key** and **algorithm**.

### Plaintext
Plaintext is constructed using the following fields in the network order:

| Field Description 		| Type/Length 			| Value Definition/Remark |
| ---------------- |-------------------|--------------|
| cVer 				| unsigned char/1 	| Version number. Enter 1		 |
| wOpenIDLen		|unsigned short/2	| User account length	|
| strOpenID			|wOpenIDLen		| User account characters	|
| dwSdkAppid		|unsigned short/4	| Developer SDKappid		|
| dwReserved1		|unsigned int/4		| Enter 0				|
| dwExpTime 		| unsigned int/4 		| Expiration time (current time + validity period, in seconds). 300 seconds is recommended |
| dwReserved2		|unsigned int/4		| Enter -1 or 0xFFFFFFFF |
| dwReserved3		|unsigned int/4		| Enter 0				|
| wRoomIDLen		|unsigned short/2	| Length of the ID of the room the user wants to enter. Enter 0 for offline voice 				|
| strRoomID			|wRoomIDLen		| Characters of the ID of the room the user wants to enter 				|

### Key
The permission key can be obtained in the GME Console.
![](https://main.qcloudimg.com/raw/389a4b02fe80df1d2c8b4ef164a25fb5.png)

### Algorithm
TEA symmetric encryption algorithm is used.
It is recommended to deploy the authentication feature on the client at the early stage and deploy it on the backend of the game app later.

| Scheme 		| Advantages 		| Disadvantages 																																|
| ------------- |-------------|-------------| 
| Backend deployment 		| High security	| Joint testing by backend developers is required |
| Client deployment 	| Quick integration	| Low security |

#### How to Implement Backend Deployment
The encrypted string generated on the backend is sent to the client and used for the following scenario: When the EnterRoom API is called for entering a room, the encrypted string will be transferred to the `authBuffer` field in the parameters for room entering.




### Algorithm Encryption Details
- Key: MD5 value of the authentication key corresponding to the APPID, with a length of 16 bytes.
- Encryption algorithm: TEA
- Encryption library and samples: See [authbuffer.zip](https://main.qcloudimg.com/raw/c8be793e20c85114499f52e0f8c29190.zip)

>The modified key takes effect within 15 minutes to 1 hour. Frequent modification is not recommended.



#### Encryption Method	
- Convert numbers in ciphertext to network byte order (Big Endian);
- Construct the ciphertext into a string;
- Encrypt the string using TEA. The string output by the symmetry_encrypt function is the encrypted permission string;

>Do not convert the binary string into a hexadecimal one.


