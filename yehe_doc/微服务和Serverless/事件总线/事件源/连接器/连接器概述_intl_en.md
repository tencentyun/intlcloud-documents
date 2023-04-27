A connector is mainly used to proactively pull events from event sources and push them to a custom event bus in **standard format**. With it, you don't need to care about the underlying consumer delivery logic. You can bind one or more connectors in the event bus to automatically pull event content from message queues and gateways and push the content to the specified event bus.



- EventBridge connectors support the following event sources:
<table>
<thead>
<tr>
<th>Event Source</th>
<th>Configuration Method</th>
</tr>
</thead>
<tbody><tr>
<td>API gateway (APIGW) HTTP</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1108/42279">APIGW connector</a></td>
</tr>
<tr>
<td>CKafka</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1108/42280">CKafka connector</a></td>
</tr>
<tr>
<td>DTS data subscription</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1108/46991">DTS connector</a></td>
</tr>
</tbody></table>

- EventBridge provides the following connector management capabilities:
  - Creating connectors
  - Viewing connectors
  - Editing connectors
  - Starting connectors
  - Stopping connectors
  - Deleting connectors

