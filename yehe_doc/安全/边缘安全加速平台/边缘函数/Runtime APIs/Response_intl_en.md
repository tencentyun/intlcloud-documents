The **Response** API represents the response to an HTTP request. It is designed based on the standard Web API [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response).

>? In Edge Functions, you can obtain a `Response` object by using the following methods:
>- Create a Response object by using the `Response` constructor API to respond to [event.respondWith](https://www.tencentcloud.com/document/product/1145/52688#respondwith).
>- Use <a href="https://www.tencentcloud.com/document/product/1145/52687">fetch</a> to obtain a Response object.

## Constructor API
```typescript
const response = new Response(body?: string | ArrayBuffer | Blob | ReadableStream | null | undefined, init?: ResponseInit);
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
      <td>body</td>
      <td>
        string | <br/>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer">ArrayBuffer</a> | <br/>
        <a href="https://developer.mozilla.org/en-US/docs/Web/API/Blob">Blob</a> | <br/>
        <a href="https://www.tencentcloud.com/document/product/1145/52695">ReadableStream</a> | <br/>
        null | <br/>
        undefined
      </td>
      <td>Yes</td>
      <td>The body content of the <code>Response</code> object.</td>
    </tr>
    <tr>
      <td>init</td>
      <td><a href="#ResponseInit">ResponseInit</a></td>
      <td>No</td>
      <td>The initial configuration items of the <code>Response</code> object.</td>
    </tr>
  </tbody>
</table>

#### ResponseInit[](id:ResponseInit)

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
      <td align="left">status</td>
      <td align="left">number</td>
      <td align="left">No</td>
      <td align="left">The status code for the response.</td>
    </tr>
    <tr>
      <td align="left">statusText</td>
      <td align="left">string</td>
      <td align="left">No</td>
      <td align="left">The status message for the response. The maximum length is 4,095 bytes. If the length exceeds the upper limit, the extra content will be truncated.</td>
    </tr>
    <tr>
      <td align="left">headers</td>
      <td align="left"><a href="https://www.tencentcloud.com/document/product/1145/52689">Headers</a></td>
      <td align="left">No</td>
      <td align="left">The headers associated with the response.</td>
    </tr>
  </tbody>
</table>

## Attributes
### body[](id:body)
```typescript
// response.body
readonly body: ReadableStream;
```
The response body. For more information, see [ReadableStream](https://www.tencentcloud.com/document/product/1145/52695).

### bodyUsed
```typescript
// response.bodyUsed
readonly bodyUsed: boolean;
```

Indicates whether the response body is read.

### headers
```typescript
// response.headers
readonly headers: Headers;
```

The response headers. For more information, see [Headers](https://www.tencentcloud.com/document/product/1145/52689).

### ok
```typescript
// response.ok
readonly ok: boolean;
```

Indicates whether the response was successful. If the status code ranges from 200 to 299, the response was successful.

### status
```typescript
// response.status
readonly status: number;
```
The status code for the response.

### statusText
```typescript
// response.statusText
readonly statusText: string;
```

The status message for the response.

### url
```typescript
// response.url
readonly url: string;
```
The URL of the response.

### redirected
```typescript
// response.redirected
readonly redirected: boolean;
```

Indicates whether the response is the result of a redirect.

### redirectUrls
```typescript
// response.redirectUrls
readonly redirectUrls: Array<String>
```

All URLs for redirection.

## Methods

>! If the size of the `HTTP body` obtained by using a method exceeds 1 MB, the OverSize exception will be thrown. In this case, we recommend that you use [response.body](#body) to read the response body in streaming mode. For more information, see [ReadableStream](https://www.tencentcloud.com/document/product/1145/52695).


### arrayBuffer
```typescript
request.arrayBuffer(): Promise<ArrayBuffer>;
```
The arrayBuffer() method takes a Response stream, reads it to completion, and returns a promise that resolves with an [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer).

### blob
```typescript
request.blob(): Promise<Blob>;
```
The blob() method takes a Response stream, reads it to completion, and returns a promise that resolves with a [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob).

### clone
```typescript
request.clone(copyHeaders?: boolean): Request;
```

The clone() method creates a clone of a response object.

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
        Specifies whether to copy the response headers of the original object. Default value: <code>false</code>. Valid values:<br/>
        <li>
          <font color="#9ba6b7">true</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            Copy the response headers of the original object.
          </div>
        </li>
        <li>
          <font color="#9ba6b7">false</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            Reference the response headers of the original object.
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

The json() method takes a Response stream, reads it to completion, and returns a promise which resolves with the parsing result of the body text as `json`.

### text
```typescript
request.text(): Promise<string>;
```

The text() method takes a Response stream, reads it to completion, and returns a promise that resolves with a String.

### getCookies
```typescript
request.getCookies(): Cookies;
```

The getCookies() method obtains cookies from `response` headers. The cookies will be automatically parsed into [Cookies](https://www.tencentcloud.com/document/product/1145/52685) objects.

### setCookies
```typescript
request.setCookies(cookies: Cookies): boolean;
```

The setCookies() method sets cookies for `response` headers. 

## Sample Code
```typescript
addEventListener('fetch', (event) => {
  const response =  new Response('hello world');
  event.respondWith(response);
});
```

## References 
- [MDN documentation: Response](https://developer.mozilla.org/en-US/docs/Web/API/Response)
- [Sample Functions: Returning an HTML Page](https://www.tencentcloud.com/document/product/1145/52702)
- [Sample Functions: Modifying a Response Header](https://www.tencentcloud.com/document/product/1145/52706)
- [Sample Functions: Performing an A/B Test](https://www.tencentcloud.com/document/product/1145/52707)