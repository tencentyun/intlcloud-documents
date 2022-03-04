### Is manual recognition supported? How do I access it?

Yes, and a separate manual recognition API needs to be accessed. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to get the access documentation.

### Is there a fee for accessing manual recognition?

Yes. You can [contact us](https://intl.cloud.tencent.com/contact-us) for pricing information.

### Can I configure callbacks for manual recognition based on different push domain names?

Yes. You can create multiple sub-accounts under the root account and use them to configure callbacks for manual recognition. Then, their keys can be used to call the service.

### How does manual recognition determine whether content is non-compliant?

After content is pushed to manual recognition, the message called back contains the `ManualDetailCode` field, which represents the type of violation identified by manual recognition.

### Can the QPS of manual recognition be adjusted?

Yes. If you have such needs, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance with adjustment on the backend.