A **FetchEvent** object represents any incoming HTTP request event. Edge Functions processes HTTP requests by registering `fetch` event listeners.

## Overview
In Edge Functions, use [addEventListener](https://www.tencentcloud.com/document/product/1145/52683) to register a `fetch` event listener to generate an HTTP request event [FetchEvent](https://www.tencentcloud.com/document/product/1145/52688), thereby processing HTTP requests.

>! The `FetchEvent` object cannot be constructed directly. You can use `addEventListener` to register a `fetch` event listener to obtain the `event` object.

```typescript
// `event` is the `FetchEvent` object.
addEventListener('fetch', (event) => {
  event.respondWith(new Response('hello world!'));
});
```

## Attributes

### ClientId

```typescript
// event.clientId
readonly clientId: string;
```

The ClientId attribute specifies the ID allocated by Edge Functions for each request.

### request
```typescript
// event.request
readonly request: Request;
```
The request attribute specifies the HTTP request object initiated by the client. For more information, see [Request](https://www.tencentcloud.com/document/product/1145/52690).

### Methods
### respondWith

```typescript
event.respondWith(response: Response | Promise<Response>): void;
```

Edge Functions takes over requests from the client and uses this method to return custom responses. 

>! In the `fetch` event callback of the `addEventListener` event listener, the `event.respondWith()` method is used to respond to the client. If this method is not invoked, Edge Functions forwards the current request back to the origin.

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
      <td>response</td>
      <td>
        <a href="https://www.tencentcloud.com/document/product/1145/52691">Response</a>  
        Promise&lt;<a href="https://www.tencentcloud.com/document/product/1145/52691">Response</a>&gt;
      </td>
      <td>Yes</td>
      <td>
        The response to the HTTP request of the client.
      </td>
    </tr>
  </tbody>
</table>

### waitUntil
```typescript
event.waitUntil(task: Promise<any>): void;
```
The waitUntil() method is used to notify Edge Functions to wait until a `Promise`-based task is completed, extending the event processing lifecycle.

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
      <td>task</td>
      <td>
        Promise&lt;<a href="https://www.tencentcloud.com/document/product/1145/52691">Response</a>&gt;
      </td>
      <td>Yes</td>
      <td>
        The `Promise`-based task. 
      </td>
    </tr>
  </tbody>
</table>

### passThroughOnException
```typescript
event.passThroughOnException(): void;
```

The passThroughOnException() method is used to prevent runtime error responses. If the function code throws an unhandled exception, Edge Functions forwards the request back to the origin, enhancing the service availability.

## Sample Code
- If the `event.respondWith` method is not invoked, Edge Functions forwards the current request back to the origin.

```typescript
function handleRequest(request) {
  return new Response('Edge Functions, Hello World!');
}

addEventListener('fetch', event => {
  const request = event.request;
  // If the request URL contains the string /ignore/, Edge Functions forwards the current request back to the origin.
  if (request.url.indexOf('/ignore/') !== -1) {
    // The event.respondWith method is not invoked.
    return;
  }

  // Customize content in the edge function to respond to the client.
  event.respondWith(handleRequest(request));
});
```

- If the function code throws an unhandled exception, Edge Functions forwards the current request back to the origin.

```typescript
addEventListener('fetch', event => {
  // If the function code throws an unhandled exception, Edge Functions forwards the current request back to the origin. 
  event.passThroughOnException();
  throw new Error('Throw error');
});
```

## References 
- [MDN documentation: FetchEvent](https://developer.mozilla.org/en-US/docs/Web/API/FetchEvent)
- [Sample Functions: Returning an HTML Page](https://www.tencentcloud.com/document/product/1145/52702)
- [Sample Functions: Using the Cache API](https://www.tencentcloud.com/document/product/1145/52710)
