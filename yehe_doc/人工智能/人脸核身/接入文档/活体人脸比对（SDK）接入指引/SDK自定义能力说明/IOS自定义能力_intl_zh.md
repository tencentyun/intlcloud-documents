本文主要介绍海外版慧眼SDK当前所具备的自定义的能力

### 一、自定义UI

本文主要介绍如何使用自定义UI，定制慧眼识别页面以及图标。

#### 构建步骤

1、SDK压缩包解压后，进入demo目录，打开HuiYanODemo项目。

2、切换构建secheme到UserUIBundle，command+B可以构建出产物。![image-20230110144645956](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20230110144645956.png)

3、构建出bundle后右键查看包内容，打开info.plist，删掉“Executable file”字段，否则会影响AppStore上架，导致上传IPA报错。也可以将info.plist文件删掉。

![image-20221219151658429](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20221219151658429.png)

4、将构建产物直接替换掉根目录SDK目录下的UserUIBundle.bundle，将该目录下所有lib和bundle添加到自己的项目中（注：若没有修改bundle内容，可不进行替换，直接使用该目录下的bundle即可）。![image-20230110144900946](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20230110144900946.png)

#### 自定义内容

1）图标Icon。可以将Icon替换到以下列表，命名要保持原有命名。

![image-20230110144933817](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20230110144933817.png)

2）xib内布局调整。如TXYOsAuthingViewController 识别页面，可以修改xib内组件的布局，增加静态组件，但是不允许删除组件。该页面逻辑由SDK内部.m文件完成，仅支持修改布局和增加无逻辑组件（如增加背景图）。

![image-20230110145052550](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20230110145052550.png)

3）通过设置userUIBundleName字段设置到SDK中

 这个设置了会使用自定义打包的UI bundle 文件，会加载里面这个名称的TXYOsAuthingViewController布局文件
 若是未找到TXYOsAuthingViewController 名称的布局文件，将会加载默认布局。




### 二、自定义语言

#### 添加自定义语言

1）demo中UserUIBundle文件夹中包含Localizable。下图中右侧可设置支持的语言类型，对应左侧会出现子文件，在子文件中对已有的key字符串做多语言映射。

![image-20230215192445766](https://staticintl.cloudcachetci.com/yehe/backend-news/FsTn542_10.png)

2）若右侧没有目标语言可先对工程设置里添加对应语言，之后重复步骤1即可

![image-20230215192602327](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20230215192602327.png)

3）对目标文件进行翻译映射。下图示例为简体中文的映射，若添加其他语言左侧key保持不变，右侧为译文即可。

![image-20230215192714407](https://staticintl.cloudcachetci.com/yehe/backend-news/C9TH578_12.png)

4）SDK中设置为

```object-c
    customerConfig.userLanguageBundleName = @"UserUIBundle";
    customerConfig.userLanguageFileName = @"en.lproj";
```

userLanguageFileName可以查看编译出的bundle文件中对应的文件名

![image-20230215193116760](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20230215193116760.png)



#### 设置自定义SDK语言

1、将自定义UseLanguage.bundle添加至项目中(Copy Bundle Resources)



![image_1](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/SDK%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/iOS%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/huiyan/img_10.png)

2、配置设置如下

```
HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
config.languageType = CUSTOMIZE_LANGUAGE; 
config.userLanguageFileName = @"ko";//例：设置 ko.lproj 
config.userLanguageBundleName = @"UseLanguage";//自定义打包bundle名称 例： UseLanguage.bundle
```

若config.languageType = DEFAULT;则会从自定义Bundle找该地区的语言文件，若是未找到则默认为en。



### 维护方式

1、将Demo工程作为自定义UI的工程，通过修改Demo工程里的bundle源文件，然后构建bundle接入自己项目。缺点需要自行维护Demo工程。
