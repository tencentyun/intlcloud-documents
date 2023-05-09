This document introduces the custom capabilities of the FaceID SDK (global edition).

### I. Custom UI

#### Customizing layout

The FaceID SDK supports custom UI by using `AuthUiConfig` (see the API description document) or passing in `Layout resId`.

The usage is as follows:

```java
AuthUiConfig authConfig = new AuthUiConfig();
authUiConfig.setAuthLayoutResId(R.layout.demo_huiyan_fragment_authing);
authUiConfig.setAuthCircleCorrectColor(resources.getColor(R.color.demo_blue));
huiYanOsConfig.setAuthUiConfig(authUiConfig);
```

The following figure shows the default layout:

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/Private_Dome/v1.0.9/Android/clipboard_20220120_072359.png)

The default layout is as shown above, where the positions of all controls can be adjusted by modifying the `Layout.xml` file. For more information, see the demo's `demo_huiyan_fragment_authing.xml` file.

 

>!
>
> The `View type` and the corresponding `android:id` in `demo_huiyan_fragment_authing.xml` are involved in UI event binding, so **do not modify them**.

The default layout provided here is as follows:

```xml
<?xml version="1.0" encoding="utf-8"?>
<com.tencent.could.huiyansdk.view.HuiYanReflectLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/txy_auth_layout_bg"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <!-- Cancel button -->
    <TextView
        android:id="@+id/txy_cancel_txt_btn"
        android:text="@string/txy_cancel"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:textColor="@color/txy_black"
        android:textSize="16sp"
        android:layout_marginTop="@dimen/txy_title_margin_top"
        android:layout_marginStart="@dimen/txy_protocol_margin_size"
        />

    <!-- Countdown display control -->
    <TextView
        android:id="@+id/txy_count_down_txt_view"
        android:text="@string/txy_count_down_txt"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:textSize="16sp"
        android:textColor="@color/txy_black"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="@dimen/txy_title_margin_top"
        android:layout_marginRight="@dimen/txy_protocol_margin_size"
        android:visibility="gone"
        />

    <!-- Camera preview frame (if it is 720p, the height in the code will be automatically multiplied by 1.3)  -->
    <com.tencent.could.huiyansdk.view.CameraDateGatherView
        android:id="@+id/txy_camera_gather_view"
        android:layout_width="@dimen/txy_auth_head_size"
        android:layout_height="258dp"
        android:background="@android:color/transparent"
        android:layout_marginBottom="@dimen/txy_auth_view_move"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <!-- General background, which is a ring with vertical lines -->
    <com.tencent.could.huiyansdk.view.CommonAuthBackView
        android:id="@+id/txy_auth_common_background_views"
        android:layout_width="230dp"
        android:layout_height="230dp"
        android:layout_marginBottom="@dimen/txy_auth_view_move"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        />

    <!-- Profile photo to display -->
    <ImageView
        android:id="@+id/txy_camera_prepare_img"
        app:srcCompat="@drawable/txy_prepare_face_head_white"
        android:layout_width="@dimen/txy_auth_head_size"
        android:layout_height="@dimen/txy_auth_head_size"
        android:layout_marginBottom="@dimen/txy_auth_view_move"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent" />

    <!-- Frontend animation view -->
    <com.tencent.could.huiyansdk.view.LoadingFrontAnimatorView
        android:id="@+id/txy_auth_loading_front_animator_view"
        android:visibility="gone"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginBottom="@dimen/txy_auth_view_move"
        android:layout_width="@dimen/txy_auth_head_size"
        android:layout_height="@dimen/txy_auth_head_size"
        />

    <!--  Prompt display page  -->
    <TextView
        android:id="@+id/txy_auth_feed_back_txt"
        app:layout_constraintTop_toBottomOf="@id/txy_auth_common_background_views"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:textColor="@color/txy_black"
        android:layout_marginTop="@dimen/txy_protocol_line_space"
        android:text="@string/txy_face_preparing3"
        android:textSize="18sp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

    <!--  Prompt control for additional warning message  -->
    <TextView
        android:id="@+id/txy_auth_feed_back_extra_tip_txt"
        android:textSize="14sp"
        android:textColor="@color/txy_black"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center_horizontal"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_marginTop="20dp"
        app:layout_constraintTop_toBottomOf="@id/txy_auth_feed_back_txt"
        />

    <!--  Content prompt for liveness detection and face comparison -->
    <TextView
        android:id="@+id/txy_auth_tips_txt"
        android:textSize="14sp"
        android:textColor="@color/txy_black"
        android:paddingHorizontal="25dp"
        android:layout_marginHorizontal="25dp"
        android:layout_marginBottom="35dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

</com.tencent.could.huiyansdk.view.HuiYanReflectLayout>
```



#### Binding events for custom layout

The previous section describes how to customize the UI layout. This section describes how to bind events to the controls added to the custom UI layout to meet your specific needs.

When the liveness detection and face comparison UI is created, `onMainViewCreate(View authView)` of `HuiYanAuthEventCallBack` will be called. When the liveness detection and face comparison UI is to be terminated, the `onMainViewDestroy()` method will be called back, and you can customize the processing logic in the corresponding lifecycle.

```java
// Set a callback listener for key events in FaceID
HuiYanOsApi.setAuthEventCallBack(new HuiYanAuthEventCallBack() {
    @Override
    public void onAuthTipsEvent(HuiYanAuthTipsEvent tipsEvent) {
        Log.e(TAG, "current is : " + tipsEvent);
    }

    @Override
    public void onMainViewCreate(View authView) {
        if (authView == null) {
            return;
        }
        // Get the added controls and register custom events
        Button findBtn = authView.findViewById(R.id.add_view_offer_button);
        if (findBtn != null) {
            findBtn.setOnClickListener(view -> {
                Log.e(TAG, "click test button!");
            });
        }
    }

    @Override
    public void onMainViewDestroy() {
        Log.e(TAG, "onMainViewDestroy");
    }
});
```

Based on the callback of `onMainViewCreate` and the callback method of `onMainViewDestroy`, you can bind events to the added UI controls to achieve the desired effect.



### II. Custom Prompt and Language

#### Customizing prompt

If you want to modify a prompt or add a language file, follow the instructions below. The FaceID SDK provides a translation file **hy_customer_string.xml** , which contains all the configuration text that can be modified.

1. Open the project in the main module (which integrates the FaceID SDK).
2. Add the **hy_customer_string.xml** file to the corresponding language folder.
3. Modify the text content that needs to be customized.
4. After being packaged, the modified content will automatically overwrite the original content.

![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/%E8%87%AA%E5%AE%9A%E4%B9%89%E6%8F%90%E7%A4%BA%E8%AF%AD.png)



#### Adding a language

To add a language, perform the following steps:

1. Add the corresponding language folder to the project in the main module (which integrates the FaceID SDK).

2. Copy the `hy_customer_string.xml` file to the language folder and modify the value content.

   ![](https://ai-sdk-release-1254418846.cos.ap-guangzhou.myqcloud.com/huiyan/image/%E6%96%B0%E5%A2%9E%E8%AF%AD%E8%A8%80.png)

3. Specify the target language code in the code (with Thai as an example).

```java
huiYanOsConfig.setLanguageStyle(LanguageStyle.CUSTOMIZE_LANGUAGE);
huiYanOsConfig.setLanguageCode("th-TH");
```


#### Language codes for Android

Some language codes for Android are provided for reference.

| Language Code     | Language - Country/Region       |
| ---------- | -------------------------- |
| **af-ZA**  | **Afrikaans - South Africa**      |
| **sq-AL**  | **Albanian - Albania** |
| **ar-DZ**  | **Arabic - Algeria**   |
| **ar-BH**  | **Arabic - Bahrain**         |
| **ar-EG**  | **Arabic - Egypt**         |
| **ar-IQ**  | **Arabic - Iraq**       |
| **ar-JO**  | **Arabic - Jordan**         |
| **ar-KW**  | **Arabic - Kuwait**       |
| **ar-LB**  | **Arabic - Lebanon**       |
| **ar-LY**  | **Arabic - Libya**       |
| **ar-MA**  | **Arabic - Morocco**       |
| **ar-OM**  | **Arabic - Oman**         |
| **ar-QA**  | **Arabic - Qatar**       |
| **eu-ES**  | **Basque - Basque**         |
| **be-BY**  | **Belarusian - Belarus**    |
| **bg-BG**  | **Bulgarian - Bulgaria**     |
| **ca-ES**  | **Catalan - Catalonia** |
| **zh-HK**  | **Chinese - Hong Kong (China)**        |
| **zh-MO**  | **Chinese - Macao (China)**        |
| **zh-CN**  | **Chinese - China**             |
| **zh-SG**  | **Chinese - Singapore**           |
| **zh-TW**  | **Chinese - Taiwan (China)**        |
| **zh-CHS** | **Simplified Chinese**          |
| **zh-CHT** | **Traditional Chinese**          |
| **hr-HR**  | **Croatian - Croatia** |
| **cs-CZ**  | **Czech - Czech Republic**            |
| **da-DK**  | **Danish - Denmark**           |
| **div-MV** | **Dhivehi - Maldives**       |
| **nl-BE**  | **Dutch - Belgium**           |
| **nl-NL**  | **Dutch - Netherlands**            |
| **en-AU**  | **English - Australia**             |
| **en-CA**  | **English - Canada**           |
| **en-ZA**  | **English - South Africa**            |
| **en-PH**  | **English - Philippines**     |
| **en-NZ**  | **English - New Zealand**          |
| **en-GB**  | **English - UK**            |
| **en-US**  | **English - US**            |
| **fa-IR**  | **Persian - Iran**       |
| **fi-FI**  | **Finnish - Finland**           |
| **fr-FR**  | **French - France**             |
| **fr-BE**  | **French - Belgium**           |
| **fr-MC**  | **French - Monaco**           |
| **fr-CH**  | **French - Switzerland**             |
| **gl-ES**  | **Galician - Galicia**     |
| **ka-GE**  | **Georgian - Georgia** |
| **de-DE**  | **German - Germany**             |
| **de-LU**  | **German - Luxembourg**           |
| **de-CH**  | **German - Switzerland**             |
| **el-GR**  | **Greek - Greece**             |
| **gu-IN**  | **Gujarati - India**          |
| **he-IL**  | **Hebrew - Israel**         |
| **hi-IN**  | **Hindi - India**         |
| **hu-HU**  | **Hungarian - Hungary**       |
| **is-IS**  | **Icelandic - Iceland**           |
| **it-IT**  | **Italian - Italy**         |
| **ja-JP**  | **Japanese - Japan**             |
| **kk-KZ**  | **Kazakh - Kazakhstan**          |
| **kn-IN**  | **Kannada - India**         |
| **ko-KR**  | **Korean - South Korea**             |
| **lv-LV**  | **Latvian - Latvia**   |
| **lt-LT**  | **Lithuanian - Lithuania**         |
| **ms-BN**  | **Malay - Brunei**             |
| **ms-MY**  | **Malay - Malaysia**         |
| **mr-IN**  | **Marathi - India**         |
| **mn-MN**  | **Mongolian - Mongolia**             |
| **nn-NO**  | **Nynorsk - Norway**   |
| **pl-PL**  | **Polish - Poland**             |
| **pt-BR**  | **Portuguese - Brazil**           |
| **pt-PT**  | **Portuguese - Portugal**         |
| **ro-RO**  | **Romanian - Romania**   |
| **sa-IN**  | **Sanskrit - India**             |
| **ru-RU**  | **Russian - Russia**             |
| **sk-SK**  | **Slovak - Slovakia**     |
| **es-AR**  | **Spanish - Argentina**         |
| **es-ES**  | **Spanish - Spain**         |
| **sv-SE**  | **Swedish - Sweden**             |
| **th-TH**  | **Thai - Thailand**             |
| **tr-TR**  | **Turkish - Türkiye**       |
| **uk-UA**  | **Ukrainian - Ukraine**         |
| **ur-PK**  | **Urdu - Pakistan**          |
| **vi-VN**  | **Vietnamese - Vietnam**             |
