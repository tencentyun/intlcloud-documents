
This document describes how to use the watermarking SDK on Android, iOS and Windows.
## SDK Preparation
Download the [demo and SDK](https://main.qcloudimg.com/raw/5066e0eda60b0e00c9e78e0acfa7ec55/%E6%B0%B4%E5%8D%B0SDK.zip).

## Android
### Preparations
- Perform the following steps:
 1. Select a .so file depending on the operating platform. Copy the .so file and .jar file to your project directory, and then add dependencies.
 2. Call the SDK API’s function to generate a watermark.
 3. Add the 20-byte watermark content in front of the message body when sending the message.
- The SDK folder contains the .so file and .jar file, as shown below:
![](https://main.qcloudimg.com/raw/3936cbb5a6ec5a9e21ad75a12f0ad8e4.png)
- SDK API description:
 - Package: com.gamesec
 - Class: Mark
- API description:
<table>
<tbody>
<tr>
<th>API Name</th>
<th>Description</th></tr>
<tr>
<td>CreateSDKBuffFromStr</td>
<td>Creates watermarks</td></tr></tbody></table>

### Directions (Android Studio)
1. Copy all the content in the sdk/android directory to the libs folder in your project directory.
 ![](https://main.qcloudimg.com/raw/0ca7cbe946a4d8eee2b2ca0cd4e3c808.png)
2. Modify the build.gradle file of the project, set the jni directory, and add the jar dependencies as follows:
```
android {
		sourceSets {
				main {
						jniLibs.srcDirs =['libs/jni'] // Set the jni directory
					 }
				   }
			}
		dependencies {
						implementation files('libs/gamesec.jar') // Add the dependencies
				     }
```
3. These instructions also apply to Eclipse, but you do not need to configure the build.gradle file.

### API calling
1. Import the package.
```
import com.gamesec.*;
```
2. Instantiate an object of class Mark.
```
Mark mark = new Mark();
```
3. Call the CreateSDKBuffFromStr API to generate a watermark.
```
byte [ ] CreateSDKBuffFromStr (String pSDKinfo, String buffer, String uDesIp, int uDesPort)
```
 - **Parameter description:**
<table>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Description</th>
</tr>
<tr>
<td>pSDKinfo</td>
<td>String</td>
<td>Watermarked key</td>
</tr>
<tr>
<td>buffer</td>
<td>String</td>
<td>Placeholder parameter. You need to pass in an empty string.</td>
</tr>
<tr>
<td>uDeslp</td>
<td>String</td>
<td>Server IP, such as "1.2.3.4"</td>
</tr>
<tr>
<td>uDesPort</td>
<td>int</td>
<td>Server port</td>
</tr>
</table>
 - **Response:**
<table>
<tr>
<th>Type</th>
<th>Description</th>
</tr>
<tr>
<td>byte[]</td>
<td>Calculated 20-byte watermark content</td>
</tr>
</table>
 - **Sample:**
```
String pSDKinfo = "566c2dea9420eb37-b6c8-566c2dea9420eb3710525135e8485e80806a2f9c";
String uDesIp = "115.159.147.198";
int uDesPort = 8899 ;
byte[] bytes = mark.CreateSDKBuffFromStr(pSDKinfo, "", uDesIp, uDesPort);
```

4. Add the watermark content to the message body as follows:
```
Socket s = new Socket(uDesIp, uDesPort);
OutputStream out = s.getOutputStream();
PrintWriter output = new PrintWriter(out, true);
// Pass in the watermark content first
output.print(bytes); 
output.println("msg msg msg");
BufferedReader input = new BufferedReader(new InputStreamReader(s.getInputStream()));
String msg = input.readLine();
s.close();
```

## iOS
### Preparations
- Perform the following steps:
	1. Copy the SDK folder to your project directory, and add a bridging header file to your Swift project.
	2. Call the SDK API’s function to generate a watermark.
	3. Add the 20-byte watermark content in front of the message body when sending the message.
- The SDK folder contains the .a file and .h file, as shown below:
 ![](https://main.qcloudimg.com/raw/11c1012406344128256a363e593bb2ec.png)
- API description:
<table>
<tbody>
<tr>
<th>API Name</th>
<th>Description</th></tr>
<tr>
<td>CreateSDKBuffFromStr</td>
<td>Creates watermarks</td></tr></tbody></table>

### Directions (Xcode)
1. Copy all the content in the sdk/ios directory to the libs folder in your project directory.
![](https://main.qcloudimg.com/raw/4ab142c35d9d85b6365e9eecce5f66d8.png)
2. To add the SDK folder to your Xcode, right-click the project name and click **Add Files to**.
![](https://main.qcloudimg.com/raw/babb1d9440fc75f8f79eca4efa007dfe.png)
3. On the dialog box, choose **Create folder references**, select the .a file and .h file, and then click **Add**.
![](https://main.qcloudimg.com/raw/bb83314a0468f9cc189bb36268ca2853.png)
4. Click the project name, select **General**, and add the .a file to **Linked Framews and Libraries**.
![](https://main.qcloudimg.com/raw/286f35e15a6e269b62f489fd9c838904.png)
5. Unlike an Object-C project, a Swift project requires a bridging header file. Create a bridging header file named "bridge.h", and add the following code:
			# import "gamesec.h";
6. Click the project name, select **Build Settings**, and add the bridge.h file to **Object-C Bridging Header**.
![](https://main.qcloudimg.com/raw/d5c8dec743f6743fafae2e932c44163f.png)

### API calling
1. For a Swift project, you can directly create a watermark via API calls, while an Object-C project requires a header file.
```
# import "gamesec.h";
```
2. Call the CreateSDKBuffFromStr API to generate a watermark.
```
uint32_t CreateSDKBuffFromStr(char *pSDKinfo, uint8_t *buffer, char* uDstIp, uint16_tuDstPort);
```
**Parameter description:**
<table>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Configuration</th>
</tr>
<tr>
<td>pSDKinfo</td>
<td>char *</td>
<td>Watermarked key</td>
</tr>
<tr>
<td>buffer</td>
<td>uint8_t *</td>
<td>Watermark pointer, which outputs watermark content</td>
</tr>
<tr>
<td>uDeslp</td>
<td>char *</td>
<td>Server IP, such as "1.2.3.4"</td>
</tr>
<tr>
<td>uDesPort</td>
<td>uint16_t</td>
<td>Server port</td>
</tr>
</table>
 
 >!The buffer parameter outputs 20-byte watermark content.
3. Sample:
**Swift:**
```
	let pSDKinfo = UnsafeMutablePointer<Int8>(mutating: (
			"566c2dea9420eb37-b6c8-566c2dea9420eb3710525135e8485e80806a2f9c" 
			as NSString).utf8String);
					var buffer = UnsafeMutablePointer<UInt8>.allocate(capacity: 20);
			let uDstIp = UnsafeMutablePointer<Int8>(mutating: (
			"115.159.147.198" as NSString).utf8String);
					let uDstport = UInt16.init("8899")!;

			CreateSDKBuffFromStr(pSDKinfo, buffer, uDstIp, uDstport);

					for i in 0 ..< 20 {
							let b = (buffer+i).pointee;
							// The watermark content is stored in the first 20 bytes of the output. The output type is uint8.
							print(" \(b)");
					}
**Object-C:** 

			char *pSDKinfo = "566c2dea9420eb37-b6c8-566c2dea9420eb3710525135e8485e80806a2f9c";
					uint8_t buffer[20];
					char *uDstIp = "115.159.147.198";
					uint16_t uDstPort = 8899;

					CreateSDKBuffFromStr(pSDKinfo, buffer, uDstIp, uDstPort);

					for(int i=0;i<20;i++)
			{
					// The watermark content is stored in the first 20 bytes of the output
							NSLog(@"%d", (int8_t)buffer[i]); 
			}
```
4. Add the 20-byte watermark content in front of the message body when sending the message.

## Windows
### Preparations
Download the gamesec.dll file which contains a function to create watermarks.
```
uint32_t CreateSDKBuffFromStr(char *pSDKinfo, uint8_t *buffer, char* uDstIp, uint16_t uDstPort);
```
**Parameter description:**
<table>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Description</th>
</tr>
<tr>
<td>pSDKinfo</td>
<td>char *</td>
<td>Watermarked key</td>
</tr>
<tr>
<td>buffer</td>
<td>uint8_t *</td>
<td>Watermark pointer, which outputs watermark content</td>
</tr>
<tr>
<td>uDeslp</td>
<td>char *</td>
<td>Server IP, such as "1.2.3.4"</td>
</tr>
<tr>
<td>uDesPort</td>
<td>uint16_t</td>
<td>Server port</td>
</tr>
</table>

 >!The watermark content is stored in the first 20 bytes of the buffer output.


### API calling
To call the watermark function, import the .dll file using the LoadLibrary function (you need to add Windows.h):
```
 // Define the function pointer
    typedef int(*FUNC)(char *, uint8_t *, char* , uint16_t );
    // Set the .dll path
    HINSTANCE Hint = ::LoadLibrary(L"E:\\sdk\\gamesec.dll");
    FUNC CreateSDKBuffFromStr = (FUNC)GetProcAddress(Hint, "CreateSDKBuffFromStr");
```
Sample:
```
 // Save the watermark
    uint8_t buffer[BUFFER_SIZE];
    memset(buffer, 0, BUFFER_SIZE);
    
    int UDP_TEST_PORT = 8899;
    
    const char * CONST_UDP_SERVER_IP  = "115.159.147.198";
    char * UDP_SERVER_IP = new char[strlen(CONST_UDP_SERVER_IP)];
    strcpy(UDP_SERVER_IP, CONST_UDP_SERVER_IP);
    
    const char * CONST_pSDKinfo = 
    "566c2dea9420eb37-b6c8-566c2dea9420eb3710525135e8485e80806a2f9c";
    char * pSDKinfo = new char[strlen(CONST_pSDKinfo)];
    strcpy(pSDKinfo, CONST_pSDKinfo);
    
    // Make 10 API calls
    for (int i = 0; i < 5; i++) {
    CreateSDKBuffFromStr(pSDKinfo, buffer, (char *)UDP_SERVER_IP, UDP_TEST_PORT);
    
    for (int i = 0; i <= 20; i++)
    {
    // The watermark content is stored in the first 20 bytes of the output
    printf("%d ", (int8_t)buffer[i]);
    }
    printf("\n\n");
    }
```
