API gateway fee is calculated by recorded number of API calls and outbound traffic. A call is recorded when there is a request, call and return from client to API.
> Note: API gateway is free of charge during beta test periods.

API gateway outbound traffic is the outgoing traffic relative to API gateway. For example, if backend service is HTTP call, outbound traffic should be the traffic from API gateway to HTTP and API gateway traffic responding to front-end client. See the table below for outbound traffic relationships:

| HTTP Type | Source | Target | Traffic Type |
| --- | --- | --- | --- |
| HTTP request | Client, browser & sdk | API gateway | Inbound traffic | 
| HTTP request | API gateway | Backend service | Outbound traffic | 
| HTTP response | Backend service | API gateway | Inbound traffic | 
| HTTP response | API gateway | Client, browser, sdk | Outbound traffic | 


## Backend HTTP Call Billing

Traffic and billing methods for HTTP service differ across regions:

| HTTP Service Region | HTTP Address | Traffic Type | Billability |
| ---          |   ---     | ---   | ---   |
| In the region of the API service within Tencent Cloud | Private network address | Private network traffic | Free | 
| In the region of the API service within Tencent Cloud | Public network address | Public network traffic | Billed | 
| Not in the region of the API service within Tencent Cloud | Public network address | Public network traffic | Billed | 
| Non-Tencent Cloud Internet address | Public network address | Public network traffic | Billed | 

## Backend Serverless Cloud Function Call Billing

Traffic and billing methods for Serverless Cloud Function (SCF)  differ across regions:

| SCF Region | Traffic Type | Billability |
| ---          |   ---     | ---      |
| In the region of the API service | Private network traffic | Free | 
| Not in the region of the API service | Public network traffic | Billed | 

