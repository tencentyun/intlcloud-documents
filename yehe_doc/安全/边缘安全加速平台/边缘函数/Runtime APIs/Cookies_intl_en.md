The **Cookies** API provides a group of methods for you to manage cookies.

>! The unique keys of Cookies objects are in the format of `name + domain + path`. You can manage Cookies objects based on the unique keys.

## Constructor API
```typescript
const cookies = new Cookies(cookieStr?: string, isSetCookie?: boolean);
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
      <td>cookieStr</td>
      <td>string</td>
      <td>No</td>
      <td>The Cookie string or <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie">Set-Cookie</a> string.</td>
    </tr>
    <tr>
      <td>isSetCookie</td>
      <td>boolean</td>
      <td>No</td>
      <td>Specifies whether the value of the cookieStr parameter is a <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie">Set-Cookie</a> string. Default value: false.</td>
    </tr>
  </tbody>
</table>

## Methods
### get
```typescript
cookies.get(name?: string): null | Cookie | Array<Cookie>;
```

The get() method obtains the [Cookie](#Cookie) object of the specified name. If multiple objects are matched, a [Cookie](#Cookie) array is returned.

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
      <td>name</td>
      <td>string</td>
      <td>No</td>
      <td>
        The name of <code>Cookie</code> object. Valid options:
        <li>
          <font color="#9ba6b7">Default name</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            Obtains all Cookie objects.
          </div> 
        </li>
        <li>
          <font color="#9ba6b7">Specified name</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            Obtains the Cookie object of the specified name. If multiple objects are matched, a <a href="#Cookie">Cookie</a> array is returned.
          </div> 
        </li>
      </td>
    </tr>
  </tbody>
</table>

#### Cookie[](id:Cookie)
The following table describes the attributes of the `Cookie` object. For more information, see [Set-Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie).

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
			<td>name</td>
			<td>string</td>
			<td>Yes</td>
			<td>The name of the <code>Cookie</code> object.</td>
		</tr>
    <tr>
			<td>value</td>
			<td>string</td>
			<td>Yes</td>
			<td>The value of the <code>Cookie</code> object.</td>
		</tr>
    <tr>
			<td>domain</td>
			<td>string</td>
			<td>Yes</td>
			<td>The host to which the <code>Cookie</code> object will be sent.</td>
		</tr>
    <tr>
			<td>path</td>
			<td>string</td>
			<td>Yes</td>
			<td>The path to which the <code>Cookie</code> object will be sent.</td>
		</tr>
    <tr>
			<td>expires</td>
			<td>string</td>
			<td>Yes</td>
			<td>
        The maximum effective time of the <code>Cookie</code> object. The value meets the <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Date">HTTP Date</a> header standards.
      </td>
		</tr>
    <tr>
			<td>max_age</td>
			<td>string</td>
			<td>Yes</td>
			<td>The number of seconds until the <code>Cookie</code> object expires.</td>
		</tr>
    <tr>
			<td>samesite</td>
			<td>string</td>
			<td>Yes</td>
			<td>Controls whether the <code>Cookie</code> object is sent with cross-site requests, providing some protection against cross-site request forgery (CSRF) attacks.</td>
		</tr>
    <tr>
			<td>httponly</td>
			<td>boolean</td>
			<td>Yes</td>
			<td>Forbids JavaScript from accessing the <code>Cookie</code> object. The attribute is carried only by HTTP requests.</td>
		</tr>
    <tr>
			<td>secure</td>
			<td>boolean</td>
			<td>Yes</td>
			<td>Specifies that the <code>Cookie</code> object can be carried only by HTTPS requests.</td>
		</tr>
	</tbody>
</table>


### set
```typescript
cookies.set(name: string, value: string, options?: Cookie): boolean;
```

The set() method adds cookies in overwrite mode. If `true` is returned, cookies are successfully added. If `false` is returned, cookies fail to be added because the number of cookies exceeds the upper limit. For more information, see [Cookie limits](#CookiesLimit).

>! Cookies are added in overwrite mode based on unique keys in the format of `name + domain + path`.

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
      <td>name</td>
      <td>string</td>
      <td>Yes</td>
      <td>The name of the <code>Cookie</code> object.</td>
    </tr>
    <tr>
      <td>value</td>
      <td>string</td>
      <td>Yes</td>
      <td>The value of the <code>Cookie</code> object.</td>
    </tr>
    <tr>
      <td>Cookie</td>
      <td>string</td>
      <td>No</td>
      <td>The configuration items of the <a href="#Cookie">Cookie</a> object.</td>
    </tr>
  </tbody>
</table>

### append
```typescript
cookies.append(name: string, value: string, options?: Cookie): boolean;
```

The append() method appends cookies in scenarios where multiple values correspond to the same name. If `true` is returned, cookies are successfully appended. If `false` is returned, cookies fail to be appended because the value already exists or the number of cookies exceeds the upper limit. For more information, see [Cookie limits](#CookiesLimit).

>! Cookies are appended based on unique keys in the format of `name + domain + path`.

### remove
```typescript
cookies.remove(name: string, options?: Cookie): boolean;
```

The remove() method deletes cookies.

>! Cookies are deleted based on unique keys in the format of `name + domain + path`.

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
      <td>name</td>
      <td>string</td>
      <td>Yes</td>
      <td>The name of the <code>Cookie</code> object.</td>
    </tr>
    <tr>
      <td>options</td>
      <td><a href="#Cookie">Cookie</a></td>
      <td>Yes</td>
      <td>
        The configuration items of the <a href="#Cookie">Cookie</a> object. The configuration items `domain` and `path` support the wildcard character (*), indicating that all items are matched.
      </td>
    </tr>
  </tbody>
</table>

## Use Limits
### Automatic escape of special characters
- The following characters are automatically escaped if they are contained in the value of the `name` attribute: ` " ( ) , / : ; ? < = > ? @ [ ] \ { }`. `0x00~0x1F` and `0x7F~0xFF`.

- The following characters are automatically escaped if they are contained in the value of the `value` attribute: ` , ， ; " \`. `0x00~0x1F` and `0x7F~0xFF`.

### Cookie limits[](id:CookiesLimit)
- The size of the Cookie attribute `name` cannot exceed 64 bytes.

- The accumulated size of the Cookie attributes `value, domain, path, expires, max_age, and samesite` cannot exceed 1 KB.

- The total length of all fields after escape of cookies cannot exceed 4 KB.

- The total number of Cookie objects contained in cookies cannot exceed 64.

## Sample Code
```typescript
function handleEvent(event) {
  const response = new Response('hello world');
    
  // Generate a Cookies object.
  const cookies = new Cookies('ssid=helloworld; expires=Sun, 10-Dec-2023 03:10:01 GMT; path=/; domain=.tencentcloud.com; samesite=.tencentcloud.com', true);
  
  // Set the response header Set-Cookie.
  response.setCookies(cookies);

  return response;
}

addEventListener('fetch', (event) => {    
  event.respondWith(handleEvent(event));
});
```

## References 
- [MDN documentation: Set-Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie)
- [Sample Functions: Performing an A/B Test](https://www.tencentcloud.com/document/product/1145/52707)
- [Sample Functions: Setting Cookies](https://www.tencentcloud.com/document/product/1145/52708)
