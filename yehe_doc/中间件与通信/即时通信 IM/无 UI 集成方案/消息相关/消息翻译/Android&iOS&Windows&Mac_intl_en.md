## Overview
The message translation feature currently supports the translation of text messages only, which can be triggered by manual API calls. Non-text messages such as image, video, file, audio, and custom messages cannot be translated.
> ? This feature is available only in SDK enhanced edition v7.0 or later.

## Translating Text Messages
Call the `translateText` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a1e1806c27bc7b76a3b816492ed9cbe5c) / [iOS & macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#aee0c1e26b0401576ee82967698da35f6) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#ad4df190bf4089a64f69b84a874a60028)) to translate texts.

API parameters are described as follows:

| Input Parameter | Definition                             | Description                                                  |
| --------------- | -------------------------------------- | ------------------------------------------------------------ |
| sourceTextList  | List of text messages to be translated | 1. Multiple text messages can be passed in at a time.<br> 2. UTF-8 encoding is required; otherwise, translation will failed.<br>3. For non-pure texts such as those with HTML tags, the translation may fail.<br>4. The total texts to be translated per request can contain up to 2,000 characters (each Chinese character, letter, punctuation mark, or space is counted as a character). |
| sourceLanguage  | Source language                        | Pass in a specific language or `auto` (automatically identify the source language). If no value is passed in, the default value `auto` will be used. |
| targetLanguage  | Target language                        | Multiple target languages are supported. For more information, see [Supported Text Translation Languages](#languageSupport). |
| callback        | Translation result callback            | In the callback, `key` indicates the text to be translated, and `value` indicates the translated text. |

Sample code:

<dx-tabs>
::: Android
```java
List<String> textList = new ArrayList<>();
textList.add("");
textList.add("");
textList.add("");
String targetLanguage = "en";
V2TIMManager.getMessageManager().translateText(textList, null, targetLanguage, new V2TIMValueCallback<HashMap<String, String>>() {
    @Override
    public void onSuccess(HashMap<String, String> translateHashMap) {
        // Texts translated successfully. `translateHashMap`: {"": "Good morning", "": "Good afternoon", "": "Good evening"}
    }

    @Override
    public void onError(int code, String desc) {
        // Text translation failed
    }
});
```
:::
::: iOS and macOS
```objectivec
NSArray *sourceText = @[@"", @"", @""];
NSString *targetLanguage = @"en";
[[V2TIMManager sharedInstance] translateText:sourceText
                              sourceLanguage:nil
                              targetLanguage:targetLanguage
                                  completion:^(int code, NSString *desc, NSDictionary<NSString *,NSString *> *result) {
    if (code == 0) {
        // Texts translated successfully. `result`: @{@"": @"Good morning", @"": @"Good afternoon", @"": @"Good evening"}
    } else {
        // Text translation failed
    }
}];
```
:::
::: Windows
```cpp
template <class T>
class ValueCallback final : public V2TIMValueCallback<T> {
public:
    using SuccessCallback = std::function<void(const T&)>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;

    ValueCallback() = default;
    ~ValueCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
    }

    void OnSuccess(const T& value) override {
        if (success_callback_) {
            success_callback_(value);
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
};

V2TIMStringVector textList;
textList.PushBack(u8"");
textList.PushBack(u8"");
textList.PushBack(u8"");
V2TIMString targetLanguage = u8"en";

auto callback = new ValueCallback<V2TIMStringToV2TIMStringMap>{};
callback->SetCallback(
    [=](const V2TIMStringToV2TIMStringMap& result) {
        // Texts translated successfully. `result`: {{"", "Good morning"}, {"", "Good afternoon"}, {"", "Good evening"}}
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // Text translation failed
        delete callback;
    });

V2TIMManager::GetInstance()->GetMessageManager()->TranslateText(textList, "", targetLanguage, callback);
```
:::
</dx-tabs>

[](id:languageSupport)
## Supported Text Translation Languages
| Source Language             | Supported Target Language                                    |
| --------------------------- | ------------------------------------------------------------ |
| zh (Simplified Chinese)     | en (English), ja (Japanese), ko (Korean), fr (French), es (Spanish), it (Italian), de (German), tr (Turkish), ru (Russian), pt (Portuguese), vi (Vietnamese), id (Bahasa Indonesian), th (Thai), and ms (Malay) |
| zh-TW (Traditional Chinese) | en (English), ja (Japanese), ko (Korean), fr (French), es (Spanish), it (Italian), de (German), tr (Turkish), ru (Russian), pt (Portuguese), vi (Vietnamese), id (Bahasa Indonesian), th (Thai), and ms (Malay) |
| en (English)                | zh (Simplified Chinese), ja (Japanese), ko (Korean), fr (French), es (Spanish), it (Italian), de (German), tr (Turkish), ru (Russian), pt (Portuguese), vi (Vietnamese), id (Bahasa Indonesian), th (Thai), ms (Malay), ar (Arabic), and hi (Hindi) |
| ja (Japanese)               | zh (Simplified Chinese), en (English), ko (Korean)           |
| ko (Korean)                 | zh (Simplified Chinese), en (English), ja (Japanese)         |
| fr (French)                 | zh (Simplified Chinese), en (English), es (Spanish), it (Italian), de (German), tr (Turkish), ru (Russian), and pt (Portuguese) |
| es (Spanish)                | zh (Simplified Chinese), en (English), fr (French), it (Italian), de (German), tr (Turkish), ru (Russian), and pt (Portuguese) |
| it (Italian)                | zh (Simplified Chinese), en (English), fr (French), es (Spanish), de (German), tr (Turkish), ru (Russian), and pt (Portuguese) |
| de (German)                 | zh (Simplified Chinese), en (English), fr (French), es (Spanish), it (Italian), tr (Turkish), ru (Russian), and pt (Portuguese) |
| tr (Turkish)                | zh (Simplified Chinese), en (English), fr (French), es (Spanish), it (Italian), de (German), ru (Russian), and pt (Portuguese) |
| ru (Russian)                | zh (Simplified Chinese), en (English), fr (French), es (Spanish), it (Italian), de (German), tr (Turkish), and pt (Portuguese) |
| pt (Portuguese)             | zh (Simplified Chinese), en (English), fr (French), es (Spanish), it (Italian), de (German), tr (Turkish), and ru (Russian) |
| vi (Vietnamese)             | zh (Simplified Chinese), en (English)                        |
| id (Bahasa Indonesian)      | zh (Simplified Chinese), en (English)                        |
| th (Thai)                   | zh (Simplified Chinese), en (English)                        |
| ms (Malay)                  | zh (Simplified Chinese), en (English)                        |
| ar (Arabic)                 | en (English)                                                 |
| hi (Hindi)                  | en (English)                                                 |
