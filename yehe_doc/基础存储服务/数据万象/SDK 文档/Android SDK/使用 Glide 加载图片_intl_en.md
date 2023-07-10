
This document describes how to load images with Glide.

## Installing Glide

```
implementation 'com.github.bumptech.glide:glide:version'
```

## Basic Image Processing

Use Glide and CI together to perform basic image processing operations (except TPG and AVIF features).

1. Construct a `CIImageLoadRequest` by using `CloudInfinite` and `CITransformation`.
```
CloudInfinite cloudInfinite = new CloudInfinite();
CITransformation transform = new CITransformation();
transform.thumbnailByScale(50).iradius(60);
CIImageLoadRequest request = cloudInfinite.requestWithBaseUrlSync(url, transform);
```
2. Get the URL through the obtained `CIImageLoadRequest` and use Glide to load it.
```
Glide.with(activity).load(request.getUrl().toString()).into(imageview);
```

## Using CI's Glide Feature

Install the cloud-infinite-glide SDK and glide:compiler.
```
implementation 'com.qcloud.cos:cloud-infinite-glide:1.2.1'	
annotationProcessor 'com.github.bumptech.glide:compiler:version' 
```
Register relevant decoders and loaders through `AppGlideModule` to implement corresponding features.
```
 // Register the custom `GlideModule`
 // You should create this class to register `CIImageRequestModelLoader` and `ImageAveDecoder`.<br>
 // If you develop class libraries, you can inherit `LibraryGlideModule` to create a similar registration class.
@GlideModule
public class MyAppGlideModule extends AppGlideModule {
    @Override
    public void registerComponents(@NonNull Context context, @NonNull Glide glide, Registry registry) {
        // Register a loader that supports `CIImageLoadRequest`
        registry.prepend(CIImageLoadRequest.class, InputStream.class, new CIImageRequestModelLoader.Factory());

        // Register the main color decoder
        registry.prepend(InputStream.class, Bitmap.class, new ImageAveDecoder(glide.getBitmapPool()));
    }
}
```

#### Preloading with image main color

```
// Register the main color decoder in `AppGlideModule` first
registry.prepend(InputStream.class, Bitmap.class, new ImageAveDecoder(glide.getBitmapPool()));

// Use Glide's thumbnail to preload the main color
Glide.with(context)
               .load(imageUrl)
               .thumbnail(CloudInfiniteGlide.getImageAveThumbnail(context, imageUrl))
               .into(imageview);
```

#### Directly loading `CIImageLoadRequest`

Currently, this method is only used for the case where the header transfers the target image format during format conversion.

```
registry.prepend(CIImageLoadRequest.class, InputStream.class, new CIImageRequestModelLoader.Factory());
```

## Using CI's TPG Feature

Install the TPG SDK and glide:compiler.
```
implementation 'com.qcloud.cos:tpg:1.3.2'	
annotationProcessor 'com.github.bumptech.glide:compiler:version' 
```
Register relevant decoders through `AppGlideModule` to implement corresponding features.
```
 // Register the custom `GlideModule`
 // You should create this class to register `TpgDecoder` and `ByteBufferTpgGifDecoder`.<br>
 // If you develop class libraries, you can inherit `LibraryGlideModule` to create a similar registration class.
@GlideModule
public class MyAppGlideModule extends AppGlideModule {
    @Override
    public void registerComponents(@NonNull Context context, @NonNull Glide glide, Registry registry) {
        /*------------------Decoder start-------------------------*/
        // Register the static TPG image decoder
        registry.prepend(InputStream.class, Bitmap.class, new TpgDecoder(glide.getBitmapPool()));
        // Register the animated TPG image decoder
        ByteBufferTpgGifDecoder byteBufferTpgGifDecoder = new ByteBufferTpgGifDecoder(context, glide.getBitmapPool(), glide.getArrayPool());
        registry.prepend(InputStream.class, GifDrawable.class, new StreamTpgGifDecoder(byteBufferTpgGifDecoder));
        registry.prepend(ByteBuffer.class, GifDrawable.class, byteBufferTpgGifDecoder);
        /*------------------Decoder end-------------------------*/
    }
}
```

#### Loading static TPG image

```
registry.prepend(InputStream.class, Bitmap.class, new TpgDecoder(glide.getBitmapPool()));
```

#### Loading animated TPG image

```
ByteBufferTpgGifDecoder byteBufferTpgGifDecoder = new ByteBufferTpgGifDecoder(context, glide.getBitmapPool(), glide.getArrayPool());
registry.prepend(InputStream.class, GifDrawable.class, new StreamTpgGifDecoder(byteBufferTpgGifDecoder));
registry.prepend(ByteBuffer.class, GifDrawable.class, byteBufferTpgGifDecoder);
```

## Using CI's AVIF Feature

Install the AVIF SDK and glide:compiler.
```
implementation 'com.qcloud.cos:avif:1.0.0'	
annotationProcessor 'com.github.bumptech.glide:compiler:version' 
```
Register relevant decoders through `AppGlideModule` to implement corresponding features.
```
 // Register the custom `GlideModule`
 // You should create this class to register relevant decoders.<br>
 // If you develop class libraries, you can inherit `LibraryGlideModule` to create a similar registration class.
@GlideModule
public class MyAppGlideModule extends AppGlideModule {
    @Override
    public void registerComponents(@NonNull Context context, @NonNull Glide glide, Registry registry) {
        /*------------------Decoder start-------------------------*/
        // Register the static AVIF image decoder
        registry.prepend(Registry.BUCKET_BITMAP, InputStream.class, Bitmap.class, new StreamAvifDecoder(glide.getBitmapPool(), glide.getArrayPool()));
        registry.prepend(Registry.BUCKET_BITMAP, ByteBuffer.class, Bitmap.class, new ByteBufferAvifDecoder(glide.getBitmapPool()));
        // Register the animated AVIF image decoder
        registry.prepend(InputStream.class, AvifSequenceDrawable.class, new StreamAvifSequenceDecoder(glide.getBitmapPool(), glide.getArrayPool()));
        registry.prepend(ByteBuffer.class, AvifSequenceDrawable.class, new ByteBufferAvifSequenceDecoder(glide.getBitmapPool()));
        /*------------------Decoder end-------------------------*/
    }
}
```

#### Loading static AVIF image

```
registry.prepend(Registry.BUCKET_BITMAP, InputStream.class, Bitmap.class, new StreamAvifDecoder(glide.getBitmapPool(), glide.getArrayPool()));
registry.prepend(Registry.BUCKET_BITMAP, ByteBuffer.class, Bitmap.class, new ByteBufferAvifDecoder(glide.getBitmapPool()));
```

#### Loading animated AVIF image

```
registry.prepend(InputStream.class, AvifSequenceDrawable.class, new StreamAvifSequenceDecoder(glide.getBitmapPool(), glide.getArrayPool()));
registry.prepend(ByteBuffer.class, AvifSequenceDrawable.class, new ByteBufferAvifSequenceDecoder(glide.getBitmapPool()));
```

