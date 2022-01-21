## Web

为您的 Web 应用程序提供了一个 JavaScript 包。开始集成有两个步骤：

## 1.集成 JavaScript
<aside>
💡 使用 npm、包管理器和依赖项管理系统将 JavaScript 包集成到您的项目中。

</aside>

```jsx
npm i @tencent/risk-assessment
```

## 2.获取设备结果

<aside>
💡 需要您的腾讯云账号的 APP_ID, SECRET_ID，SECRET_KEY来检索设备结果
</aside>

首先，将 JavaScript 代码片段复制到您的项目中。

```jsx
import RiskAssessment from "@tencent/risk-assessment"

RiskAssessment(APP_ID, SECRET_ID, SECRET_KEY)
  .then((res) => {

    //do something with the res

  })
```

<aside>
💡 在浏览器端会有跨域问题，所有需要您安装谷歌插件 Allow CORS来解决。下载好 Allow CORS后，需要设置如下图的配置

</aside>

![Untitled](https://user-images.githubusercontent.com/56524120/148018289-07013d7e-8426-494f-8f1a-fb3c91acfd44.png)

配置好后，就可以在浏览器端获取到返回的数据了。

**示例设备结果响应**

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

若显示以上数据的话，恭喜您调用成功。
