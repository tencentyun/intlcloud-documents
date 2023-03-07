An open-source project requires maintaining a user-friendly and readable `CHANGELOG.md` so that users can quickly know whether they will be affected by the version and assess the upgrade risk if applicable.

You need to submit a `.txt` change file to the `.changelog` directory to describe the change when sending a pull request. The file will then be parsed via the [go-changelog](https://github.com/hashicorp/go-changelog) tool to generate a `CHANGELOG.md` file subject to the following update rules:

## Changelog Format

### Naming

The changelog involved in the current pull request should be submitted to the `.changelog` directory and named in the format of `{PR-NUMBER}.txt`. For example, if the pull request number is `1326`, the changelog should be named `.changelog/1326.txt`.

![](https://qcloudimg.tencent-cloud.cn/image/document/75448838bcf79eade86de13a4b21b585.png)

### Format

The `changelog.txt` has the following format, where `{HEADER}` is the changelog type, and `{ENTRY}` is the changelog details.
```
   release-note:{HEADER}
{ENTRY}
```

If a pull request contains multiple changelog entries, you can add multiple blocks to the same changelog file as follows:

```
   release-note:bug
resource/tencentcloud_teo_zone: change tag description from zoneName to zoneId.

   release-note:enhancement
resource/tencentcloud_redis_instance: support update `security_groups`.
```


## Changelog Rule Categorization

A changelog presents only changes to the code repository of a specific version affecting the operator. The following are general principles and samples of a change to be recorded in a changelog.

### New resource

The changelog of a new resource should contain only the resource name and be named `release-note:new-resource`.

```
   release-note:new-resource
tencentcloud_postgresql_instance
```


### New data source

The changelog of a new data source should contain only the data source name and be named `release-note:new-data-source`.

```
   release-note:new-data-source
tencentcloud_sqlserver_zone_config
```

### Bug fix

The changelog of a new bug fix should be named `release-note:bug`, with a prefix indicating the corresponding resource or data source, a colon, and a summary.
>?
> Use the `provider` prefix for a provider-level fix.
> 

```
   release-note:bug
resource/tencentcloud_cdn_domain: Fix `https_config` inconsistency after apply
```


### Feature enhancement

The changelog of a new feature enhancement should be named `release-note:enhancement`, with a prefix indicating the corresponding resource or data source, a colon, and a summary.
>?
> Use the `provider` prefix for a provider-level feature enhancement.
> 

```
   release-note:enhancement
resource/tencentcloud_cdn_domain: Support follow redirect and authentication
```



### Feature disuse

The changelog of a feature disuse should be named `release-note:deprecation`, with a prefix indicating the corresponding resource or data source, a colon, and a summary.

>?
> Use the `provider` prefix for a provider-level feature disuse.
> 

``` 
   release-note:deprecation
resource/tencentcloud_kubernetes_cluster: The `as_enabled` attribute is being deprecated.
```


## Situations Requiring No Changelog Submission
- Resource and provider documentation updates

- Test updates

- Code refactoring

