- ## Foreword
  This article is based on the [Tencent Cloud AV Chat Room](https://pub.dev/packages/tencent_cloud_av_chat_room) plug-in, combined with the [Live Flutter SDK](https://www.tencentcloud.com/document/product/1071/50587 ) Realized live broadcast business scenario.

  ## Tencent Cloud AV Chat Room

  `Tencent Cloud AV Chat Room` is a UI component based on [Tencent Cloud Chat SDK](https://pub.dev/packages/tencent_cloud_chat_sdk) and implemented around chat interaction scenarios.

  You can use this component to quickly implement an application with **tens of millions of interactions**.

  <p align="center">
      <img src="https://qcloudimg.tencent-cloud.cn/raw/609ef69a95153a435e8c57e8d72530fd.jpg">
  </p>
  

  [](id:msg)
  ## Introduction

  ### Preconditions

  - Have [registered](https://www.tencentcloud.com/zh/document/product/378/17985) Tencent Cloud account and completed [identity verification](https://www.tencentcloud.com/zh/document/ product/378/3629).
  - Create an application by referring to [Create and upgrade an application](https://www.tencentcloud.com/zh/document/product/1047/34577), and record `SDKAppID`.
  - Select your application in [IM Console](https://console.tencentcloud.com/im), click Accessibility Tools -> UserSig Generation & Verification in the left navigation bar, and create a UserID and its corresponding `UserSig `, copy the three `UserID`, `Signature (Key)`, `UserSig`, which will be used in subsequent logins.
  - Create a Flutter app.
  - Add tencent_cloud_av_chat_room in the pubspec.yaml file under dependencies. Or execute the following command:

  ```
  /// step 1:
  flutter pub add tencent_cloud_av_chat_room
  
  /// step 2:
  flutter pub get
  ```

  ### Step 1: Initialize and login to IM

  There are two ways to initialize and log in to IM:

  - **External component**: The entire application is initialized and logged in only once.
  - **Inside the component**: pass parameters into the component through configuration.
    If you are integrating this plugin in an existing IM flutter project, you can skip this step.

  ##### Outside the component (recommended)

  Initialize IM in the flutter app you created, note that the IM app only needs to be initialized once. This step can be skipped if integrating in an existing IM project.

  ```dart
  import 'package:tencent_av_chat_room_kit/tencent_cloud_chat_sdk_type.dart';
  
  class _MyHomePageState extends State<MyHomePage> {
  	 final int _sdkAppID = 0; // SDKAppID of the IM application created in the preconditions
  	 final String _loginUserID = ""; // UserID in precondition
  	 final String _userSig = ""; // UserSig in preconditions
  	@override
  	void initState() {
  		super.initState();
  		_initAndLoginIm();
  	  }
  
  	_initAndLoginIm() async {
  		await TencentImSDKPlugin.v2TIMManager.initSDK(
  			sdkAppID: _sdkAppID,
  			loglevel: LogLevelEnum.V2TIM_LOG_ALL,
  			listener: V2TimSDKListener());
  		TencentImSDKPlugin.v2TIMManager
            .login(userID: _loginUserID, userSig: _userSig);
  	}
  }
  ```

  ##### Inside the component

  You can also pass `SDKAppID`, `UserSig`, `UserID` into the component through configuration to initialize and log in IM.

  ```dart
  import 'package:tencent_cloud_av_chat_room/tencent_cloud_av_chat_room.dart';
  
  class _TencentAVChatRoomKitState extends State<TencentCloudAVChatRoom> {
  	final int _sdkAppID = 0; // SDKAppID of the IM application created in the preconditions
  	final String _loginUserID = ""; // UserID in precondition
  	final String _userSig = ""; // UserSig in preconditions
  	@override
    	Widget build(BuildContext context) {
  		return TencentCloudAVChatRoom(
  			config: TencentCloudAvChatRoomConfig(
  				loginUserID: _loginUserID, sdkAppID: _sdkAppID, userSig: _userSig));
  	}
  }
  ```

  ### Step 2: Using Components

  Use that component in your appropriate module.

  ```dart
  import 'package:tencent_cloud_av_chat_room/tencent_cloud_av_chat_room.dart';
  
  class _TencentAVChatRoomKitState extends State<TencentCloudAVChatRoom> {
  	final int _sdkAppID = 0; // SDKAppID of the IM application created in the preconditions
  	final String _loginUserID = ""; // UserID in precondition
  	final String _userSig = ""; // UserSig in preconditions
  	@override
    	Widget build(BuildContext context) {
  		return TencentCloudAVChatRoom(
  			data: TencentCloudAvChatRoomData(anchorInfo: AnchorInfo()),
  			config: TencentCloudAvChatRoomConfig(
  				loginUserID: _loginUserID, sdkAppID: _sdkAppID, userSig: _userSig, avChatRoomID: ''));
  	}
  }
  ```

  ## Cooperate with Tencent Cloud View Cube to build a live broadcast room

  Live streaming is ubiquitous in life, and more and more companies and developers are building their own live streaming platforms. The following will introduce how to build a live broadcast room with Tencent Cloud View Cube.
  The live broadcast room mainly includes two parts: live broadcast and interaction. In the live broadcast part, we will use Tencent Cloud View Cube mobile live broadcast to realize live streaming, screen playback, etc. Interaction uses this plug-in to achieve live broadcast likes, gift giving, barrage sending and receiving, etc.

  The relevant code of this article can be downloaded and viewed in [Github](https://github.com/TencentCloud/chat-demo-flutter/tree/main/lib/src/pages/live_room).

  ### Live streaming and screen playback

  The live broadcast SDK is one of the sub-products of the Tencent Cloud View Cube product family. The live broadcast SDK supports live streaming push, pull streaming, host-audience interaction with hosts, host cross-room PK and other capabilities, providing users with stable and extremely fast live broadcast terminal services.
  See [Live Streaming Flutter SDK Standard Live Streaming](https://www.tencentcloud.com/document/product/1071/50587) to realize the functions of live streaming and screen playback.

  **1: Set License**

  ```dart
  // live.dart
  class Live extends StatefulWidget {
    const Live({Key? key}) : super(key: key);
  
    @override
    State<Live> createState() => _LiveState();
  }
  
  class _LiveState extends State<Live> {
  	...
  	@override
  	void initState() {
  		super.initState();
  		setupLicense();
  	}
  
  	/// Tencent Cloud License Management Page (https://console.cloud.tencent.com/live/license)
  	setupLicense() {
  		// The currently applied License LicenseUrl
  		final licenseUrl = "";
  		// License Key currently applied
  		final licenseKey = "";
  		V2TXLivePremier.setLicence(licenseUrl, licenseKey);
  	}
  	...
  }
  ```

  **2: Live streaming, screen playback**

  ```dart
  // live_player.dart
  ...
  class _LivePlayState extends State<LivePlayer> {
  	...
  	@override
  	void initState() {
  		super.initState();
  		initPlayer();
  	}
  	initPlayer() async {
  		_livePlayer = await V2TXLivePlayer.create();
  	}
  
  	@override
  	void dispose() {
  		super.dispose();
  		_livePlayer.destroy();
  	}
  
  	@override
  	Widget build(BuildContext context) {
  		return Container(
  			color: Colors.black.withOpacity(0.7),
  			child: V2TXLiveVideoWidget(
  				onViewCreated: (viewId) async {
  				_localViewId = viewId;
  				startPlay();
  				},
  			),
  		);
  	}
  
  	void startPlay() async {
  		if (_isPlaying) {
  			return;
  		}
  		if (_localViewId != null) {
  			debugPrint("_localViewId $_localViewId");
  			var code = await _livePlayer.setRenderViewID(_localViewId!);
  			if (code != V2TXLIVE_OK) {
  				debugPrint("StartPlay error： please check remoteView load");
  			}
  		}
  		var url = widget.playUrl;
  		debugPrint("play url: $url");
  		var playStatus = await _livePlayer.startLivePlay(url);
  		debugPrint("play status: $playStatus");
  		if (playStatus != V2TXLIVE_OK) {
  		setState(() {
  			_onError = true;
  		});
  		debugPrint("play error: $playStatus url: $url");
  			return;
  		}
  		await _livePlayer.setPlayoutVolume(100);
  		setState(() {
  			_isPlaying = true;
  		});
  	}
  }
  ```

  ### Live interaction (like, give gifts, send and receive barrage)

  Live interaction is particularly important in live broadcast scenarios. Users interact with the anchor through barrage, gift giving, etc.
  Next, see [Introduction](#msg) to integrate this plugin.

  **1: Initialize, log in to IM**

  We log in to IM outside the plugin, and usually the entire application only needs to initialize and log in to IM once.

  ```dart
  import 'package:tencent_av_chat_room_kit/tencent_cloud_chat_sdk_type.dart';
  
  class _MyHomePageState extends State<MyHomePage> {
  	 final int _sdkAppID = 0; // SDKAppID of the IM application created in the preconditions
  	final String _loginUserID = ""; // UserID in precondition
  	final String _userSig = ""; // UserSig in preconditions
  	@override
  	void initState() {
  		super.initState();
  		_initAndLoginIm();
  	  }
  
  	_initAndLoginIm() async {
  		await TencentImSDKPlugin.v2TIMManager.initSDK(
  			sdkAppID: _sdkAppID,
  			loglevel: LogLevelEnum.V2TIM_LOG_ALL,
  			listener: V2TimSDKListener());
  		TencentImSDKPlugin.v2TIMManager
            .login(userID: _loginUserID, userSig: _userSig);
  	}
  }
  ```

  **2: Use plugins**

  ```dart
  // live_room.dart
  
  class LiveRoom extends StatelessWidget {
  	final String loginUserID;
  	final String playUrl;
  	final String avChatRoomID = ''; // A live broadcast room is essentially all users sending and receiving messages in an av chat room type group
  
  	LiveRoom({Key? key, required this.loginUserID, required this.playUrl})
        : super(key: key);
  
  	@override
  	Widget build(BuildContext context) {
  		return Stack(
  			children: [
  				LivePlayer(playUrl: playUrl), // Live streaming and screen playback
  				TencentCloudAVChatRoom(
  					config: TencentCloudAvChatRoomConfig(
  						avChatRoomID: avChatRoomID,
  						loginUserID: loginUserID, //Login user ID
  					),
  					data: TencentCloudAvChatRoomData(
  						isSubscribe: false,
  						notification: "Broadcast Room Announcement",
  						anchorInfo: AnchorInfo(
  							subscribeNum: 200,
  							fansNum: 5768,
  							nickName: "stormy life",
  							avatarUrl:""
  						),
  					)
  				)
  			]
  		)
  	}
  }
  ```

  Above we use `Stack Widget` to combine `LivePlayer (live broadcast)` and `LiveRoom (interactive)` through cascading.

  **3: How to customize**

  The plug-in itself provides a default UI, but users often have different UIs during actual use. Next, we will introduce how to customize this plug-in.

  ```dart
  ...
  @override
  Widget build(BuildContext context) {
  return Stack(
  children: [
  LivePlayer(playUrl: playUrl), // Live streaming and screen playback
  TencentCloudAVChatRoom(
  ...
  TencentCloudAvChatRoomCustomWidgets(
  roomHeaderAction: Container(), // The area custom component is displayed in the upper right corner of the screen, and the default display is the number of people online in the live room
  roomHeaderLeading: Container(), // The area custom component is displayed in the upper left corner of the screen, and the anchor information is displayed by default
  roomHeaderTag: Container(), // Below roomHeaderAction and roomHeaderLeading, it is generally used to display leaderboards, popularity, etc.
  onlineMemberListPanelBuilder: (context, id) { // Customize the panel that expands after clicking on the number of online members in the live broadcast room
  return Container();
  },
  anchorInfoPanelBuilder: (context, id) { // Customize the expanded panel after the anchor's avatar is clicked
  return Container();
  },
  giftsPanelBuilder: (context) { // Customize the panel displayed after clicking the gift button at the bottom right of the screen
  return Container();
  },
  messageItemBuilder: (context, message, child) { // Customize bullet chat messages
  return Container();
  },
  messageItemPrefixBuilder: (context, message) { // Customize the prefix of bullet chat messages, generally used to customize fan brands, etc.
  return Container();
  },
  giftMessageBuilder: (context, message) { // Custom gift message, gift message that slides in from the left side of the screen
  return Container();
  },
  textFieldActionBuilder: (// Customize the lower right area of the screen
  context,
  ) {
  return [Container()];
  },
  textFieldDecoratorBuilder: (context) { // Customize the input box at the bottom left of the screen
  return Container();
  }
  )
  )
  ]
  )
  }
  ```

  - **4: Gift**
    
    Giving gifts is a very important scene in the live broadcast scene. This plugin provides analysis of three types of gifts by default, users only need to send a custom message in a specific format to display the gift message on the interface. The default gift panel of this plug-in is only used to display the gift message parsing function. Usually, gifts will involve the logic of user billing and measurement, so users need to call the server interface to send gifts according to their business needs. information. The gift giving process is as follows:
    
    - The short connection request from the client to its own business server involves billing logic.
    - After billing, the sender directly sees that XXX sent XXX a gift. (To ensure that the sender sees the gift they sent, when there is a large amount of messages, the abandonment strategy may be triggered)
    - After billing and settlement, call the server interface to send a custom message (gift)
      Gift Messages We do this by sending custom messages. Three gift formats are defined as follows:

  ```dart
  // Gifts with special effects (the details of the gift will slide into the left side of the screen and the special effects of the gift (Lottie/SVAGA) will be displayed on the screen)
  final customInfoRocket = {
  "version": 1.0, // protocol version number
  "businessID": "flutter_live_kit", // Business ID field
  "data": {
  "cmd":
  "send_gift_message", // must be send_gift_message
  "cmdInfo": {
  "type": 3, // gift type
  "giftUrl": "", // URL of gift image
  "giftCount": 1, // number of gifts
  "giftSEUrl": "assets/live/rocket.json", // gift special effect address, if it starts with http, the network address will be loaded
  "giftName": "Super Rocket", // gift name
  },
  }
  };
  
  // The gift does not have special effects (it will slide in on the left side of the screen)
  final customInfoPlane = {
      "version": 1.0, // protocol version number
      "businessID": "flutter_live_kit", // Business ID field
      "data": {
        "cmd":
            "send_gift_message", // must be send_gift_message
        "cmdInfo": {
          "type": 2, // gift type
          "giftUrl": "", // URL of gift image
          "giftCount": 1, // number of gifts
          "giftName": "Airplane", // gift name
        },
      }
  };
  
  // Ordinary gift (the gift will be displayed in the barrage, and will not slide in from the left side of the screen and display special effects)
  final normalGift = {
      "version": 1.0, // protocol version number
      "businessID": "flutter_live_kit", // business ID field
      "data": {
        "cmd":
            "send_gift_message", // must be send_gift_message
        "cmdInfo": {
          "type": 1, //Ordinary gift
          "giftUrl": "", // URL of gift image
          "giftCount": 1, // number of gifts
          "giftName": "flower", // gift name
          "giftUnits": "Duo", // gift units
        },
      }
  };
  ```

  **5: Theme**
  In addition to customization, this plugin also provides the capability of `theme`. The theme is divided into two parts: `color` and `font`. [Theme](#tencentcloudavchatroomtheme) can be customized according to your needs.

  ## API Docs

  ### TencentCloudAvChatRoomData

  The data that the component needs to use, such as anchor information, broadcast room announcements, etc.

  ```dart
  TencentCloudAvChatRoomData(
  anchorInfo: AnchorInfo(), // anchor information
  isSubscribe: false, // whether to subscribe
  notification: "Live Room Announcement" // Live Room Announcement
  )
  ```

  ### TencentCloudAvChatRoomConfig

  Component configuration information.

  ```dart
  TencentCloudAvChatRoomConfig(
    avChatRoomID: '', // AV Chat Group. Group ID of AV Chat Room type.[https://cloud.tencent.com/document/product/269/75697]
    loginUserID: '', // login user ID
    sdkAppID: 0, // IM application ID
    userSig: '', // sig generated by user ID and secretKey
    barrageMaxCount: 200, // The maximum number of barrage. The default is 200. When the number of entries is exceeded, the earlier barrage will be cleared.
    giftHttpBase: '', // Gift message http base.
    displayConfig: DisplayConfig() // Can control the display and hiding of some components on the interface
    )
  ```

  ### TencentCloudAvChatRoomController

  Component controller, which can be called outside the component to update data, send messages, etc.

  ```dart
  final controller = TencentCloudAvChatRoomController();
  final _needUpdateData = TencentCloudAvChatRoomData(
          anchorInfo: AnchorInfo(), // anchor information
  isSubscribe: false, // whether to subscribe
  notification: "Live Room Announcement" // Live Room Announcement
  );
  final _textString = "I am a text message";
  
  final customInfoRocket = {
  "version": 1.0, // protocol version number
  "businessID": "flutter_live_kit", // Business ID field
  "data": {
  "cmd":
  "send_gift_message", // command
  "cmdInfo": { // Information carried by the command
  "type": 3, // gift type
  "giftUrl": "1e8913f8c6d804972887fc179fa1fbd7.png", // gift image address
  "giftCount": 1, // number of gifts
  "giftSEUrl": "assets/live/rocket.json", // gift special effect address
  "giftName": "Super Rocket", // gift name
  },
  }
  };
  
  final customInfoPlane = {
      "version": 1.0,
      "businessID": "flutter_live_kit",
      "data": {
        "cmd":
            "send_gift_message",
        "cmdInfo": {
          "type": 2,
          "giftUrl": "5e175b792cd652016aa87327b278402b.png",
          "giftCount": 1,
          "giftName": "Airplane",
        },
      }
  };
  
  final customInfoFlower = {
      "version": 1.0,
      "businessID": "flutter_live_kit",
      "data": {
        "cmd":
            "send_gift_message",
        "cmdInfo": {
          "type": 1,
          "giftUrl": "8f25a2cdeae92538b1e0e8a04f86841a.png",
          "giftCount": 1,
          "giftName": "Flower",
          "giftUnits": "Duo",
        },
      }
  };
  
  // Update the data information of the incoming component.
  controller. updateData(_needUpdateData);
  
  // send text message
  controller. sendTextMessage(_textString);
  
  // Send a gift message, the gift message needs to follow the specific format above. There are three types of gifts: [1]: Normal gifts [2]: Gifts without special effects [3]: Gifts with special effects
  controller.sendGiftMessage(jsonEncode(customInfoFlower));
  
  // Send any type of message, [message] needs to be created by yourself
  controller. sendMessage(message);
  
  // Play special effects animation (Lottie, SVGA).
  controller.playAnimation("assets/live/rocket.json"):
  ```

  ### TencentCloudAvChatRoomCallback

  Event callback。

  ```dart
  TencentCloudAvChatRoomCallback(
  onMemberEnter: (memberInfo) {}, // someone enters the live room
  onRecvNewMessage: (message) {} // received barrage message
  )
  ```

  ### TencentCloudAvChatRoomCustomWidgets

  custom components

  ```dart
  TencentCloudAvChatRoomCustomWidgets(
  roomHeaderAction: Container(), // The area custom component is displayed in the upper right corner of the screen, and the default display is the number of people online in the live room
  roomHeaderLeading: Container(), // The area custom component is displayed in the upper left corner of the screen, and the anchor information is displayed by default
  roomHeaderTag: Container(), // Below roomHeaderAction and roomHeaderLeading, it is generally used to display leaderboards, popularity, etc.
  onlineMemberListPanelBuilder: (context, id) { // Customize the panel that expands after clicking on the number of online members in the live broadcast room
  return Container();
  },
  anchorInfoPanelBuilder: (context, id) { // Customize the expanded panel after the anchor's avatar is clicked
  return Container();
  },
  giftsPanelBuilder: (context) { // Customize the panel displayed after clicking the gift button at the bottom right of the screen
  return Container();
  },
  messageItemBuilder: (context, message, child) { // Customize bullet chat messages
  return Container();
  },
  messageItemPrefixBuilder: (context, message) { // Customize the prefix of bullet chat messages, generally used to customize fan brands, etc.
  return Container();
  },
  giftMessageBuilder: (context, message) { // Custom gift message, gift message that slides in from the left side of the screen
  return Container();
  },
  textFieldActionBuilder: (// Customize the lower right area of the screen
  context,
  ) {
  return [Container()];
  },
  textFieldDecoratorBuilder: (context) { // Customize the input box at the bottom left of the screen
  return Container();
  }
  )
  ```

  [](id:tcentcloudavchatroomtheme)
  ### TencentCloudAvChatRoomTheme

  Theme

  ```dart
  TencentCloudAvChatRoomTheme(
  backgroundColor: Colors.black, // The background color of the widget,
  hintColor: Colors.red, // hint text color
  highlightColor: Colors.orange, // highlight color
  accentColor: Colors.white, // foreground color
  textTheme: TencentCloudAvChatRoomTextTheme(), // font theme
  secondaryColor: Colors.grey, // secondary color
  inputDecorationTheme: InputDecorationTheme() // input box theme
  )
  ```

  ### TencentCloudAvChatRoomTextTheme

  font theme

  ```dart
  TencentCloudAvChatRoomTextTheme(
  giftBannerSubTitleStyle: TextStyle(), // gift message drawn on the left side of the screen sub title font theme, gift name
  giftBannerTitleStyle: TextStyle(), // The title font theme of the gift message drawn on the left side of the screen
  anchorTitleStyle: TextStyle(), // Anchor name font theme
  anchorSubTitleStyle: TextStyle(), // like font theme
  barrageTitleStyle: TextStyle(), // barrage message sender name subject
  barrageTextStyle: TextStyle() // Barrage message content theme
  )
  ```

  ## contact us

  If there's anything unclear or you have more ideas, feel free to contact us!

  - [Telegram Group](https://t.me/+1doS9AUBmndhNGNl)
  - [WhatsApp Group](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)
