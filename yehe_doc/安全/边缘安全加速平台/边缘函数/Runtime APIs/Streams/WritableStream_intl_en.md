The **WritableStream** API represents a writable stream or writable side. It is designed based on the standard Web API [WritableStream](https://developer.mozilla.org/en-US/docs/Web/API/WritableStream).

 >! A `WritableStream` object cannot be constructed directly. You can use [TransformStream](https://www.tencentcloud.com/document/product/1145/52698) to construct a `WritableStream` object.

## Overview

```typescript
// Use TransformStream to construct a WritableStream object.
const { writable } = new TransformStream();
```

### Attributes
#### locked
```typescript
// writable.locked 
readonly locked: boolean;
```

The locked attribute indicates whether the stream is locked.

>? A stream is locked in the following scenarios:
>- The stream has no more than one activated `writer`. Before the `writer` calls the `releaseLock()` method, the stream is locked. 
>- The stream is in being piped. The stream is locked until the piping ends.

#### highWaterMark
```typescript
// writable.highWaterMark
readonly highWaterMark: number;
```

The size of the writable buffer in bytes. Default value: 32K. Maximum value: 256K. If you enter a value greater than 256K, the value is changed to 256K automatically.

## Methods 
>! Before you use any of the following methods, make sure that the stream is not locked. Otherwise, an exception is returned.

### getWriter
```typescript
writable.getWriter(): WritableStreamDefaultWriter;
```

The getWriter() method creates a writer and locks the current stream until the writer calls the releaseLock() method. For more information about the returned values, see [WritableStreamDefaultWriter](https://www.tencentcloud.com/document/product/1145/52700).

### close
```typescript
writable.close(): Promise<void>;
```

The close() method closes the current stream.

### abort
```typescript
writable.abort(reason?: string): Promise<string>;
```
The abort() method stops the current stream.

## References 
- [MDN documentation: WritableStream](https://developer.mozilla.org/en-US/docs/Web/API/WritableStream)
- [Sample Functions: Merging Resources and Responding in Streaming Mode](https://www.tencentcloud.com/document/product/1145/52713)
- [Sample Functions: Rewriting a m3u8 File and Configuring Authentication](https://www.tencentcloud.com/document/product/1145/52715)