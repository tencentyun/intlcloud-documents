## Overview
This document describes how to create an API under a service by defining it in the API Gateway console.

## Prerequisites
You have [created a service](https://intl.cloud.tencent.com/document/product/628/11787).

## Directions
1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway) and select **Service** in the left sidebar.
2. In the service list, click the name of the target service to view it.
3. In the service details, click the **Manage API** tab and choose to create a **General API** or **Microservice API** based on the backend business type.
4. Click **Create** and complete the subsequent configuration.

## API Types
In API Gateway, you can create APIs for five types of backend services, i.e., general APIs for public URL/IP, VPC, SCF, and Mock, and microservice APIs for TSF. More information is listed below:
<table>
<thead>
  <tr>
    <th>API Type</th>
    <th>Backend Service</th>
    <th>Documentation</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="4">General API</td>
    <td>Public URL/IP</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/628/39484">Creating APIs Connecting to the Public URL/IP Backend</a></td>
  </tr>
  <tr>
	<td>VPC resources</td>
  <td><a href="https://intl.cloud.tencent.com/document/product/628/39485">Creating APIs Connecting to the VPC Resource Backend</a></td>
  </tr>
  <tr>
    <td>SCF</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/628/39486">Creating APIs Connecting to the SCF Backend</a></td>
  </tr>
  <tr>
    <td>Mock</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/628/39487">Creating APIs Connecting to the Mock Backend</a></td>
  </tr>
  <tr>
    <td>Microservice API</td>
    <td>TSF</td>
    <td><a href="https://intl.cloud.tencent.com/document/product/628/39488">Creating APIs Connecting to the TSF Backend</a></td>
  </tr>
</tbody>
</table>

<span id="basic"></span>

## Basic API Information
 Basic information of an API includes:
 * API service: a service is a set of APIs for management. Any specific API must belong to a certain service. When creating an API, you can select an existing service or create a new one.
 * API path: path of an API request domain name
 * Method: API request method. The API path + API request method is the unique identifier of an API.
 * Description: API remarks
 ![](https://main.qcloudimg.com/raw/5c4ea8f97345c1fb821058acd9f01a38.png)

