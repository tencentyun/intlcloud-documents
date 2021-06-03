You can generate UserSig online in the TRTC console, but it should be used only for quick testing at the development stage. For official launch, please [calculate UserSig on the server](https://intl.cloud.tencent.com/document/product/647/35166). This avoids key leakage and prevents attackers from stealing your traffic.


[](id:generate)
## Signature (UserSig) Generator
Signatures (UserSig) allow you to build trust with Tencent Cloud.

1. Log in to the TRTC console and select **Development Assistance** > **[UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool)**.
2. In **Signature (UserSig) Generator**, select the application (`SDKAppID`) you created from the drop-down list. A secret key (`key`) is generated automatically.
3. Enter the user name (`UserID`).
4. Click **Generate Signature (UserSig)** to generate your UserSig.
![](https://main.qcloudimg.com/raw/1beace0cb76655168f4b0b9f06eb65e4.png)


[](id:check)
## Signature (UserSig) Checker
This is used to check the validity of your signature (UserSig).

>! Make sure that you enter the correct SDKAppID and UserID for the UserSig you want to verify.

1. Log in to the TRTC console and select **Development Assistance** > **[UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool)**.
2. In **Signature (UserSig) Checker**, select the application (`SDKAppID`) whose signature you want to verify. A secret key is generated automatically.
3. Enter the user name (`UserID`).
4. Copy and paste the signature (UserSig) that needs verification to **Signature (UserSig)**, and click **Verify Now**.
>? If your UserSig is generated in **Signature (UserSig) Generator**, click **Copy Signature (UserSig)** to copy the signature.
>
![](https://main.qcloudimg.com/raw/d8ee8b9c6d1d20ae325ec61964e788d9.png)
5. View the verification results.
	- Example of successful verification:
	![](https://main.qcloudimg.com/raw/bd68863171529bd72a6bf20cbe628582.png)
	- Example of failed verification:
	![](https://main.qcloudimg.com/raw/0b32a98cad31330a56e5b2f3fa4e282c.png)


## Reference
For more information about UserSig, see [FAQs (UserSig)](https://intl.cloud.tencent.com/document/product/647/35166).
