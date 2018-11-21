This document explains how Unity can access HttpDNS.

### Code for Android

Initialize HttpDNS and Beacon APIs:
> Note: If you already have accessed MSDK or Tencent Beacon, you don't need to initialize Beacon.

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
// Initialize HttpDNS
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

Then call the HttpDNS API to resolve the domain name:
```
// This operation is recommended to be processed in a child thread
public static string GetHttpDnsIP( string strUrl ) {
string strIp = string.Empty;
// Resolve to get the IP configuration set
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

### Code for iOS

Make an API declaration in the cs file:
```
#if UNITY_IOS
[DllImport("__Internal")]
private static extern string WGGetHostByName(string domain);
#endif
```

In the part where domain name resolution is required, call the WGGetHostByName(string domain) method, and the following processing is recommended:
```
string ips = WGGetHostByName(domainStr);
string[] sArray=ips.Split(new char[] {';'});
if (sArray != null && sArray.Length > 1) {
	  if (!sArray[1].Equals("0")) {
	      // Advice for usage: If the IPv6 address exists, it is used preferentially
	      // When using the IPv6 address for URL connection, pay attention to the format: IPv6 needs to be placed in brackets for processing, for example: http://[64:ff9b::b6fe:7475]/
	    } else {
	      // Use the IPv4 address to connect
	    }
}
```

Package the unity project into an xcode project and follow the instructions above to introduce the dependent libraries and complete other operations.
