The encoder and decoder are designed based on standard Web APIs [TextEncoder](https://developer.mozilla.org/en-US/docs/Web/API/TextEncoder/TextEncoder) and [TextDecoder](https://developer.mozilla.org/en-US/docs/Web/API/TextDecoder/TextDecoder).

## TextEncoder
The TextEncoder API takes code point streams as inputs and generates `UTF-8` byte streams as outputs. For more information, see [TextEncoder](https://developer.mozilla.org/en-US/docs/Web/API/TextEncoder/TextEncoder). 

### Constructor API

```typescript
// The TextEncoder() constructor does not have any parameters.
const encoder = new TextEncoder();
```

### Attributes
```typescript
// encoder.encoding
readonly encoding: string;
```

The name of the encoding algorithm that is used by the encoder. The value is fixed to `UTF-8`.

### Methods
#### encode 
```typescript
encoder.encode(input?: string | undefined): Uint8Array
```
The encoder.encode() method takes code point streams as inputs and generates `UTF-8` byte streams as outputs.

>! The maximum length of **input** is 300 MB. An exception will be thrown if the maximum length is exceeded.

- `encoder.encode` parameters

<table>
  <thead>
    <tr>
      <th width="15%">Parameter</th>
      <th width="15%">Type</th>
      <th width="10%">Required</th>
      <th width="60%">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>input</td>
      <td>string | undefined</td>
      <td>No</td>
      <td>The text to be encoded.</li>
      </td>
    </tr>
  </tbody>
</table>

#### encodeInto 
```typescript
encoder.encodeInto(input: string, destination: Uint8Array): EncodeIntoResult;
```
The encoder.encodeInto() method takes code point streams as inputs, generates `UTF-8` byte streams as outputs, and writes the outputs to a `destination` byte array.

- Parameters

<table>
  <thead>
    <tr>
      <th width="15%">Parameter</th>
      <th width="15%">Type</th>
      <th width="10%">Required</th>
      <th width="60%">Description</th> 
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>input</td>
      <td>string</td>
      <td>Yes</td>
      <td>The text to be encoded.</td>
    </tr>
    <tr>
      <td>destination</td>
      <td><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array">Uint8Array</a></td>
      <td>Yes</td>
      <td>The object in which the encoded text is stored.</td>
    </tr>
  </tbody>
</table>


- Return value: `EncodeIntoResult`

<table>
  <thead>
    <tr>
      <th width="15%">Parameter</th>
      <th width="15%">Type</th>
      <th width="70%">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>read</td>
      <td>number</td>
      <td>The number of UTF-16 units that have been converted to UTF-8.</td>
    </tr>
    <tr>
      <td>written</td>
      <td>number</td>
      <td>The number of bytes that are modified in the destination <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array">Uint8Array</a>.</td>
    </tr>
  </tbody>
</table>

## TextDecoder
The TextDecoder API takes byte streams as inputs and generates code point streams as outputs. For more information, see [TextDecoder](https://developer.mozilla.org/en-US/docs/Web/API/TextDecoder/TextDecoder).

### Construction API

```typescript
const decoder = new TextDecoder(label?: string | undefined, options?: DecoderOptions | undefined): TextEncoder;
```

### Parameters

>! The [label](https://developer.mozilla.org/en-US/docs/Web/API/Encoding_API/Encodings) parameter does not support the following values:
>- iso-8859-16
>- hz-gb-2312
>- csiso2022kr, iso-2022-kr

<table>
  <thead>
    <tr>
      <th width="15%">Parameter</th>
      <th width="15%">Type</th>
      <th width="10%">Required</th>
      <th width="60%">Description</th> 
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>label</td>
      <td>string | <br/> undefined</td>
      <td>No</td>
      <td>
        The name of the decoding algorithm that is used by the decoder. Default value: <code>UTF-8</code>. For the valid values of <code>label</code>, see <a href="https://developer.mozilla.org/en-US/docs/Web/API/Encoding_API/Encodings">Encoding API Encodings</a>.
      </td>
    </tr>
    <tr>
      <td>options</td>
      <td><a href="#MatchOptions">DecoderOptions</a> | <br/> undefined</td>
      <td>No</td>
      <td>The configuration items of the decoder.</td>
    </tr>
  </tbody>
</table>

#### DecoderOptions[](id:MatchOptions)
The following table describes the configuration items of the decoder.

<table>
	<thead>
		<tr>
			<th width="10%">Parameter</th>
			<th width="15%">Type</th>
			<th width="10%">Default value</th>
			<th width="65%">Description</th>
	</tr>
	</thead>
	<tbody>
		<tr>
			<td>fatal</td>
			<td>boolean</td>
			<td>false</td>
			<td>Specifies whether to throw an exception when decoding fails.</td>
		</tr>
    <tr>
			<td>ignoreBOM</td>
			<td>boolean</td>
			<td>false</td>
			<td>Specifies whether to ignore <a href="https://www.w3.org/International/questions/qa-byte-order-mark">byte-order marker</a></td>.
		</tr>
	</tbody>
</table>

### Attributes
#### encoding
```typescript
// decoder.encoding
readonly encoding: string;
```
The name of the decoding algorithm that is used by the decoder.

#### fatal
```typescript
// decoder.fatal
readonly fatal: boolean;
```

Specifies whether to throw an exception when decoding fails.

#### ignoreBOM
```typescript
// decoder.ignoreBOM
readonly ignoreBOM: boolean;
```
Specifies whether to ignore [byte-order marker](https://www.w3.org/International/questions/qa-byte-order-mark).

### Methods
#### decode

```typescript
const result = decoder.decode(buffer?: ArrayBuffer | ArrayBufferView | undefined, options?: DecodeOptions | undefined): string;
```
>! The maximum length of **buffer** is 100 MB. An exception will be thrown if the maximum length is exceeded.
<table>
  <thead>
    <tr>
      <th width="15%">Parameter</th>
      <th width="15%">Type</th>
      <th width="10%">Required</th>
      <th width="60%">Description</th> 
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>buffer</td>
      <td>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer">ArrayBuffer</a> | <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer">ArrayBufferView</a> | undefined
      </td>
      <td>No</td>
      <td>
        The byte stream to be decoded.<br>
        <li>The maximum length of <code>buffer</code> is 100 MB. An exception will be thrown if the maximum length is exceeded.</li>
      </td>
    </tr>
    <tr>
      <td>options</td>
      <td>
        <a href="#DecodeOptions">DecodeOptions</a>
      </td>
      <td>No</td>
      <td>The configuration items for decoding.</td>
    </tr>
  </tbody>
</table>

#### DecodeOptions[](id:DecodeOptions)
The following table describes the configuration items for decoding.

<table>
	<thead>
		<tr>
			<th width="10%">Parameter</th>
			<th width="15%">Type</th>
			<th width="10%">Default value</th>
			<th width="65%">Description</th>
	  </tr>
	</thead>
	<tbody>
		<tr>
			<td>stream</td>
			<td>boolean</td>
			<td>false</td>
			<td>
        Specifies whether to perform decoding in streaming mode. Default value: false. Valid values:<br/>
        <li>
          <font color="#9ba6b7">true</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            Perform decoding in streaming mode. Use this value if data is processed in <code>chunks</code> and additional chunks are expected.
          </div>
        </li>
        <li>
          <font color="#9ba6b7">false</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            Do not perform decoding in streaming mode. Use this value if the current <code>chunk</code> is the last one or data is not <code>chunked</code>.
          </div>
        </li>
      </td>
		</tr>
	</tbody>
</table>

## Sample Code
```typescript
function handleEvent(event) {
  // Encoder
  const encoder = new TextEncoder();
  const encodeText = encoder.encode('hello world');
  
  // Decoder
  const decoder = new TextDecoder();
  const decodeText = decoder.decode(encodeText);

  // Response
  const response = new Response(JSON.stringify({
    encodeText: encodeText.toString(),
    decodeText,
  }));

  return response;
}

addEventListener('fetch', (event) => {
  event.respondWith(handleEvent(event));
});
```

## References 
- [MDN documentation: TextEncoder](https://developer.mozilla.org/en-US/docs/Web/API/TextEncoder)
- [MDN documentation:TextDecoder](https://developer.mozilla.org/en-US/docs/Web/API/TextDecoder)
- [MDN documentation: Encoding API Encodings](https://developer.mozilla.org/en-US/docs/Web/API/Encoding_API/Encodings)
- [Sample Functions: Protecting Data from Tampering](https://www.tencentcloud.com/document/product/1145/52714)
