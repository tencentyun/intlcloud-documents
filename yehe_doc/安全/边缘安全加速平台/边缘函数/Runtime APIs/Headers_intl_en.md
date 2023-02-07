The **Headers** API is designed based on the standard Web API [Headers](https://developer.mozilla.org/en-US/docs/Web/API/Headers). You can use this API to perform operations on HTTP request and response headers.

## Constructor API

```typescript
const headers = new Headers(init?: object | Array<[string, string]> | Headers);
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
      <td>init</td>
      <td>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object">object</a> | </br>
        <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array">Array&lt;[string, string]&gt;</a> | </br>
        Headers
      </td>
      <td>No</td>
      <td>
        The HTTP header that is used to pre-populate the Headers object. Valid parameter types:<br/>
        <li>
          <font color="#9ba6b7">object</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            The Constructor API enumerates all enumerable attributes that are included in the specified object and pre-populates the attributes to the new Headers object.
          </div> 
        </li>
        <li>
          <font color="#9ba6b7">Array&lt;[string, string]&gt;</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            Each element in the array is a <code>key-value</code> pair. Example: [key, value]. The Constructor API traverses the array and pre-populates the key-value pairs to the new Headers object.
          </div> 
        </li>
        <li>
          <font color="#9ba6b7">Headers</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            The Constructor API copies all fields from an existing Headers object to the new Headers object.
          </div> 
        </li>
      </td>
    </tr>
  </tbody>
</table>

## Methods
### append

```typescript
headers.append(name: string, value: string): void;
```

The append() method appends a new value to a header that is specified by the `Headers` object. If the header does not exist, the append() method directly adds the header.

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
			<td>name</td>
			<td>string</td>
			<td>Yes</td>
			<td>The name of the HTTP header that you want to add to the Headers object.</td>
		</tr>
    <tr>
			<td>value</td>
			<td>string</td>
			<td>Yes</td>
			<td>The value of the HTTP header that you want to add.</td>
		</tr>
	</tbody>
</table>

### delete
```typescript
headers.delete(name: string): void;
```

The delete() method deletes the specified header from the `Headers` object. 

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
			<td>name</td>
			<td>string</td>
			<td>Yes</td>
			<td>The name of the HTTP header that you want to delete from the Headers object.</td>
		</tr>
	</tbody>
</table>


### entries
```typescript
headers.entries(): iterator;
```

The entries() method obtains an array of all key-value pairs from the `Headers` object. The key-value pairs are in the format of [name, value]. For valid return values, see [Iteration protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols).

### forEach
```typescript
headers.forEach(callback: (name: string, value: string) => void | number): void;
```

The forEach() method traverses all headers that are included in the `Headers` object. If `callback` returns a non-zero value, traversal is stopped.

>! The `forEach` method does not comply with Web API standards. Edge Functions extends the functionality of the method based on Web API standards to provide an efficient way to traverse headers.

### get
```typescript
headers.get(name: string): string;
```

The get() method obtains the value of the specified header from the `Headers` object.

### has
```typescript
headers.has(name: string): boolean;
```
The has() method checks whether the `Headers` object contains the specified header.

### keys
```typescript
headers.keys(): iterator;
```

The keys() method obtains all keys that are included in the `Headers` object. For valid return values, see [Iteration protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols).

### set
```typescript
headers.set(name: string, value: string): void;
```
The set() method sets a new value for an existing header in the `Headers` object. If the header does not exist, the set() method directly adds the header.

### values
```typescript
headers.values(): iterator;
```
The values() method obtains all values that are included in the `Headers` object. For valid return values, see [Iteration protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols).

## Sample Code
```typescript
function handleEvent() {
  const headers = new Headers({
    'my-header-x': 'hello world',
  });

  const response =  new Response('hello world',{
    headers,
  });
  return response;
}

addEventListener('fetch', (event) => {
  event.respondWith(handleEvent(event));
});
```

## References
- [MDN documentation: Headers](https://developer.mozilla.org/en-US/docs/Web/API/Headers)
- [Sample Functions: Protecting Data from Tampering](https://www.tencentcloud.com/document/product/1145/52714)
- [Sample Functions: Authenticating a Request Header](https://www.tencentcloud.com/document/product/1145/52705)
- [Sample Functions: Modifying a Response Header](https://www.tencentcloud.com/document/product/1145/52706)
