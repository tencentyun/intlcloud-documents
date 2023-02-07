The **Cache** API is designed based on the standard Web API [Cache](https://developer.mozilla.org/en-US/docs/Web/API/Cache). During the runtime of edge functions, a global `caches` object that provides a group of methods for cache-related operations is injected.

>? The cached content takes effect only on the current data node and is not automatically copied to other data nodes.

## Constructor API
- Use `caches.default` to fetch the default cache instance.

```typescript
// Fetch the default cache instance.
const cache = caches.default;

// This method provides the same effect as `caches.default`.
await caches.open('default');
```

- Use `caches.open` to create a cache instance with the specified namespace.

```typescript
// Create a cache instance with the specified namespace.
const cache = await caches.open(namespace); 
```

### Parameters
The following table describes the parameters of the `caches.open(namespace)` method.

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
      <td>namespace</td>
      <td>string</td>
      <td>Yes</td>
      <td>
        The namespace of the cache.
        <li>The value "default" specifies the default instance. You can also use <code>caches.default</code> to fetch a default instance.</li>
      </td>
    </tr>
  </tbody>
</table>

## Methods

### match
```typescript
cache.match(request: string | Request, options?: MatchOptions): Promise<Response | undefined>
```

The match() method fetches the [Response](https://www.tencentcloud.com/document/product/1145/52691) cache associated with the request and returns a Promise object. If the cache exists, the object contains the Response object. If not, the object contains undefined.

>! The **cache.match()** method does not forward requests to the origin. If the cache expires, the method throws a 504 error.

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
      <td>request</td>
      <td>string | <a href="https://www.tencentcloud.com/document/product/1145/52690">Request</a></td>
      <td>Yes</td>
      <td>
        The request object. The following method and headers are supported:<br>
        <li>
          <font color="#9ba6b7">GET</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">Only the <code>GET</code> method is supported. If this parameter is set to a string, the string is used as a URL to construct a Request object.</div>
        </li>
        <li>
          <font color="#9ba6b7">Range</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">If the request contains a <code>Range</code> header and the cached response contains the Accept-Ranges header, the 206 response is returned.</div>
        </li>
        <li>
          <font color="#9ba6b7">If-Modified-Since</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">If the request contains a <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Modified-Since">If-Modified-Since</a> header and the cached response contains a <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Last-Modified">Last-Modified</a> header with the same value as that of the If-Modified-Since header, the 304 response is returned.</div>
        </li>
        <li>
          <font color="#9ba6b7">If-None-Match</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">If the request contains a <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match">If-None-Match</a> header and the cached response contains an <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag">ETag</a> header with the same value as that of the If-Modified-Since header, the 304 response is returned.</div>
        </li>
      </td>
    </tr>
    <tr>
      <td>options</td>
      <td><a href="#MatchOptions">MatchOptions</a></td>
      <td>No</td>
      <td>The options.</td>
    </tr>
  </tbody>
</table>

#### MatchOptions[](id:MatchOptions)
<table>
	<thead>
		<tr>
			<th width="10%">Parameter</th>
			<th width="15%">Type</th>
			<th width="10%">Example</th>
			<th width="65%">Description</th>
	</tr>
	</thead>
	<tbody>
		<tr>
			<td>ignoreMethod</td>
			<td>boolean</td>
			<td>true</td>
			<td>Specifies whether to ignore the request method. If you set this parameter to true, the request is considered to be a GET request regardless of its actual method.</td>
		</tr>
	</tbody>
</table>

### put
```typescript
cache.put(request: string | Request, response: Response): Promise<undefined>
```
The put() method tries to add a response to the cache by using the given request as the cache key. A Promise<undefined> object is returned regardless of whether caching is successful.

>! The put() method returns a 413 error if the Cache-Control header of the object specified in the **response** parameter instructs not to cache. 

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
			<td>request</td>
			<td>string | <a href="https://www.tencentcloud.com/document/product/1145/52690">Request</a></td>
			<td>Yes</td>
			<td>
				The cache key.
				<li>
          <font color="#9ba6b7">GET</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            The <code>request</code> parameter supports only the GET method. If other methods are specified, an error is thrown.
          </div>
        </li>
        <li>
          <font color="#9ba6b7">string</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            If the <code>request</code> parameter is set to a string, the string is used as a URL to construct a <a href="https://www.tencentcloud.com/document/product/1145/52690">Request</a> object.
          </div>
        </li>
			</td>
		</tr>
		<tr>
			<td>response</td>
			<td><a href="https://www.tencentcloud.com/document/product/1145/52691">Response</a></td>
			<td>Yes</td>
			<td>
        The cache content.<br>
        <li>
          <font color="#9ba6b7">Cache-Control</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            Valid values: s-maxage, max-age, no-store, no-cache, and private. The values no-store, no-cache, and private indicate no caching. If you use these values, the <code>cache.put</code> method returns a 413 error.
          </div>
        </li>
        <li>
          <font color="#9ba6b7">Pragma</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            If <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control">Cache-Control</a> is not specified and <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Pragma">Pragma</a> is set to no-cache, no caching is performed.
          </li>
        <li>
          <font color="#9ba6b7">ETag</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            If the <code>request</code> parameter of the <code>cache.match</code> method contains a <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match">If-None-Match</a> header, you can associate it with <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag">ETag</a>.
          </div>
        </li>
        <li>
          <font color="#9ba6b7">Last-Modified</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            If the <code>request</code> parameter of the <code>cache.match</code> method contains a <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Modified-Since">If-Modified-Since</a> header, you can associate it with <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Last-Modified">Last-Modified</a>.
          </div>
        </li>	
        <li>
          <font color="#9ba6b7">416 Range Not Satisfiable</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            If the object specified in the <code>response</code> parameter is <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/416">416 Range Not Satisfiable</a>, no caching is performed.
          </div>
        </li>
			</td>
		</tr>
	</tbody>
</table>

#### Parameter limits
The `cache.put` method throws an error in the following scenarios:
- The `request` parameter specifies a method other than the GET method.
- The status code of the `response` parameter is [206 Partial Content](https://www.webfx.com/web-development/glossary/http-status-codes/what-is-a-206-status-code/). 
- The `response` parameter contains a <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Vary">Vary: *</a> header. 


### delete

```typescript
cache.delete(request: string | Request, options?: DeleteOptions): Promise<boolean>
```
The delete() method deletes the response associated with the request from the cache. If no network exception occurs, a Promise containing `true` is returned. Otherwise, a Promise containing `false` is returned.

#### Parameters
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
      <td>request</td>
      <td>string | <a href="https://www.tencentcloud.com/document/product/1145/52690">Request</a></td>
      <td>Yes</td>
      <td>
        The cache key.
        <li>
          <font color="#9ba6b7">GET</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            The <code>request</code> parameter supports only the GET method.
          </div>
        </li>
        <li>
          <font color="#9ba6b7">string</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px"> 
            If the <code>request</code> parameter is set to a string, the string is used as a URL to construct a <a href="https://www.tencentcloud.com/document/product/1145/52690">Request</a> object.
          </div>
        </li>
      </td>
    </tr>
    <tr>
      <td>options</td>
      <td><a href="#DeleteOptions">DeleteOptions</a></td>
      <td>No</td>
      <td>The options.</td>
    </tr>
  </tbody>
</table>

#### DeleteOptions[](id:DeleteOptions)

<table>
  <thead>
    <tr>
    <th width="15%">Parameter</th>
    <th width="15%">Type</th>
    <th width="10%">Example</th>
    <th width="60%">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ignoreMethod</td>
      <td>boolean</td>
      <td>true</td>
      <td>Specifies whether to ignore the <code>request</code> method. If you set this parameter to true, the request is considered to be a GET request regardless of its actual method.</td>
    </tr>
  </tbody>
</table>

## References 
- [MDN documentation: Cache](https://developer.mozilla.org/en-US/docs/Web/API/Cache)
- [Sample Functions: Caching POST Requests](https://www.tencentcloud.com/document/product/1145/52711)
- [Sample Functions: Using the Cache API](https://www.tencentcloud.com/document/product/1145/52710)
