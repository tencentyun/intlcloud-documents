This API is used to register an event listener for a target. The event listener triggers an edge function when the specified type of event is delivered to the target. Only `fetch` request events are supported. If a `fetch` event occurs after a `fetch` event listener is registered, the event listener generates a [FetchEvent](https://www.tencentcloud.com/document/product/1145/52688) object to process the HTTP request.

## Overview

```typescript
function addEventListener(type: string, listener: (event: FetchEvent) => void): void;
```

In Edge Functions, only one event listener takes effect for the same type of event. If more than one event listeners are registered for the same type of event, only the last event listener takes effect.

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
      <td>type</td>
      <td>string</td>
      <td>Yes</td>
      <td>
        <p>The event type to listen for.</p>
        <li>Only <code>fetch</code> request events are supported.</li>
        <li>If you specify a request event type other than <code>fetch</code>, the Edge Functions engine throws an <code>Error</code> exception.</li>
      </td>
    </tr>
    <tr>
      <td>listener</td>
      <td>
        (event: <a href="https://www.tencentcloud.com/document/product/1145/52688">FetchEvent</a>) => void
      </td>
      <td>Yes</td>
      <td>
        <p>The event listener that is used to process event callbacks.</p>
        <li>You can register an event listener to generate <a href="https://www.tencentcloud.com/document/product/1145/52688">FetchEvent</a> objects to handle <code>fetch</code> request events.</li>
      </td>
    </tr>
  </tbody>
</table>

## Sample Code
```js
// Register a fetch event listener.
addEventListener('fetch', (event) => {
  // Respond to the client.
  event.respondWith(new Response('Hello World!'));
});
```

## References 
- [MDN documentation: addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
- [Sample Functions: Returning an HTML Page](https://www.tencentcloud.com/document/product/1145/52702)
- [Sample Functions: Returning a JSON Object](https://www.tencentcloud.com/document/product/1145/52703)
