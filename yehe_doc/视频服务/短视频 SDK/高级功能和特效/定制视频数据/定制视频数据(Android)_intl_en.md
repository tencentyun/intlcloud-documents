## Shoot Preprocessing Callback 

``` 
public interface VideoCustomProcessListener {
/**
  * Call back in the OpenGL thread. You can further process the captured video image in the callback
  * @param textureId   Texture ID
  * @param width   Texture width
  * @param height   Texture height
  * @return   Texture ID returned to SDK. If no processing is required, simply return the texture ID passed in.
  * Note: the texture type called back by the SDK is `GLES20.GL_TEXTURE_2D`, which must also be the texture type returned to the SDK by the API
  */
int onTextureCustomProcess(int textureId, int width, int height);

/**
  * Call back face coordinates in Enterprise Edition
  * @param points   Normalized face coordinates. Every two coordinates indicate the `X` and `Y` values of a point. The value range is [0.f,1.f]
  */
void onDetectFacePoints(float[] points);

/**
  * Call back in the OpenGL thread. You can release the created OpenGL resources in the callback
  */
void onTextureDestroyed();
}
```

## Editing Preprocessing Callback
``` 
public interface TXVideoCustomProcessListener {
        /**
         * Call back in the OpenGL thread. You can further process the captured video image in the callback
         *
         * @param textureId   Texture ID
         * @param width   Texture width
         * @param height   Texture height
         * @return   Texture ID returned to SDK. If no processing is required, simply return the texture ID passed in.
         * <p>
         * Note: the texture type called back by the SDK is `GLES20.GL_TEXTURE_2D`, which must also be the texture type returned to the SDK by the API
         */
        int onTextureCustomProcess(int textureId, int width, int height, long timestamp);

        /**
         * Call back in the OpenGL thread. You can release the created OpenGL resources in the callback
         */
        void onTextureDestroyed();
    }

```
