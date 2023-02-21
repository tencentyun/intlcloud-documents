By default, Tencent Cloud Command Line Interface (TCCLI) sends a request to the nearest endpoint to access a service. You can also specify an endpoint for a product.

## Directions
- Taking Cloud Virtual Machine (CVM) as an example, run the following command to set ap-guangzhou as the default endpoint:
```bash
tccli configure set cvm.endpoint cvm.ap-guangzhou.tencentcloudapi.com
```
- Run the following command to set ap-guangzhou as the endpoint in real time when calling the API:
```bash
tccli cvm DescribeZones --endpoint cvm.ap-guangzhou.tencentcloudapi.com
```
