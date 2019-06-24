
A function can be created in the console or through TCCLI.


## Creating a Function in the Console

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf) and select Functions on the left.
2. Select the region for which to create functions at the top of the main interface. Click **Create** to enter the function creation process.
3. You can choose to use **Blank function** or **Function template** to create a function.
 - When using **Blank function**, you need to enter the required function name and runtime environment to create the function.
 - When using **Function template**, you need to enter the required function name to create the function, and the configuration such as runtime environment depends on the configuration in the template.

## Creating a Function Through TCCLI

Before starting, you need to install and configure TCCLI by following the instructions in [TCCLI Installation and Configuration](https://cloud.tencent.com/document/product/440/6176).
Use the `tccli scf CreateFunction` command to create a function.

### Creating a Function with a Local zip Package

The sample below creates a function using a local zip package.
First, Base64-encode the zip package named hello.zip for URL encoding:
```
$ alias urlencode='python -c "import sys, urllib as ul;print ul.quote_plus(sys.argv[1])"'
$ urlencode `base64 -i hello.zip` 
UEsDBBQACAAIAFaEJU0AAAAAAAAAAAAAAAAIABAAaW5kZXgucHlVWAwAQpWPWyOVj1v2ARQAU07OT8nMS7ctLUnTteDiSklNU8hNzMzTSC1LzSvRUUjOzytJrSjRtOJSAIKCosy8Eg2ljNScnHyF8vyinBQlTSQJsB6IQFFqSWlRngJYhAsAUEsHCAg25ABRAAAAZAAAAFBLAwQKAAAAAABnhCVNAAAAAAAAAAAAAAAACQAQAF9fTUFDT1NYL1VYDABClY9bQpWPW%2FYBFABQSwMEFAAIAAgAVoQlTQAAAAAAAAAAAAAAABMAEABfX01BQ09TWC8uX2luZGV4LnB5VVgMAEKVj1sjlY9b9gEUAGNgFWNnYGJg8E1MVvAPVohQgAKQGAMnEBsBcR0Qg%2FgbGIgCjiEhQVAmSMcCIBZAU8KIEJdKzs%2FVSywoyEnVy0ksLiktTk1JSSxJVQ4IBik0mtofDaIPhAvogWgAUEsHCAyTbm5cAAAAsAAAAFBLAQIVAxQACAAIAFaEJU0INuQAUQAAAGQAAAAIAAwAAAAAAAAAAECkgQAAAABpbmRleC5weVVYCABClY9bI5WPW1BLAQIVAwoAAAAAAGeEJU0AAAAAAAAAAAAAAAAJAAwAAAAAAAAAAED9QZcAAABfX01BQ09TWC9VWAgAQpWPW0KVj1tQSwECFQMUAAgACABWhCVNDJNublwAAACwAAAAEwAMAAAAAAAAAABApIHOAAAAX19NQUNPU1gvLl9pbmRleC5weVVYCABClY9bI5WPW1BLBQYAAAAAAwADANIAAAB7AQAAAAA%3D
```

Then, create a function using the generated content in Base64 encoding:
```
$ tccli scf CreateFunction --FunctionName testclifunc --Handler index.main --Runtime Python2.7 --Code '{"ZipFile":"UEsDBBQACAAIAFaEJU0AAAAAAAAAAAAAAAAIABAAaW5kZXgucHlVWAwAQpWPWyOVj1v2ARQAU07OT8nMS7ctLUnTteDiSklNU8hNzMzTSC1LzSvRUUjOzytJrSjRtOJSAIKCosy8Eg2ljNScnHyF8vyinBQlTSQJsB6IQFFqSWlRngJYhAsAUEsHCAg25ABRAAAAZAAAAFBLAwQKAAAAAABnhCVNAAAAAAAAAAAAAAAACQAQAF9fTUFDT1NYL1VYDABClY9bQpWPW%2FYBFABQSwMEFAAIAAgAVoQlTQAAAAAAAAAAAAAAABMAEABfX01BQ09TWC8uX2luZGV4LnB5VVgMAEKVj1sjlY9b9gEUAGNgFWNnYGJg8E1MVvAPVohQgAKQGAMnEBsBcR0Qg%2FgbGIgCjiEhQVAmSMcCIBZAU8KIEJdKzs%2FVSywoyEnVy0ksLiktTk1JSSxJVQ4IBik0mtofDaIPhAvogWgAUEsHCAyTbm5cAAAAsAAAAFBLAQIVAxQACAAIAFaEJU0INuQAUQAAAGQAAAAIAAwAAAAAAAAAAECkgQAAAABpbmRleC5weVVYCABClY9bI5WPW1BLAQIVAwoAAAAAAGeEJU0AAAAAAAAAAAAAAAAJAAwAAAAAAAAAAED9QZcAAABfX01BQ09TWC9VWAgAQpWPW0KVj1tQSwECFQMUAAgACABWhCVNDJNublwAAACwAAAAEwAMAAAAAAAAAABApIHOAAAAX19NQUNPU1gvLl9pbmRleC5weVVYCABClY9bI5WPW1BLBQYAAAAAAwADANIAAAB7AQAAAAA%3D"}'

{
    "RequestId": "296275c4-d45f-41d4-b5c2-4ffd4156f783"
}

```

### Creating a Function with COS

The sample below creates a function using a zip package in a COS bucket.
To create a function with COS, you need to authorize the corresponding bucket to the SCF platform, so that the platform can access the code file and download it after authorization.
You can create a function in the console and upload the code from a bucket, and the system will automatically complete the authorization in the frontend.
If you have never created a function in the console, you can set bucket authorization by yourself so that the SCF platform can access the code file. For more information, see [Permission Management](https://cloud.tencent.com/document/product/583/18014).

First, upload the zip package named hello.zip to the bucket named gzcode in the same region, and then create the function using the following command:
```
$ tccli scf CreateFunction --FunctionName testclifunc --Handler index.main --Runtime Python2.7 --Code '{"CosBucketName":"gzcode","CosObjectName":"/hello.zip"}'

{
    "RequestId": "59b6c32f-56e2-4322-b81d-f6ab910f5265"
}

```
