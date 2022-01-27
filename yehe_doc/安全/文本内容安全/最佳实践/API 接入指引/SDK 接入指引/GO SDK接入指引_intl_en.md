## Supported Environments

- Go 1.9 or above (Go 1.14 is required if `go mod` is used). Plus, the necessary environment variables such as `GOPATH` should be set properly.

- Endpoint: tms.tencentcloudapi.com

  >! The API supports access from either a nearby region (at `tms.tencentcloudapi.com`) or a specified region (at `tms.ap-guangzhou.tencentcloudapi.com` for Guangzhou, for example). 

## Installing SDK for Go

### Method 1. Install through go get (recommended)

We recommend you use a Tencent Cloud mirror for faster download:

| System Platform      | Command                                         |
| :------------ | :----------------------------------------------- |
| Linux / macOS | `export GOPROXY=https://mirrors.tencent.com/go/` |
| Windows       | `set GOPROXY=https://mirrors.tencent.com/go/`    |

Starting from v1.0.170, you can download packages by product. You only need to download the basic package and the corresponding product package (such as CVM) instead of downloading the packages of all Tencent Cloud products, which speeds up the image build and compilation. Of course, you can also download the packages of all products at once in the same way as before.

>?
>- On-Demand installation method: you can only use the **Go Modules** mode for dependency management; that is, the environment variable `GO111MODULE` should be `auto` or `on`, and `go mod init xxx` should be executed in your project . If you use `GOPATH`, see the full installation method.
>- Full installation method: it supports both `GOPATH` and `Go Modules`.

<table>
  <tr>
     <td colspan="1" width=150>Installation Method</td>
     <td colspan="1" width=250>Description</td>
     <td colspan="1">Command</td>
  </tr>
  <tr>
     <td rowspan="2">On-demand installation (recommended)</td>
     <td colspan="1">Install the common basic package</td>
     <td colspan="1">go get -v -u github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common</td>
  </tr>
  <tr>
     <td colspan="1">Install the corresponding service package (such as CVM)</td>
     <td colspan="1">go get -v -u github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/cvm</td>
  </tr>
  <tr>
     <td colspan="1">Full installation</td>
     <td colspan="1">Download the packages of all Tencent Cloud services at once</td>
     <td colspan="1">go get -v -u github.com/tencentcloud/tencentcloud-sdk-go</td>
  </tr>
  <tr>
</table>

>?In order to support `go mod`, the SDK version number has been reduced from v3.x to v1.x, and all tags of `v3.0.*` and `3.0.*` were removed on May 10, 2021. If you need to backtrack previous tags, refer to the `commit2tag` file in the root directory of the project.

### Method 2. Install through source package

Go to the [GitHub](https://github.com/tencentcloud/tencentcloud-sdk-go) or [Gitee](https://gitee.com/tencentcloud/tencentcloud-sdk-go) code hosting page to download the latest code, decompress, and install it in the `$GOPATH/src/github.com/tencentcloud` directory.

## Using SDK

See the sample code below, which calls the `TextModeration` API. The `region` is configured as `Guangzhou` as an example and should be configured as needed.

```
package main
import ("fmt"
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/errors"
    "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/profile"
    tms "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/tms/v20201229") func main() {
    credential: = common.NewCredential("SecretId", "SecretKey", ) cpf: = profile.NewClientProfile() cpf.HttpProfile.Endpoint = "tms.tencentcloudapi.com"
    client,
    _: = tms.NewClient(credential, "ap-guangzhou", cpf) request: = tms.NewTextModerationRequest() response,
    err: = client.TextModeration(request) if _,
    ok: = err.( * errors.TencentCloudSDKError);ok {
        fmt.Printf("An API error has returned: %s", err) return
    }
    if err != nil {
        panic(err)
    }
    fmt.Printf("%s", response.ToJsonString())
}
```