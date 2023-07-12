### What do I do if the `Call to undefined method GuzzleHttp\Utils::chooseHandler()` error is thrown when the PHP SDK is running?


The PHP SDK depends on Guzzle. You are advised to install the SDK using Composer.
- If you install the SDK using Composer, run the `php composer.phar install` command to install the SDK and the dependencies.
- If you install the SDK using the source code, run the `composer install` command to install the SDK and the dependencies. For more information, please see [PHP SDK - Download and Installation](https://intl.cloud.tencent.com/document/product/436/12266).


### What do I do if the `cURL error 60: See http://curl.haxx.se/libcurl/c/libcurl-errors.html` error is reported when I use the PHP SDK to upload files?

If something is wrong with your certificate in the PHP environment, errors similar to `cURL error 60: See http://curl.haxx.se/libcurl/c/libcurl-errors.html` will be reported. You can solve the problem as follows:

1. Download the `cacert.pem` certificate file at `https://curl.haxx.se/ca/cacert.pem` and save it to the PHP installation path.
2. Edit the `php.ini` file, delete the semicolon (;) before the `curl.cainfo` configuration item, and set its value to the absolute path of the `cacert.pem` certificate file.
3. Restart PHP-dependent services.

