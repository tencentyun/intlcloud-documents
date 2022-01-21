
## Use Cases

By using Puppeteer in SCF, you can take screenshots of, save, screencap, and generate PDFs from specific webpages as needed. This feature extends the on-demand launch feature of SCF and only starts instance execution when needed, without using virtual machines or containers to continuously run the service. Therefore, you can easily encapsulate the feature as a general capability.

The runtime environment of SCF currently has only one built-in font. This document describes how to use custom fonts in SCF to meet your personalized needs.

The best practice in this document is implemented based on SCF's image deployment capability. It packages Chrome, Puppeteer, and desired font files in an image and deploys a function through this image.


## Directions
### Dockerfile
This document provides a simple Alpine-based image to create an image build file that includes Chrome and Puppeteer. The file can be named `mypuppeteer.dockerfile` as shown below:

```
FROM alpine

# Installs latest Chromium (92) package.
RUN apk add --no-cache \
      chromium \
      nss \
      freetype \
      harfbuzz \
      ca-certificates \
      ttf-freefont \
      nodejs \
      yarn


# Tell Puppeteer to skip installing Chrome. We'll be using the installed package.
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=true \
    PUPPETEER_EXECUTABLE_PATH=/usr/bin/chromium-browser

# Puppeteer v10.0.0 works with Chromium 92.
RUN yarn add puppeteer@10.0.0

# Add the CJK font to support Chinese character
COPY NotoSansCJK.ttc  /usr/share/fonts/TTF

```


<dx-alert infotype="notice" title="">
-The [font file](https://github.com/googlefonts/noto-cjk/tree/main/Sans) used in the code needs to be downloaded and placed in the same directory as the docker file.
- This document only provides a sample. You can select font files as needed and adjust the filenames and corresponding fields in the docker file.
</dx-alert>



### Image build

You can build the image by running the following command, which will create an image named `mypuppeteer:v1`:

```shell
docker build -t mypuppeteer:v1 -f mypuppeteer.dockerfile .

```

### Local test

After the local image is built, you can use the following `test.js` script to quickly test and verify it by taking and saving a screenshot of a webpage.

```js
const puppeteer = require('puppeteer');
(async () => {
  const browser = await puppeteer.launch({
    executablePath: '/usr/bin/chromium-browser',
    args: ['--no-sandbox','--disable-setuid-sandbox','--ignore-certificate-errors'],
    defaultViewport: {
        width: 1920,
        height: 1080,
        deviceScaleFactor: 3,
      },
  });
  const page = await browser.newPage();
  await page.goto('https://www.baidu.com');
  await page.screenshot({path: '/home/test.png'});
  await browser.close();
})();
```

Run the following command to run the image, mount the test script directory into a container and run it, and the screenshot file will also be generated in this directory.

```shell
docker run -it --rm -v $(pwd):/home mypuppeteer:v1 node /home/test.js
```

You can verify whether the font file works by checking whether the screenshot file is output.


### Subsequent operations
After the image that can run Chrome and Puppeteer is built, you can further build a function runtime environment based on it, push it to the image repository of Tencent Cloud, and then use SCF's custom image deployment capabilities to create your own services.
For the description of custom image deployment in SCF and how to use it, see [Feature Description](https://intl.cloud.tencent.com/document/product/583/41076).



