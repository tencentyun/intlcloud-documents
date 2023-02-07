A **TransformStream** consists of a readable stream and a writable stream. It is designed based on the standard Web API [TransformStream](https://developer.mozilla.org/en-US/docs/Web/API/TransformStream).

## Constructor API
```typescript
const { readable, writable } = new TransformStream(transformer?: any, writableStrategy?: WritableStrategy);
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
      <td>transformer</td>
      <td>any</td>
      <td>No</td>
      <td><strong>This parameter is not supported. The values do not take effect and are ignored automatically.</strong></td>
    </tr>
    <tr>
      <td>writableStrategy</td>
      <td><a href="#WritableStrategy">WritableStrategy</a></td>
      <td>No</td>
      <td>The strategy for the writable side.</td>
    </tr>
  </tbody>
</table>

#### WritableStrategy[](id:WritableStrategy)

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
			<td>highWaterMark</td>
			<td>number</td>
			<td>Yes</td>
			<td>
        The size of the writable buffer in bytes. Default value: 32K. Maximum value: 256K. If you enter a value greater than 256K, the value is changed to 256K automatically.
      </td>
		</tr>
	</tbody>
</table>

## Attributes
### readable
```typescript
readonly readable: ReadableStream;
```

The readable stream. For more information, see [ReadableStream](https://www.tencentcloud.com/document/product/1145/52695).

### writable
```typescript
readonly writable: WritableStream;
```

The writable stream. For more information, see [WritableStream](https://www.tencentcloud.com/document/product/1145/52699).

## Sample Code
```typescript
async function handleEnterRoom() {
  // Generate readable streams and writeable streams.
  const { readable, writable } = new TransformStream();
  // Fetch a remote resource. 
  const response = await fetch('https://www.tencentcloud.com/');
  // Respond to the client in streaming mode. 
  response.body.pipeTo(writable);

  return new Response(readable, response);
}

addEventListener('fetch', (event) => {
  event.respondWith(handleEvent(event));
});
```

## References 
- [MDN documentation: TransformStream](https://developer.mozilla.org/en-US/docs/Web/API/TransformStream)
- [Sample Functions: Merging Resources and Responding in Streaming Mode](https://www.tencentcloud.com/document/product/1145/52713)
- [Sample Functions: Rewriting a m3u8 File and Configuring Authentication](https://www.tencentcloud.com/document/product/1145/52715)