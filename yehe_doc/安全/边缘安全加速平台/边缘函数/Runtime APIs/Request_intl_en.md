The **Request** API represents an HTTP request. It is designed based on the standard Web API [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request).

>? In Edge Functions, you can obtain a `Request` object by using the following methods:
>- Create a Request object for the Fetch API by using the `Request` constructor.
>- Use the FetchEvent object [event.request](https://www.tencentcloud.com/document/product/1145/52690) to obtain a Request object.

## Constructor API
```typescript
const request = new Request(input: string | Request, init?: RequestInit)
```

### Parameters

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
      <td>input</td>
      <td>
        string | <br/>
        <a href="https://www.tencentcloud.com/document/product/1145/52690">Request</a>
      </td>
      <td>Yes</td>
      <td>A URL string or a Request object.</td>
    </tr>
    <tr>
      <td>options</td>
      <td><a href="#RequestInit">RequestInit</a></td>
      <td>No</td>
      <td>The initial configuration items of the Request object.</td>
    </tr>
  </tbody>
</table>


#### RequestInit[](id:RequestInit)

The following table describes the initial configuration items of the Request object.

<table>
  <thead>
    <tr>
      <th width="15%">Parameter</th>
      <th width="20%">Type</th>
      <th width="10%">Required</th>
      <th width="10%">Default Value</th>
      <th width="45%">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>method</td>
      <td>string</td>
      <td>No</td>
      <td>GET</td>
      <td>The request method. Examples: <code>GET</code> and <code>POST</code>.</td>
    </tr>
    <tr>
      <td>headers</td>
      <td><a href="https://www.tencentcloud.com/document/product/1145/52689">Headers</a></td>
      <td>No</td>
      <td>-</td>
      <td>The headers that you want to add to the request.</td>
    </tr>
    <tr>
      <td>body</td>
      <td>
        string |<br>
        <a href="https://developer.mozilla.org/en-US/docs/Web/API/Blob">Blob</a> | <br>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer">ArrayBuffer</a> | <br>
        ArrayBufferView | <br>
        <a href="https://www.tencentcloud.com/document/product/1145/52695">ReadableStream</a>
      </td>
      <td>No</td>
      <td>-</td>
      <td>The request body.</td>
    </tr>
    <tr>
      <td>redirect</td>
      <td>string</td>
      <td>No</td>
      <td>follow</td>
      <td>The redirect mode. Valid values: <code>manual</code>, <code>error</code>, and <code>follow</code>.</td>
    </tr>
    <tr>
      <td>maxFollow</td>
      <td>number</td>
      <td>No</td>
      <td>12</td>
      <td>The maximum number of redirects allowed.</td>
    </tr>
    <tr>
      <td>version</td>
      <td>string</td>
      <td>No</td>
      <td>HTTP/1.1</td>
      <td>The HTTP version. Valid values: <code>HTTP/1.0</code>, <code>HTTP/1.1</code>, and <code>HTTP/2.0</code>.</td>
    </tr>
    <tr>
      <td>copyHeaders</td>
      <td>boolean</td>
      <td>No</td>
      <td>-</td>
      <td>Specifies whether to copy the headers of the Request object. <strong>This parameter is not in the Web API specifications.</strong></td>
    </tr>
    <tr>
      <td>eo</td>
      <td><a href="#RequestInitEoProperties">RequestInitEoProperties</a></td>
      <td>No</td>
      <td>-</td>
      <td>The behavior that Edge Functions adopts in processing the request.<strong>This parameter is not in the Web API specifications.</strong></td>
    </tr>
  </tbody>
</table>

#### RequestInitEoProperties[](id:RequestInitEoProperties)
It specifies the behavior that Edge Functions adopts in processing the request. It is not in the Web API specifications.

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
      <td align="left">resolveOverride</td>
      <td align="left">string</td>
      <td align="left">No</td>
      <td align="left">
        Overrides the original domain name resolution for the <a href="https://www.tencentcloud.com/document/product/1145/52687">fetch</a> request. You can specify a domain name or IP address that meets the following requirements:
        <li>The IP address cannot contain a scheme or port number.</li>
        <li>For an IPv6 address, you do not need to enclose it in a pair of square brackets.</li>
      </td>
    </tr>
  </tbody>
</table>


## Attributes

### body[](id:body)
```typescript
// request.body
readonly body: ReadableStream;
```
The request body. For more information, see [ReadableStream](https://www.tencentcloud.com/document/product/1145/52695).

### bodyUsed
```typescript
// request.bodyUsed
readonly bodyUsed: boolean;
```

Indicates whether the request body is read.

### headers
```typescript
// request.headers
readonly headers: Headers;
```

The request header. For more information, see [Headers](https://www.tencentcloud.com/document/product/1145/52689).

### method
```typescript
// request.method
readonly method: string;
```

The request method. Default value: `GET`.

### redirect
```typescript
// request.redirect
readonly redirect: string;
```

The request redirect mode. Valid values: `follow`, `error`, and `manual`. Default value: `manual`.

### maxFollow
```typescript
// request.maxFollow
readonly maxFollow: number;
```

The maximum number of redirects.

### url
```typescript
// request.url
readonly url: string;
```

The request URL.

### version
```typescript
// request.version
readonly version: string;
```

The HTTP version that is used by the request.

### eo
```typescript
// request.version
readonly eo: IncomingRequestEoProperties;
```
Some other information provided by Edge Functions on the current request. For more information, see [IncomingRequestEoProperties](#IncomingRequestEoProperties).

#### IncomingRequestEoProperties[](id:IncomingRequestEoProperties)

The client request object [event.request](https://www.tencentcloud.com/document/product/1145/52690) contains an `eo` attribute.

<table>
  <thead>
    <tr>
      <th width="25%">Parameter</th>
      <th width="15%">Type</th>
      <th width="35%">Description</th>
      <th width="25%">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>geo</td>
      <td><a href="#GeoProperties">GeoProperties</a></td>
      <td>The location information of the client request.</td>
      <td>-</td>
    </tr>
  </tbody>
</table>

#### GeoProperties[](id:GeoProperties)
The location information of the client request.
<table>
  <thead>
    <tr>
      <th width="25%">Parameter</th>
      <th width="15%">Type</th>
      <th width="35%">Description</th>
      <th width="25%">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>asn</td>
      <td>number</td>
      <td><a href="https://en.wikipedia.org/wiki/Autonomous_system_(Internet)">ASN</a></td>
      <td>132203</td>
    </tr>
    <tr>
      <td>countryName</td>
      <td>string</td>
      <td>The name of the country.</td>
      <td>Singapore</td>
    </tr>
    <tr>
      <td>countryCodeAlpha2</td>
      <td>string</td>
      <td>The <a href="https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2">ISO-3611 alpha2</a> code of the country.</td>
      <td>SG</td>
    </tr>
    <tr>
      <td>countryCodeAlpha3</td>
      <td>string</td>
      <td>The <a href="https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3">ISO-3611 alpha3</a> code of the country.</td>
      <td>SGP</td>
    </tr>
    <tr>
      <td>countryCodeNumeric</td>
      <td>string</td>
      <td>The <a href="https://en.wikipedia.org/wiki/ISO_3166-1_numeric">ISO-3611 numeric</a> code of the country.</td>
      <td>702</td>
    </tr>
    <tr>
      <td>regionName</td>
      <td>string</td>
      <td>The name of the region.</td>
      <td>-</td>
    </tr>
    <tr>
      <td>regionCode</td>
      <td>string</td>
      <td>The code of the region.</td>
      <td>AA-AA</td>
    </tr>
    <tr>
      <td>cityName</td>
      <td>string</td>
      <td>The name of the city.</td>
      <td>singapore</td>
    </tr>
    <tr>
      <td>latitude</td>
      <td>number</td>
      <td>The latitude.</td>
      <td>1.29027</td>
    </tr>
    <tr>
      <td>longitude</td>
      <td>number</td>
      <td>The longitude.</td>
      <td>103.851959</td>
    </tr>
  </tbody>
</table>

## Methods

>! The method to get the request body. The `HTTP body` contains a maximum of 1M bytes. If the body exceeds the size, an OverSize exception is returned. We recommend that you stream read an oversized [request.body](#body). For more information, see [ReadableStream](https://www.tencentcloud.com/document/product/1145/52695).

### arrayBuffer
```typescript
request.arrayBuffer(): Promise<ArrayBuffer>;
```
The arrayBuffer() method reads the request body and returns it as a promise that resolves with an [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer).

### blob
```typescript
request.blob(): Promise<Blob>;
```
The blob() method reads the request body and returns it as a promise that resolves with a [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob).

### clone
```typescript
request.clone(copyHeaders?: boolean): Request;
```

The clone() method creates a clone of a request object.

#### Parameters

<table>
	<thead>
		<tr>
			<th width="10%">Parameter</th>
			<th width="15%">Type</th>
			<th width="10%">Required</th>
			<th width="65%">Description</th>
	</tr>
	</thead>
	<tbody>
		<tr>
			<td>copyHeaders</td>
			<td>boolean</td>
			<td>No</td>
			<td>
        Specifies whether to copy the request headers of the original object. Default value: <code>false</code>. Valid values:<br/>
        <li>
          <font color="#9ba6b7">true</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            Copy the request headers of the original object.
          </div>
        </li>
        <li>
          <font color="#9ba6b7">false</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            Reference the request headers of the original object.
          </div>
        </li>
      </td>
		</tr>
	</tbody>
</table>

### json
```typescript
request.json(): Promise<object>;
```

The json() method reads the request body and returns a promise that resolves with the parsing result of the body text as `json`.

### text
```typescript
request.text(): Promise<string>;
```

The json() method reads the request body and returns a promise that resolves with a String.

### getCookies
```typescript
request.getCookies(): Cookies;
```

The getCookies() method obtains cookies from `request` headers. The cookies will be automatically parsed into [Cookies](https://www.tencentcloud.com/document/product/1145/52685) objects.

### setCookies
```typescript
request.setCookies(cookies: Cookies): boolean;
```

The setCookies() method sets cookies for `request` headers. 

#### Parameters

<table>
	<thead>
		<tr>
			<th width="10%">Parameter</th>
			<th width="15%">Type</th>
			<th width="10%">Required</th>
			<th width="65%">Description</th>
	</tr>
	</thead>
	<tbody>
		<tr>
			<td>cookies</td>
			<td><a href="https://www.tencentcloud.com/document/product/1145/52685">Cookies</a></td>
			<td>No</td>
			<td>
        A new Cookies object.
      </td>
		</tr>
	</tbody>
</table>

## Sample Code
```typescript
async function handleRequest() {
  const request = new Request('https://www.tencentcloud.com/');
  const response = await fetch(request);
  return response;
}

addEventListener('fetch', (event) => {
  event.respondWith(handleRequest());
});
```

## References
- [MDN documentation: Request](https://developer.mozilla.org/en-US/docs/Web/API/Request)
- [Sample Functions: Using the Cache API](https://www.tencentcloud.com/document/product/1145/52710)
- [Sample Functions: Performing Redirect Based on the Request Location](https://www.tencentcloud.com/document/product/1145/52709)
