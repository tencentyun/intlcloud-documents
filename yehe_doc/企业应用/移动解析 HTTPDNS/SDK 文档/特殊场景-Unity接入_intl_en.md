This document describes how to connect Unity to HTTPDNS.

## Sample Code for Android

Initialize the HTTPDNS and Beacon APIs first:
> ?If you have connected to MSDK or separately connected to Tencent Beacon, you don't need to initialize Beacon.

```
private static AndroidJavaObject m_dnsJo;
private static AndroidJavaClass sGSDKPlatformClass;
public static void Init() {
AndroidJavaClass jc = new AndroidJavaClass("com.unity3d.player.UnityPlayer");
if (jc == null)
return;
AndroidJavaObject joactivety = jc.GetStatic("currentActivity");
if (joactivety == null)
return;
AndroidJavaObject context = joactivety.Call("getApplicationContext");
// Initialize HTTPDNS
AndroidJavaObject joDnsClass = new AndroidJavaObject("com.tencent.msdk.dns.MSDKDnsResolver");
Debug.Log(" WGGetHostByName ===========" + joDnsClass);
if (joDnsClass == null)
return;
m_dnsJo = joDnsClass.CallStatic("getInstance");
Debug.Log(" WGGetHostByName ===========" + m_dnsJo);
if (m_dnsJo == null)
return;
m_dnsJo.Call("init", context);
// Initialize Beacon
AndroidJavaObject joBeaconClass = new AndroidJavaObject("com.tencent.beacon.event.UserAction");
if (joBeaconClass == null)
return;
m_dnsJo.Call("initUserAction", context);
}
```

Then, call the HTTPDNS APIs to resolve the domain:
```
// We recommend you perform this operation in a child thread
public static string GetHttpDnsIP( string strUrl ) {
string strIp = string.Empty;
// Resolve and get the IP configuration set
strIp = m_dnsJo.Call("getAddrByName", strUrl);
Debug.Log( strIp );
if( strIp != null )
{
// Take the first one
string[] strIps = strIp.Split(';');
strIp = strIps[0];
}
return strIp;
}
```

## Sample Code for iOS

Declare the APIs in the CS file:
```
#if UNITY_IOS
[DllImport("__Internal")]
private static extern string WGGetHostByName(string domain);
#endif
```

For the part that requires DNS query, call the `WGGetHostByName(string domain)` method and proceed as follows:
```
string ips = WGGetHostByName(string domain);
string[] sArray=ips.Split(new char[] {';'});
if (sArray != null && sArray.Length > 1) {
	  if (!sArray[1].Equals("0")) {
	      // Suggestion: use an IPv6 address first if it exists
	      // TODO: make a connection by using an IPv6 address. Be sure to enclose the IPv6 address in square brackets, such as `http://[64:ff9b::b6fe:7475]/`
	    } else {
	      // Connect by using the IPv4 address
	    }
}
```

Package the Unity project into an Xcode project and perform operations such as importing dependent libraries as described above.



