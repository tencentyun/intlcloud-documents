 The **ReadableStream** API represents a readable stream or readable end. It is designed based on the standard Web API [ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream).

 >! A `ReadableStream` object cannot be constructed directly. You can use [TransformStream](https://www.tencentcloud.com/document/product/1145/52698) to construct a `ReadableStream` object.

## Overview

```typescript
// Use TransformStream to construct a ReadableStream object.
const { readable } = new TransformStream();
```

## Attributes
```typescript
// readable.locked
readonly locked: boolean;
```
The locked attribute indicates whether a stream is locked.

>? A stream is locked in the following scenarios:
>- The stream has no more than one activated `reader`. Before the `reader` calls the `releaseLock()` method, the stream is locked. 
>- The stream is in being piped. The stream is locked until the piping ends.

## Methods
>! Before you use any of the following methods, make sure that the stream is not locked. Otherwise, an exception is returned.

### getReader
```typescript
readable.getReader(options?: ReaderOptions): ReadableStreamDefaultReader | ReadableStreamBYOBReader;
```

The getReader() method creates a `reader` and locks the current stream until the `reader` calls the `releaseLock()` method.

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
      <td>options</td>
      <td><a href="#ReaderOptions">ReaderOptions</td>
      <td>Yes</td>
      <td>The configuration items for generating the reader.</li>
      </td>
    </tr>
  </tbody>
</table>

#### ReaderOptions[](id:ReaderOptions)
The following table describes the parameters of the `ReaderOptions` object.

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
			<td>mode</td>
			<td>string</td>
			<td>No</td>
			<td>
        <code>Reader</code> The type of the `reader`. Default value: <code>undefined</code>. Valid values:<br/>
        <li>
          <font color="#9ba6b7">undefined</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            Create a <code>reader</code> of the <a href="https://www.tencentcloud.com/document/product/1145/52697">ReadableStreamDefaultReader</a> type.
          </div>
        </li>
        <li>
          <font color="#9ba6b7">byob</font><br/>
          <div style="padding-left: 20px;padding-bottom: 6px">
            Create a <code>reader</code> of the <a href="https://www.tencentcloud.com/document/product/1145/52696">ReadableStreamBYOBReader</a> type.
          </div>
        </li>
      </td>
		</tr>
	</tbody>
</table>

### pipeThrough
```typescript
readable.pipeThrough(transformStream: TransformStream, options?: PipeToOptions): ReadableStream; 
```

The pipeThrough() method pipes the data of the current readable stream to the writable side of the `transformStream` and returns the readable side of the `transformStream`.

>! During the piping, the `writable` side of the current stream is locked.

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
      <td>transformStream</td>
      <td><a href="https://www.tencentcloud.com/document/product/1145/52698">TransformStream</td>
      <td>Yes</td>
      <td>The destination to which the current stream is piped.</td>
    </tr>
    <tr>
      <td>options</td>
      <td><a href="#PipeToOptions">PipeToOptions</td>
      <td>Yes</td>
      <td>The configuration items for piping the stream.</td>
    </tr>
  </tbody>
</table>

#### PipeToOptions[](id:PipeToOptions)

The following table describes the configuration items for piping the stream.

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
			<td>preventClose</td>
			<td>boolean</td>
			<td>No</td>
			<td>If the value is <code>true</code>, the writable stream is not closed along with the readable stream.</td>
		</tr>
    <tr>
			<td>preventAbort</td>
			<td>boolean</td>
			<td>No</td>
			<td>If the value is <code>true</code>, the writable stream is not stopped when an exception occurs on the readable stream.</td>
		</tr>
    <tr>
			<td>preventCancel</td>
			<td>boolean</td>
			<td>No</td>
			<td>If the value is <code>true</code>, the writable stream is not closed when the readable stream is incorrect.</td>
		</tr>
    <tr>
			<td>signal</td>
			<td><a href="https://www.tencentcloud.com/document/product/1145/52694#abortsignal">AbortSignal</a></td>
			<td>No</td>
			<td>If `signal` is stopped, ongoing pipe operations are stopped.</td>
		</tr>
	</tbody>
</table>

### pipeTo
```typescript
readable.pipeTo(destination: WritableStream, options?: PipeToOptions): Promise<void>;
```

The pipeTo() method pipes the current readable stream to the `destination` writable stream.

>! During the piping, the `destination` of the current stream is locked.

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
      <td>destination</td>
      <td><a href="https://www.tencentcloud.com/document/product/1145/52699">WritableStream</td>
      <td>Yes</td>
      <td>The writable stream.</td>
    </tr>
    <tr>
      <td>options</td>
      <td><a href="#PipeToOptions">PipeToOptions</td>
      <td>Yes</td>
      <td>The configuration items for piping the stream.</td>
    </tr>
  </tbody>
</table>

### tee
```typescript
readable.tee(): [ReadableStream, ReadableStream];
```
The tee() method tees the current readable stream and returns two independent branches.

### cancel
```typescript
readable.cancel(reason?: string): Promise<string>;
```

The cancel() method ends the current stream.

## References 
- [MDN documentation: ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)
- [Sample Functions: Merging Resources and Responding in Streaming Mode](https://www.tencentcloud.com/document/product/1145/52713)
- [Sample Functions: Rewriting a m3u8 File and Configuring Authentication](https://www.tencentcloud.com/document/product/1145/52715)
