## Web

A JavaScript package is provided for your web application. You can integrate it in the following two steps:

## 1. Integrate JavaScript
<aside>
💡 Integrate the JavaScript package into your project by using npm, a package manager and dependency management system.

</aside>

```jsx
npm i @tencent/risk-assessment
```

## 2. Get the device result

<aside>
💡 Your Tencent Cloud account's `APP_ID`, `SECRET_ID`, and `SECRET_KEY` are required to retrieve the device result.
</aside>

First, copy the JavaScript code into your project.

```jsx
import RiskAssessment from "@tencent/risk-assessment"

RiskAssessment(APP_ID, SECRET_ID, SECRET_KEY)
  .then((res) => {

    //do something with the res

  })
```

<aside>
💡 There will be a cross-origin problem on the browser, which needs to be solved by installing the `Allow CORS` extension. After downloading it, configure it as shown below:

</aside>

![Untitled](https://user-images.githubusercontent.com/56524120/148018289-07013d7e-8426-494f-8f1a-fb3c91acfd44.png)

After the configuration is completed, the returned data can be obtained on the browser.

**Sample device result response**

```jsx
{
	"Data":{
		"Code":0,
		"Message":"OK",
        	"UUid":"21f71983-6a4c-4b1c-a5a3-4b79a08bacc1",
		"Value":{
		"RiskLevel":"pass",
		"RiskType":null
			}
		},
	"RequestId":"250f67d3-0f14-4955-bc64-5c5b5d2ebc60"
}
```

If the above data is displayed, the call is successful.
