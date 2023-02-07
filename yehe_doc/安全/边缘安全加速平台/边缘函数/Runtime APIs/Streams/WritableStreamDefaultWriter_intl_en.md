The **WritableStreamDefaultWriter** API defines a writer for a writable stream. It is designed based on the standard Web API [WritableStreamDefaultWriter](https://developer.mozilla.org/en-US/docs/Web/API/WritableStreamDefaultWriter).

 >! A `WritableStreamDefaultWriter` object cannot be constructed directly. You can use the [WritableStream.getWriter](https://www.tencentcloud.com/document/product/1145/52699#getwriter) method to construct a `WritableStreamDefaultWriter` object.

## Overview
```typescript
// Use TransformStream to construct a WritableStream object.
const { writable } = new TransformStream();

// Use the WritableStream object to obtain the writer. 
const writer = writable.getWriter();
```

## Attributes
### closed 
```typescript
// writer.closed
readonly closed: Promise<void>;
```

The closed attribute returns a Promise object. If the stream is closed, the status of the Promise object is `fulfilled`. If an exception occurs on the lock on the writer is released, the status of the Promise object is `rejected`.

### ready
```typescript
// writer.ready
readonly ready: Promise<void>;
```

The ready attribute returns a Promise object. When the size required by the internal queue of the stream changes from non-positive to positive, the Promise object is in the fulfilled status, indicating that it no longer applies backpressure.

### desiredSize
```typescript
// writer.desiredSize
readonly desiredSize: number;
```

The desiredSize attribute returns the size required to fill the internal queue of the stream.


## Methods
### write
```typescript
writer.write(chunk: Chunk): Promise<void>;
```

The write() method writes the `Chunk` data to the stream.

>! You cannot call the `write` method to initiate the next stream writing operation until the current stream writing operation ends.

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
      <td>chunk</td>
      <td><a href="#Chunk">Chunk</td>
      <td>Yes</td>
      <td>The chunk of data to be written to the stream.</li>
      </td>
    </tr>
  </tbody>
</table>

#### Chunk[](id:Chunk)
The `Chunk` parameter indicates the data to be written to the stream.

```typescript
type Chunk = string | ArrayBuffer | ArrayBufferView;
```

### close
```typescript
writer.close(): Promise<void>;
```

The close() method closes the current stream.

### abort
```typescript
writer.abort(reason?: string): Promise<string>;
```
The abort() method stops the current stream.

### releaseLock
```typescript
writer.releaseLock(): void;
```

The releaseLock() method cancels the association with the stream and releases the lock on the stream.

## References 
- [MDN documentation: WritableStreamDefaultWriter](https://developer.mozilla.org/en-US/docs/Web/API/WritableStreamDefaultWriter)
