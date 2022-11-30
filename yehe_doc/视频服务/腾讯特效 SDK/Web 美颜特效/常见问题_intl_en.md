This document answers questions you may encounter when using the Tencent Effect web SDK.

[](id:q1)
### What should I do if the video is flipped and stutters when I run a demo project with Chrome?
The SDK uses GPU acceleration. You need to enable **hardware acceleration** in your browser settings.

[](id:q2)
### I have a web streaming application. Can I use the Tencent Effect web SDK to beautify the images published by the application?
Yes, you can use the SDK as a render. It supports different input and output types.

[](id:q3)
### Will my signature service be called too frequently?
No. The SDK has a signature caching mechanism. You can also design your own response logic for `getSignature`. Just make sure it complies with the rules of method signatures.

[](id:q4)
### Will the custom effects I created in the console be different from the actual effects applied by the SDK?
No. The actual rendering effects delivered by the SDK are the same as when you preview them in the console.

[](id:q5)
### The example in “Running a Demo Project” uses `localhost:8090` to run a project locally. Can I use a different localhost port?

Yes, you can. On the web license management page of the console, set the domain of your license to the domain and port you want to use, and in the `package.json` file, modify the port number of the `dev` command.
For example, if you want to use `localhost:9999` to run a demo project, set the domain to `localhost:9999`.

[](id:q6)
### Low-latency publishing failed. When I opened the browser console, the message “streamurl authentication failed” was shown. What should I do?
This is usually because the signature expired. Please generate a new signature for publishing. For details about the format of publishing URLs, see [Splicing Live Streaming URLs](https://intl.cloud.tencent.com/document/product/267/38393).

[](id:q7)
### An error occurred when I called `getEffectList` to query effects. What should I do?
This is likely because you didn’t call the API at the right time. **`getEffectList` must be called after the `created` callback**.

[](id:q8)
### I used the built-in camera mode of the SDK on my webpage. When I previewed effects, echoes could be heard. What should I do?
If you enable audio and use the speaker when previewing effects, the audio played by the speaker will be captured by the built-in camera, which causes echoes. To solve this, disable audio when you preview effects.
```
const output = await sdk.getOutput()
const video = document.createElement('video')
document.body.appendChild(video)

video.setAttribute('muted', '')
video.volume = 0
video.srcObject = output
```

[](id:q9)
### Authentication failed, and the code 401 was returned. What should I do?
The SDK uses `getSignature`, with pass-through parameters, to request a signature and authenticates the signature with the backend. If a signature has expired, it will try again. If authentication fails again, it will throw an error and ban all subsequent operations. Check your `getSignature` logic. Make sure your signature has not expired (valid for five minutes) and the correct signature generation logic is used.