Callback of Pre-processing for Shooting 
```
/**
 * Call back in the OpenGL thread, where captured images can be processed.
 * @param texture    Texture ID
 * @param width      Texture width
 * @param height     Texture height
 * @return           Texture returned to the SDK
 * Note: the texture type called back by the SDK is GL_TEXTURE_2D, which must also be the texture type returned by the API. This callback follows the calling of beauty filter APIs, and the texture format is GL_RGBA.
 */
- (GLuint)onPreProcessTexture:(GLuint)texture width:(CGFloat)width height:(CGFloat)height;

/**
 * Callback of facial feature positions (Enterprise Edition API)
 * @prama points Coordinates of facial features
 * Note: facial feature positions are called back before `onPreProcessTexture:width:height:`. The callback is used for effects that use widgets, for example, animated stickers or the eye enlarging or face slimming filter.
 */
- (void)onDetectFacePoints:(NSArray *)points;

/**
 * Call back in the OpenGL thread, where the OpenGL resources created can be released.
 */
- (void)onTextureDestoryed;
```


## Callback of Pre-processing for Video Editing
```
/** 
 Call back in the OpenGL thread, where captured images can be processed.
 @param textureId  Texture ID
 @param width      Texture width
 @param height     Texture height
 @param timestamp        Texture timestamp (ms)
 @return           Texture returned to the SDK
 Note: the texture type called back by the SDK is GL_TEXTURE_2D, which must also be the texture type returned by the API. This callback follows the calling of beauty filter APIs, and the texture format is GL_RGBA.
 Timestamp is the PTS of the current video frame and is measured in milliseconds. You can customize beauty filter effects based on your needs.
 */
- (GLuint)onPreProcessTexture:(GLuint)texture width:(CGFloat)width height:(CGFloat)height timestamp:(UInt64)timestamp;

/**
 * Call back in the OpenGL thread, where the OpenGL resources created can be released.
 */
- (void)onTextureDestoryed;
```
