 The **ReadableStreamBYOBReader** API defines a reader for a readable stream. It is designed based on the standard Web API [ReadableStreamBYOBReader](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamBYOBReader). `BYOB` is an abbreviation of bring your own buffer. A ReadableStreamBYOBReader object allows to read data from streams and write the read data to the buffer, thereby reducing replicas.

 >! A `ReadableStreamBYOBReader` object cannot be constructed directly. You can use the [ReadableStream.getReader](https://www.tencentcloud.com/document/product/1145/52695#getreader) method to construct a `ReadableStreamBYOBReader` object.

## Overview 
```typescript
// Use TransformStream to construct a ReadableStream object.
const { readable } = new TransformStream();

// Use the ReadableStream object to obtain the reader.
const reader = readable.getReader({
  mode: 'byob',
});
```

## Attributes

```typescript
// readable.locked
readonly locked: boolean;
```

The locked attribute returns a Promise object. If the stream is closed, the status of the Promise object is `fulfilled`. If an exception occurs on the stream or the lock on the reader is released, the status of the Promise object is `rejected`.

## Methods
### read
```typescript
reader.read(bufferView: ArrayBufferView): Promise<{value: ArrayBufferView, done: boolean}>;
```

The read() method reads data from the stream and writes the read data to the `bufferView` on the buffer.

>! You cannot initiate the next stream reading operation until the current stream reading operation ends.

#### Returned values
The `reader.read` method returns a Promise object that contains the read data and the reading status.

- If a chunk is available, the Promise object is in the `fulfilled` status and contains an object in the `{ value: theChunk, done: false }` format.
- If the stream is closed, the status of the Promise object is switched to `fulfilled`, and an object in the `{ value: theChunk, done: true }` format is contained.
- If an exception occurs on the stream, the Promise object is in the `rejected` status, and the relevant error information is included.

### cancel
```typescript
reader.cancel(reason?: string): Promise<string>;
```
The cancel() method closes the stream and ends the reading operation.

### releaseLock
```typescript
reader.releaseLock(): void;
```

The releaseLock() method cancels the association with the stream and releases the lock on the stream.


## References 
- [MDN documentation: ReadableStreamBYOBReader](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamBYOBReader)
