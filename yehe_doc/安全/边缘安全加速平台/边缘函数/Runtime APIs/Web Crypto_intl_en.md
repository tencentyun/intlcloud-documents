The **Web Crypto API** is designed based on the standard Web API [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API). The Web Crypto API provides a set of functions for common cryptographic operations. Performing cryptographic operations by using the Web Crypto API is significantly faster than performing them purely in JavaScript.

>! The `Crypto` object cannot be constructed directly. It is globally injected during the runtime of edge functions. Directly use the global crypto instance.

## Overview
```typescript
// Perform encoding.
const encodeContent = new TextEncoder().encode('hello world');
// Use crypto to perform SHA-256 hashing. The resulting hash is a promise that fulfills with an ArrayBuffer.
const sha256Content = await crypto.subtle.digest(
  { name: 'SHA-256' },
  encodeContent 
);
const result = new Uint8Array(sha256Content); 
```

## Attributes
```typescript
// crypto.subtle
readonly subtle: SubtleCrypto;
```
The Web Crypto API supports common cryptographic operations, such as hashing, signature signing and verification, and encryption and decryption. For more information, see [SubtleCrypto](#SubtleCrypto).

### Methods
### getRandomValues
```typescript
crypto.getRandomValues(buffer: TypedArray): TypedArray;
```

The getRandomValues() method generates a random value, fills the buffer with the random value, and returns the buffer.

#### Parameters

<table>
	<thead>
		<tr>
			<th width="10%">Parameter</th>
			<th width="20%">Type</th>
			<th width="10%">Required</th>
			<th width="60%">Description</th>
	</tr>
	</thead>
	<tbody>
		<tr>
			<td>buffer</td>
			<td>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int8Array">Int8Array</a> |<br>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array">Uint8Array</a> |<br>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8ClampedArray">Uint8ClampedArray</a> |<br>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int16Array">Int16Array</a> |<br>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint16Array">Uint16Array</a> |<br>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Int32Array">Int32Array</a> |<br>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint32Array">Uint32Array</a> |<br>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt64Array">BigInt64Array</a> |<br>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigUint64Array">BigUint64Array</a>
      </td>
			<td>Yes</td>
			<td>
        The buffer of random values. The value cannot exceed 65,536 bytes in length. For more information, see <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray">TypedArray</a>.
      </td>
		</tr>
	</tbody>
</table>

### randomUUID
```typescript
crypto.randomUUID(): string;
```

The randomUUID() method generates a new random (version 4) UUID.

## SubtleCrypto[](id:SubtleCrypto)
The SubtleCrypto API supports common cryptographic operations, such as hashing, signature signing and verification, and encryption and decryption. For more information, see [SubtleCrypto](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto#Methods).

>? **SubtleCrypto** methods are classified into the following types based on features:
>- **Encryption methods**: `encrypt/decrypt`, `sign/verify`, and `digest`. Such methods can be used to implement security-related features such as privacy and identity verification.
>- **Key management methods**: `generateKey`, `deriveKey`, and `importKey/exportKey`. Such methods can be used to manage keys.

### digest
```typescript
crypto.subtle.digest(algorithm: string | object, data: ArrayBuffer): Promise<ArrayBuffer>;
```

The decrypt() method returns a Promise object that fulfills with the generated data digest (hash). For more information, see [SubtleCrypto.digest](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/digest).

### encrypt 
```typescript
crypto.subtle.encrypt(algorithm: object, key: CryptoKey, data: ArrayBuffer): Promise<ArrayBuffer>;
```

The encrypt() method returns a Promise object that fulfills with the encrypted data. For more information, see [SubtleCrypto.encrypt](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/encrypt).

### decrypt
```typescript
crypto.subtle.decrypt(algorithm: object, key: CryptoKey, data: ArrayBuffer): Promise<ArrayBuffer>;
```

The decrypt() method returns a Promise object that fulfills with the decrypted data. For more information, see [SubtleCrypto.decrypt](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/decrypt).

### sign
```typescript
crypto.subtle.sign(algorithm: string | object, key: CryptoKey, data: ArrayBuffer): Promise<ArrayBuffer>;
```

The sign() method returns a Promise object that fulfills with the signature. For more information, see [SubtleCrypto.sign](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/sign).

### verify
```typescript
crypto.subtle.verify(algorithm: string | object, key: CryptoKey, signature: BufferSource, data: ArrayBuffer): Promise<boolean>;
```

The verify() method returns a Promise object that fulfills with the signature verification result. For more information, see [SubtleCrypto.verify](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/verify).

### generateKey[](id:generateKey)
```typescript
crypto.subtle.generateKey(algorithm: object, extractable: boolean, keyUsages: Array<string>): Promise<CryptoKey | CryptoKeyPair>;
```

The generateKey() method returns a Promise object that fulfills with a [CryptoKey](id:CryptoKey) or a [CryptoKeyPair](id:CryptoKeyPair). For more information, see [SubtleCrypto.generateKey](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/generateKey).

### deriveKey[](id:deriveKey)
```typescript
crypto.subtle.deriveKey(algorithm: object, baseKey: CryptoKey, derivedKeyAlgorithm: object, extractable: boolean, keyUsages: Array<string>): Promise<CryptoKey>;
```

The deriveKey() method returns a Promise object that fulfills with a [CryptoKey](id:CryptoKey). For more information, see [SubtleCrypto.deriveKey](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/deriveKey).

### importKey[](id:importKey)
```typescript
crypto.subtle.importKey(format: string, keyData: BufferSource, algorithm: string | object, extractable: boolean, keyUsages: Array<string>): Promise<CryptoKey>;
```

The importKey() method returns a Promise object that fulfills with a [CryptoKey](id:CryptoKey). For more information, see [SubtleCrypto.importKey](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/importKey).

### exportKey
```typescript
crypto.subtle.exportKey(format: string, key: CryptoKey): Promise<ArrayBuffer>;
```

The exportKey() method returns a Promise object that fulfills with an ArrayBuffer containing the key. For more information, see [SubtleCrypto.exportKey](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/exportKey).

### deriveBits
```typescript
crypto.subtle.deriveBits(algorithm: object, baseKey: CryptoKey, length: integer): Promise<ArrayBuffer>;
```

The deriveBits() method returns a Promise object that fulfills with an ArrayBuffer of pseudo-random bits. For more information, see [SubtleCrypto.deriveBits](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/deriveBits).

### wrapKey 
```typescript
crypto.subtle.wrapKey(format: string, key: CryptoKey, wrappingKey: CryptoKey, wrapAlgo: string | object): Promise<ArrayBuffer>;;
```

The wrapKey() method returns a Promise object that fulfills with an ArrayBuffer containing the wrapped key. For more information, see [SubtleCrypto.wrapKey](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/wrapKey).

### unwrapKey[](id:unwrapKey)
```typescript
crypto.subtle.unwrapKey(format: string, wrappedKey: ArrayBuffer, unwrappingKey: CryptoKey, unwrapAlgo: string | object, unwrappedKeyAlgo: string | object, extractable: boolean, keyUsages: Array<string>): Promise<CryptoKey>;
```

The unwrapKey() method returns a Promise object that fulfills with the unwrapped [CryptoKey](id:CryptoKey). For more information, see [SubtleCrypto.unwrapKey](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/unwrapKey).

## CryptoKey[](id:CryptoKey)
A `CryptoKey` represents a key that is generated by using an encryption algorithm. For more information, see [CryptoKey](https://developer.mozilla.org/en-US/docs/Web/API/CryptoKey). The CryptoKey object cannot be constructed directly. You can use the following methods to generate CryptoKey objects:

- [crypto.subtle.generateKey](#generateKey)
- [crypto.subtle.importKey](#importKey)
- [crypto.subtle.deriveKey](#deriveKey)
- [crypto.subtle.unwrapKey](#unwrapKey)

The following table describes the `CryptoKey` attributes.

<table>
	<thead>
		<tr>
			<th width="10%">Attribute</th>
			<th width="15%">Type</th>
			<th width="10%">Read-only</th>
			<th width="65%">Description</th>
	</tr>
	</thead>
	<tbody>
		<tr>
			<td>type</td>
			<td>string</td>
			<td>Yes</td>
			<td>The type of the key.</td>
		</tr>
    <tr>
			<td>extractable</td>
			<td>boolean</td>
			<td>Yes</td>
			<td>Specifies whether the key can be exported.</td>
		</tr>
    <tr>
			<td>algorithm</td>
			<td>object</td>
			<td>Yes</td>
			<td>The algorithm for which this key can be used and the associated parameters.</td>
		</tr>
    <tr>
			<td>usages</td>
			<td>Array&lt;string&gt;</td>
			<td>Yes</td>
			<td>The usage of the key.</td>
		</tr>
	</tbody>
</table>

## CryptoKeyPair[](id:CryptoKeyPair)
A `CryptoKeyPair` represents a key pair that is generated by using an encryption algorithm. For more information, see [CryptoKeyPair](https://developer.mozilla.org/en-US/docs/Web/API/CryptoKeyPair). The CryptoKeyPair object cannot be constructed directly. You can use the following method to generate CryptoKeyPair objects:

- [crypto.subtle.generateKey](#generateKey)

The following table describes the `CryptoKeyPair` attributes.


<table>
	<thead>
		<tr>
			<th width="10%">Attribute</th>
			<th width="15%">Type</th>
			<th width="10%">Read-only</th>
			<th width="65%">Description</th>
	</tr>
	</thead>
	<tbody>
		<tr>
			<td>privateKey</td>
			<td><a href="#CryptoKey">CryptoKey</a></td>
			<td>Yes</td>
			<td>The private key. For encryption and decryption algorithms, this key is used for decryption. For signature signing and verification algorithms, this key is used for signature signing.</td>
		</tr>
    <tr>
			<td>publicKey</td>
			<td><a href="#CryptoKey">CryptoKey</a></td>
			<td>Yes</td>
			<td>The public key. For encryption and decryption algorithms, this key is used for encryption. For signature signing and verification algorithms, this key is used for signature verification.</td>
		</tr>
	</tbody>
</table>

## Supported Algorithms
Edge Functions supports all algorithms that are defined in the [WebCrypto](https://www.w3.org/TR/WebCryptoAPI/) specification. The following table describes the algorithms.
<table>
<thead>
<tr>
<th width="12%">Algorithm</th>
<th width="11%">encrypt() decrypt()</th>
<th width="11%">sign() verify()</th>
<th width="11%">wrapKey() unwrapKey()</th>
<th width="11%">deriveKey() deriveBits()</th>
<th width="11%">generateKey()</th>
<th width="11%">importKey()</th>
<th width="11%">exportKey()</th>
<th width="11%">digest()</th>
</tr>
</thead>
<tbody><tr>
<td>RSASSA-PKCS1-v1_5</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
<td style="color:#aaa">-</td>
</tr>
<tr>
<td>RSA-PSS</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
<td style="color:#aaa">-</td>
</tr>
<tr>
<td>RSA-OAEP</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
<td style="color:#aaa">-</td>
</tr>
<tr>
<td>ECDSA</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
<td style="color:#aaa">-</td>
</tr>
<tr>
<td>ECDH</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
<td style="color:#aaa">-</td>
</tr>
<tr>
<td>HMAC</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
<td style="color:#aaa">-</td>
</tr>
<tr>
<td>AES-CTR</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
<td style="color:#aaa">-</td>
</tr>
<tr>
<td>AES-CBC</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
<td style="color:#aaa">-</td>
</tr>
<tr>
<td>AES-GCM</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
<td style="color:#aaa">-</td>
</tr>
<tr>
<td>AES-KW</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
<td style="color:#aaa">-</td>
</tr>
<tr>
<td>HKDF</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
</tr>
<tr>
<td>PBKDF2</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td>✓</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
</tr>
<tr>
<td>SHA-1</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td>✓</td>
</tr>
<tr>
<td>SHA-256</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td>✓</td>
</tr>
<tr>
<td>SHA-384</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td>✓</td>
</tr>
<tr>
<td>SHA-512</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td>✓</td>
</tr>
<tr>
<td>MD5</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td style="color:#aaa">-</td>
<td>✓</td>
</tr>
</tbody></table>

## Sample Code
```typescript
function uint8ArrayToHex(arr) {
	return Array.prototype.map.call(arr, (x) => ((`0${x.toString(16)}`).slice(-2))).join('');
}

async function handleEvent(event) {
	const encodeArr = TextEncoder().encode('hello world');
	// Execute MD5.
	const md5Buffer = await crypto.subtle.digest({ name: 'MD5' }, encodeArr);
	// Generate a hexadecimal string.
	const md5Str = uint8ArrayToHex(new Uint8Array(md5Buffer));
	
	const response = new Response(md5Str);
	return response;
}
  
addEventListener('fetch', async (event) => {    
  event.respondWith(handleEvent(event));
});
```

## References 
- [MDN documentation: Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API)
- [MDN documentation: SubtleCrypto](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto#Methods)
- [MDN documentation: CryptoKey](https://developer.mozilla.org/en-US/docs/Web/API/CryptoKey)
- [MDN documentation: CryptoKeyPair](https://developer.mozilla.org/en-US/docs/Web/API/CryptoKeyPair)
- [Sample Functions: Protecting Data from Tampering](https://www.tencentcloud.com/document/product/1145/52714)
- [Sample Functions: Rewriting a m3u8 File and Configuring Authentication](https://www.tencentcloud.com/document/product/1145/52715)
- [Sample Functions: Caching POST Requests](https://www.tencentcloud.com/document/product/1145/52711)