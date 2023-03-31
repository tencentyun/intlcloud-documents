- ## Description

  Since version of v1.1.0, the capability of theme and customize colors has been improved to a large extent.

  While TUIKit provides a default set of colors for those widgets that you can use directly, you can also customize those colors up to your needs.

  ## Customize Colors

  ### The color object of the colors

  In this object, you can easily customize each color on the interface of the widgets TUIKit provided.

  Instantiate a `TUITheme()` object, and specify each color you want to modify, apart from the default ones, directly to it.

  This object contains the color configuration for those colors.


  ```dart
    // Primary Color For The App
    final Color? primaryColor;
  
    // Secondary Color For The App
    final Color? secondaryColor;
  
    // Info Color, Used For Secondary Action Or Info
    final Color? infoColor;
  
    // Weak Background Color, Lighter Than Main Background, Used For Marginal Space Or Shadowy Space
    final Color? weakBackgroundColor;
  
    // Weak Background Color, Lighter Than Main Background, Used For Marginal Space Or Shadowy Space
    final Color? wideBackgroundColor;
  
    // Weak Divider Color, Used For Divider Or Border
    final Color? weakDividerColor;
  
    // Weak Text Color
    final Color? weakTextColor;
  
    // Dark Text Color
    final Color? darkTextColor;
  
    // Light Primary Color, Used For AppBar Or Several Panels
    final Color? lightPrimaryColor;
  
    // TextColor
    final Color? textColor;
  
    // Caution Color, Used For Warning Actions
    final Color? cautionColor;
  
    // Group Owner Identification Color
    final Color? ownerColor;
  
    // Group Admin Identification Color
    final Color? adminColor;
  
    // white
    final Color? white;
  
    // black
    final Color? black;
  
    // input fill color
    final Color? inputFillColor;
  
    // grey text color
    final Color? textgrey;
  
  
    /// The background color of the conversation item.
    final Color? conversationItemBgColor;
  
    /// The border color of the conversation item.
    final Color? conversationItemBorderColor;
  
    /// The background color of the conversation item when activated.
    final Color? conversationItemActiveBgColor;
  
    /// The background color of the conversation item when pinned to top.
    final Color? conversationItemPinedBgColor;
  
    /// The font color of the conversation title.
    final Color? conversationItemTitleTextColor;
  
    /// The font color of the conversation last message.
    final Color? conversationItemLastMessageTextColor;
  
    /// The font color of the time on conversation item.
    final Color? conversationItemTitmeTextColor;
  
    /// The indicator color of an online status user.
    final Color? conversationItemOnlineStatusBgColor;
  
    /// The indicator color of an offline status user.
    final Color? conversationItemOfflineStatusBgColor;
  
    /// The background color of the conversation unread count.
    final Color? conversationItemUnreadCountBgColor;
  
    /// The font color of the conversation unread count.
    final Color? conversationItemUnreadCountTextColor;
  
    /// The font color of the draft text on conversation item.
    final Color? conversationItemDraftTextColor;
  
    /// The color of the icon, indicates that this conversation is not supposed to notify the user when new messages incomes.
    final Color? conversationItemNoNotificationIconColor;
  
    /// The font color of the slider bar of conversation item.
    final Color? conversationItemSliderTextColor;
  
    /// The background color of 'clear' button on the slider bar of conversation item.
    final Color? conversationItemSliderClearBgColor;
  
    /// The background color of 'pin to top' button on the slider bar of conversation item.
    final Color? conversationItemSliderPinBgColor;
  
    /// The background color of 'delete' button on the slider bar of conversation item.
    final Color? conversationItemSliderDeleteBgColor;
  
    /// The background color of the conversation item when chosen on desktop.
    final Color? conversationItemChooseBgColor;
  
    /// The background color of the chat page.
    final Color? chatBgColor;
  
    /// The background color of the time divider on chat page.
    final Color? chatTimeDividerTextColor;
  
    /// The background color of the top app bar on chat page.
    final Color? chatHeaderBgColor;
  
    /// The font color of title on top app bar on chat page.
    final Color? chatHeaderTitleTextColor;
  
    /// The font color of 'back' text on top app bar on chat page.
    final Color? chatHeaderBackTextColor;
  
    /// The font color of action on top app bar on chat page.
    final Color? chatHeaderActionTextColor;
  
    /// The font color of title on top app bar on chat page.
    final Color? chatMessageItemTextColor;
  
    /// The background color of the message from self.
    final Color? chatMessageItemFromSelfBgColor;
  
    /// The background color of the message from other users.
    final Color? chatMessageItemFromOthersBgColor;
  
    /// The font color of the read receipt indicator.
    final Color? chatMessageItemUnreadStatusTextColor;
  
    /// The background color of the dynamic tongue.
    final Color? chatMessageTongueBgColor;
  
    /// The font color of the dynamic tongue.
    final Color? chatMessageTongueTextColor;
  ```

  ### Configuration

  Invoke the `setTheme` method from TUIKit, and specify it with the `TUITheme()` object from the previous phase.

  This method can be invoked at any time to modify the color dynamically.

  ```dart
  final CoreServicesImpl _coreInstance = TIMUIKitCore.getInstance();
  _coreInstance.setTheme(theme: TUITheme());
  ```

  ## Contact us[](id:contact)

  If there's anything unclear or you have more ideas, feel free to contact us!

  - [Telegram Group](https://t.me/+1doS9AUBmndhNGNl)
  - [WhatsApp Group](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)
