## Callback for Pre-Processing for Shooting  
<dx-codeblock>
::: objc objc
/**
 * Call back in the OpenGL thread, where captured images can be processed.
 * @param texture    Texture ID
 * @param width      Texture width
 * @param height     Texture height
 * @return           Texture returned to the SDK
 * Note: The type of textures called back by the SDK is GL_TEXTURE_2D, which must also be the texture type returned by the API. This callback follows the calling of beauty filter APIs, and the texture format is GL_RGBA.
 */
- (GLuint)onPreProcessTexture:(GLuint)texture width:(CGFloat)width height:(CGFloat)height;

/**
 * Call back in the OpenGL thread. You can release OpenGL resources here.
 */
- (void)onTextureDestoryed;
:::
</dx-codeblock>


## Callback for Pre-Processing for Video Editing
<dx-codeblock>
::: objc objc
/** 
 Call back in the OpenGL thread, where captured images can be processed.
 @param textureId  Texture ID
 @param width      Texture width
 @param height     Texture height
 @param timestamp        Texture timestamp (ms)
 @return           Texture returned to the SDK
 Note: The type of textures called back by the SDK is GL_TEXTURE_2D, which must also be the texture type returned by the API. This callback follows the calling of beauty filter APIs, and the texture format is GL_RGBA.
 Timestamp is the PTS of the current video frame and is measured in milliseconds. You can customize beauty filter effects based on your needs.
 */
- (GLuint)onPreProcessTexture:(GLuint)texture width:(CGFloat)width height:(CGFloat)height timestamp:(UInt64)timestamp;

/**
 * Call back in the OpenGL thread. You can release OpenGL resources here.
 */
- (void)onTextureDestoryed;
:::
</dx-codeblock>
