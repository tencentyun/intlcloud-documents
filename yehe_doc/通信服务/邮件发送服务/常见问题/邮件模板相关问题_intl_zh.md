## 邮件模板相关问题
#### 如何发送高度定制化的模板邮件？
腾讯云 DMS 中的模板功能基于 Handlebars 模板系统。除了直接使用简单的表达式之外，您还可以使用 Handlebars 创建包含高级功能 (如嵌套属性、数组迭代、基本条件语句以及创建内联部分) 的模板。本部分提供有关这些功能的一些示例。

除本部分介绍的功能以外，Handlebars 还包含许多其他功能。有关更多信息，请参阅  [handlebarsjs.com](http://handlebarsjs.com/)

1. **嵌套输入对象**
	输入对象可以包含其他对象或数组。例如：

		{
			person: {
				firstname: "Yehuda",
			    lastname: "Katz",
				},
		}

	在邮件模板中，您可以通过以下方式引用嵌套属性：提供父属性名称，后跟句点 `.`，然后是要包含其值的属性的名称。例如，对于上例中显示的数据结构，要在电子邮件模板中包含收件人全名:
	
		{{person.firstname}} {{person.lastname}}
	
	发送电子邮件时，输出结果为：
	Yehuda Katz

	Handlebars 能够解析多层嵌套路径，这意味着您可以灵活地组织模板数据结构。

2. **遍历列表**
	`each` 帮助程序函数可遍历数组中的项目，例如对于一个用户的许多兴趣：

		{
			interests: [
				"football",
				"swimming",
				"reading",
			],
		}

	`each` 助手代码会迭代一个数组，使你可以通过 Handlebars 简单访问每个对象的属性表达式。

		{{#each interests}}
			{{this}}
		{{/each}} 

	发送电子邮件时，输出结果为：
	- football
	- swimming
	- reading

3. **基本的条件语句**
	你可以使用 `if` 助手代码来根据条件渲染代码块。如果其参数返回 `false`、`undefined`、`null`、`""`、 `0` 或者 `[]`，Handlebars 将不会渲染该块。

	例如，输入对象中有一个判断其是否是作者的参数 `author`：

		{
			author: true,
			firstName: "Yehuda",
			lastName: "Katz",
		}

	通过`if` 助手代码判断，仅在收件人是作者的情况下显示其全名：

		{{#if author}}
			{{firstName}} {{lastName}}
		{{/if}}

	发送电子邮件时，输出结果为：
		Yehuda Katz
		
#### 模板自定义值的格式要求？
发送模板邮件时，需要上传一个 JSON 格式的文件以指明替换模板中自定义变量的值。本部分提供有关该 JSON 文件的相关说明。

JSON 文件的格式如下：

	{
		"Destinations":[
			{
				"Destination":{
					ToAddresses":[
					"address1@example.com"
					]	
				},
				"ReplacementTemplateData": "{ Handlebars input 1 }"
			},
			{
				"Destination":{
					ToAddresses":[
					"address2@example.com",
					"address3@example.com"
					]	
				},
				"ReplacementTemplateData": "{ Handlebars input 2 }"
			}
		],
		"DefaultTemplateData": "{ Handlebars input 3 }"
	}

此代码包含以下属性：
-   Destinations  – 包含一个或多个目标的数组。
        -   Destination  – 收件人地址。您可以包含多个“收件人”、“抄送”和“密件抄送”地址。
        -   ReplacementTemplateData  – 包含键-值对的 JSON 对象。键与模板中的变量 (例如  `{{name}}`) 对应。值表示用来替换电子邮件中的变量的内容。
            
 -   DefaultTemplateData  – 包含键-值对的 JSON 对象。键与模板中的变量 (例如  `{{name}}`) 对应。值表示用来替换电子邮件中的变量的内容。此对象将替换未在 Destinations 中指明的收件地址收到的邮件内容。

使用以上 JSON 文件发信，address1@example.com 将会收到 Handlebars input 1 替换邮件模板生成的邮件，address2@example.com 和 address3@example.com 将会收到 Handlebars input 2 替换邮件模板生成的邮件，其他收件地址将会收到 Handlebars input 3 替换邮件模板生成的邮件。

例如，针对编辑好的邮件模板：
~~~
Hi {{prefix}} {{lname}} {{fname}},

Thank you for choosing Tencent Cloud DMS.

Best regards,
Tencent Cloud Team
~~~
可使用以下 JSON 文件替换模板自定义值：

	{
	  "Destinations": [
	    {
	      "Destination": {
	        "ToAddresses": [
	          "tomlee@example.com"
	        ]
	      },
	      "ReplacementTemplateData": "{ \"fname\":\"Tom\", \"lname\":\"Lee\", \"prefix\":\"Mr.\" }"
	    },
	    {
	      "Destination": {
	        "ToAddresses": [
	          "micheal@example.com"
	        ]
	      },
	      "ReplacementTemplateData": "{ \"fname\":\"Micheal\", \"prefix\":\"Mr.\" }"
	    },
	    {
	      "Destination": {
	        "ToAddresses": [
	          "tina@example.com"
	        ]
	      },
	      "ReplacementTemplateData": "{ \"fname\":\"Tina\", \"lname\":\"chan\", \"prefix\":\"Ms.\" }"
	    },
	    {
	      "Destination": {
	        "ToAddresses": [
	          "richard.roe@example.com",
	          "richard.work@example.com"
	        ]
	      },
	      "ReplacementTemplateData": "{ \"fname\":\"Richard\""
	    }
	  ],
	  "DefaultTemplateData": "{ \"fname\":\"Friend\", \"lname\":\"Sweety\", \"prefix\":\"\"}"
	}


#### 删除邮件模板后能否恢复？
邮件模板删除后无法恢复。

删除邮件模板将会导致您无法再使用该模板发送模板邮件，建议将所有邮件模板在您的主机上进行备份。

另外，编辑邮件模板名称可能导致您在 【重发】 模板邮件任务时需要重新选择 【邮件模板】。