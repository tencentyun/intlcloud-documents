This document introduces the custom capabilities of the eKYC SDK (global edition).

### I. Custom UI

This section describes how to use the custom UI to customize the recognition page and icons.

#### Building bundle

1. Decompress the SDK package, go to the demo directory, and open the HuiYanODemo project.

2. Switch the building scheme to `UserUIBundle`, and run `command+B` to build artifacts.![image-20230110144645956](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20230110144645956.png)

3. After `bundle` is built, right-click it to view the package content. Open `info.plist`, and delete the `Executable file` field. If this field is not deleted, artifacts cannot be published at AppStore, which causes an IPA upload error. You can also directly delete the `info.plist` file.

![image-20221219151658429](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20221219151658429.png)

4. Directly replace `UserUIBundle.bundle` in the root directory (that is, SDK directory) with artifacts, and add all `lib` and `bundle` in this directory to your project. (Note: If the `bundle` content is not modified, you can directly use `bundle` in this directory without replacement.)![image-20230110144900946](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20230110144900946.png)

#### Customizing content

1. Icon: You can replace Icon to the following list, with the name unchanged.

![image-20230110144933817](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20230110144933817.png)

2. xib layout adjustment: For the TXYOsAuthingViewController recognition page, you can modify control layout in xib by adding static components, but not deleting components. The logic of this page is implemented by the internal **.m** file of SDK. You are allowed to modify the layout and add non-logical components only. (For example, add a background image.)

![image-20230110145052550](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20230110145052550.png)

3. You can add settings to SDK by setting the `userUIBundleName` field.

 After this setting, the UI bundle file with custom packaging will be used, and the `TXYOsAuthingViewController` layout file in it will be loaded. 
 If this layout file is not found, the default layout will be loaded.







### II. Custom language

#### Adding a custom language

1. In the Demo, the `UserUIBundle` folder contains `Localizable`. As shown in the following figure, you can set supported languages on the right, and corresponding subfiles are displayed on the left. In the subfiles, multi-language mapping is done for the existing key character strings.

![image-20230215192445766](https://staticintl.cloudcachetci.com/yehe/backend-news/FsTn542_10.png)

2. If there is no target language on the right, you can first add the corresponding language to the project settings, and then repeat step 1.

![image-20230215192602327](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20230215192602327.png)

3. Perform translation mapping on the target file. The following example shows the mapping of simplified Chinese. To add mapping for other languages, keep `key` on the left unchanged and add translation on the right.

![image-20230215192714407](https://staticintl.cloudcachetci.com/yehe/backend-news/C9TH578_12.png)

4. Settings in the SDK are as follows:

```object-c
    customerConfig.userLanguageBundleName = @"UserUIBundle";
    customerConfig.userLanguageFileName = @"en.lproj";
```

`userLanguageFileName` can be used to view the corresponding filename in the compiled `bundle` file.

![image-20230215193116760](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/doc_image/image-20230215193116760.png)



#### Setting a custom SDK language

1. Add the custom `UseLanguage.bundle` to the project (Copy Bundle Resources).



![image_1](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/SDK%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/iOS%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/huiyan/img_10.png)

2. Configure the settings as follows:

```
HuiYanOsConfig *config = [[HuiYanOsConfig alloc] init];
config.languageType = CUSTOMIZE_LANGUAGE; 
config.userLanguageFileName = @"ko";//For example, set `ko.lproj` 
config.userLanguageBundleName = @"UseLanguage";//Custom bundle name, such as `UseLanguage.bundle`
```

If `config.languageType = DEFAULT;` is set, the system will find the language file for the current region in the custom bundle, and if it cannot be found, the language will be `en` by default.



### Maintenance method

Take the Demo project as a custom UI project. Modify the `bundle` source file in the Demo project, and build `bundle` to access your project. You need to maintain the Demo project by yourself.
