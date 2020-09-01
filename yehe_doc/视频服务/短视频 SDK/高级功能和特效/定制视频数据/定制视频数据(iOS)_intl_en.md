## Shoot Preprocessing Callback 
```objc
/**
 * Call back in the OpenGL thread. You can further process the captured video image in the callback
 * @param texture   Texture ID
 * @param width   Texture width
 * @param height   Texture height
 * @return   Texture returned to SDK
 * Note: the texture type called back by the SDK is `GL_TEXTURE_2D`, which must also be the texture type returned to the SDK by the API. The callback is after that of SDK beauty filter, and the texture format is `GL_RGBA`
 */
- (GLuint)onPreProcessTexture:(GLuint)texture width:(CGFloat)width height:(CGFloat)height;

/**
 * Face data callback (Enterprise Edition API)
 * @prama points   Face coordinates
 * Note: features related to face recognition such as face recognition-based stickers, eye enlarging filter, and face slimming filter are used. This callback will be called before `onPreProcessTexture:width:height:`
 */
- (void)onDetectFacePoints:(NSArray *)points;

/**
 * Call back in the OpenGL thread. You can release the created OpenGL resources in the callback
 */
- (void)onTextureDestoryed;
```
## Editing Preprocessing Callback
```objc
/** 
 Call back in the OpenGL thread. You can further process the captured video image in the callback
 @param texture   Texture ID
 @param width   Texture width
 @param height   Texture height
 @param timestamp   Texture timestamp in ms
 @return   Texture returned to SDK
 Note: the texture type called back by the SDK is `GL_TEXTURE_2D`, which must also be the texture type returned to the SDK by the API. The callback is after that of SDK beauty filter, and the texture format is `GL_RGBA`
 `timestamp` is the presentation timestamp (PTS) of the current video frame in ms. You can customize the special effect filter as needed.
 */
- (GLuint)onPreProcessTexture:(GLuint)texture width:(CGFloat)width height:(CGFloat)height timestamp:(UInt64)timestamp;

/**
 * Call back in the OpenGL thread. You can release the created OpenGL resources in the callback
 */
- (void)onTextureDestoryed;
```
