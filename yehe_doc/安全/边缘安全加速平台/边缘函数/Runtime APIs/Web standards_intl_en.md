Edge Functions designs a serverless code execution environment based on the **V8 JavaScript engine** and provides the following standardized Web APIs.

## JavaScript Standard Built-in Objects

Edge Functions supports all JavaScript standard built-in objects. For more information, see [Standard built-in objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects).

## URL
```typescript
const urlInfo = new URL('https://www.tencentcloud.com/');
```

The URL API is used to parse, construct, standardize, and encode URLs. For more information, see [URL](https://developer.mozilla.org/en-US/docs/Web/API/URL).

## Blob
```typescript
const blob = new Blob(['hello', 'world'], { type: 'text/plain' });
```

The Blob API represents a file-like object of immutable and raw data. For more information, see [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob).

## Base64
### btoa
```typescript
function btoa(data: string | ArrayBuffer | ArrayBufferView): string;
```

The btoa() method performs Base64 encoding. Unicode strings are not supported. For more information, see [btoa()](https://developer.mozilla.org/en-US/docs/Web/API/btoa).

### atob
```typescript
function atob(data: string): string;
```

The atob() method performs Base64 decoding. Unicode strings are not supported. For more information, see [atob()](https://developer.mozilla.org/en-US/docs/Web/API/atob).

### btoaUTF8
```typescript
function btoaUTF8(data: string): string;
```

The btoaUTF8() method performs Base64 encoding. Unicode strings are supported.

### atobUTF8
```typescript
function atobUTF8(data: string): string;
```

The atobUTF8() method performs Base64 decoding. Unicode strings are supported.

## EventTarget and Event

### EventTarget

```typescript
const eventTarget = new EventTarget();
```

The EventTarget API allows objects to publish and subscribe to events. For more information, see [EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget).

### Event
```typescript
const event = new Event('type name');
```

The Event API represents a basic event. For more information, see [Event](https://developer.mozilla.org/en-US/docs/Web/API/Event).

## AbortSignal and AbortController
### AbortSignal
```typescript
const signal = AbortSignal.abort();
```

The AbortSignal API represents a signal object that allows you to stop a request. For more information, see [AbortSignal](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal).

### AbortController
```typescript
const controller = new AbortController();
```

The AbortController API represents a controller object that allows you to stop a request. For more information, see [AbortController](https://developer.mozilla.org/en-US/docs/Web/API/AbortController).
