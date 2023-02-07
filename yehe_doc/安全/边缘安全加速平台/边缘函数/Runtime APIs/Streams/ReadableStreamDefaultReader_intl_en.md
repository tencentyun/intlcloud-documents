 The **ReadableStreamDefaultReader** API defines a reader for a readable stream. It is designed based on the standard Web APIs [ReadableStreamDefaultReader](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamDefaultReader).

 >! A `ReadableStreamDefaultReader` object cannot be constructed directly. You can use the [ReadableStream.getReader](https://www.tencentcloud.com/document/product/1145/52695#getreader) method to construct a `ReadableStreamDefaultReader` object.

## Overview

```typescript
// Use TransformStream to construct a ReadableStream object.
const { readable } = new TransformStream();

// Use the ReadableStream object to obtain the reader.
const reader = readable.getReader();
```

## Attributes
### closed 
```typescript
// reader.closed
readonly closed: Promise<void>;
```

The closed attribute returns a Promise object. If the stream is closed, the status of the Promise object is `fulfilled`. If an exception occurs on the stream or the lock on the reader is released, the status of the Promise object is `rejected`.

## Methods
### read
```typescript
reader.read(): Promise<{value: Chunk, done: boolean}>;
```

The read() method reads data from the stream.

>! You cannot initiate the next stream reading operation until the current stream reading operation ends.

#### Returned values
The `reader.read` method returns a Promise object that contains the read data [Chunk](#Chunk) and the reading status.

- If a chunk is available, the Promise object is in the `fulfilled` status and contains an object in the `{ value: theChunk, done: false }` format.
- If the stream is closed, the Promise object is in the `fulfilled` status and contains an object in the `{ value: undefined, done: true }` format.
- If an exception occurs on the stream, the Promise object is in the `rejected` status, and the relevant error information is included.

#### Chunk[](id:Chunk)
The `Chunk` parameter indicates the data to be read from the stream.

```typescript
type Chunk = string | ArrayBuffer | ArrayBufferView;
```

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
- [MDN documentation: ReadableStreamDefaultReader](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamDefaultReader)
