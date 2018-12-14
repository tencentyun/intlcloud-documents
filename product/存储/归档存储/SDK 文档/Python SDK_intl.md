## Preparations for Development

The Python SDK contains all the APIs for accessing and working with CAS.

### Related resources

[GitHub Address](https://github.com/tencentyun/cas_python_sdk). Welcome to share codes and report problems.


### Environment dependencies
Python 2.7


### Install SDK
There are two ways to install the SDK: installation using pip and manual installation.

**1. Installation using pip**

	pip install cassdk

**2. Manual installation**

Download the source code from [GitHub Address](https://github.com/tencentyun/cas_python_sdk) and install it manually via setup:

    python setup.py install
### Configure SDK

To use API services in CAS, get appid, secret_id, and secret_key from [here](https://console.cloud.tencent.com/capi).

```Python

	# Before using CAS APIs, initialize a client object for CAS, including information needed for the client to access CAS, and encapsulate the http API at the underlying layer.
    client = CASClient(host, appid, secret_id, secret_key) # host:host stands for the domain name, not the host IP or host name. For example: cas.ap-chengdu.myqcloud.com

    response = client.list_vaults()                       # Return HttpResponse
    ...

    # To use high-level APIs, initialize the CAS API objects with client.
    cas_api = CasAPI(client)
    cas_response = cas_api.list_vaults()                  # Return CASResponse type
    ...
```

### Uninstall SDK

Delete package with pip uninstall

## Low-Level API Description

All the Http APIs, including vault operations, archive operations, and job operations, are encapsulated in the CASClient class.
Since CASClient encapsulates the basic Http APIs, the HTTPRESPONSE type is returned for all the APIs, which makes it easy to get the header, status, and body of the response.

**The low-level APIs and high-level APIs share the same methods and signatures. The response types depend on APIs. For specific responses, see [API documentation](/document/product/572/8742).**

## High-Level API Description

CAS high-level APIs encapsulate the low-level APIs. The core class is CasAPI. It provides synchronous blocking calls and exception throwing for all the basic APIs.

Based on the CasAPI class, classes of vault, archive, and job are created for different objects, making it easy to call APIs for vault operations, archive operations and job operations. The following is a detailed description of the high-level APIs.

### CASAPI class

The CASAPI class is a high-level abstraction of low-level APIs. It shares the same method signature with the CASClient class, except that all methods are synchronous blocking calls and throw exceptions (mainly CASERERERRROR and CASCLIENTRROR). CASRESPONSE is returned for the class, and you can get the fields in the response body by using operations of the lexicographical class. (For specific fields, see the responses for different methods in the HTTP API manual)

Each CASAPI object needs to be initialized with the correct CASClient object.

### Vault class

The vault class encapsulates all the basic vault operations, including Create Vault, Delete Vault, Upload Archives to Vault, and Delete Archives from Vault. In addition, you can also get the metadata of vault objects in member variables of the vault class object.

#### Member variables

| Member Variable | Variable Type | Variable Description |
| ------------------- | ------ | ---------------------------------------- |
| creation_date | string | The UTC date when the vault was created. It is in an ISO 8601 date format, for example, 2017-03-20T17:03:43.221Z. |
| last_inventory_date | string | The UTC date when CAS completed the last vault inventory. It is in an ISO 8601 date format, for example, 2017-03-20T17:03:43.221Z. |
| number_of_archives | int | The number of archives in the vault as per the last vault inventory. This field will return 0 if an inventory has not yet run on the vault. |
| size                | int    | The total size in bytes of the archives in the vault as of the last inventory date. This field will return 0 if an inventory has not yet run on the vault. |
| qcs                 | string | The resource name of the vault |
| name                | string | The vault name that was specified at creation time |

#### Construction method

Method signature: Vault(cas_api, vault_props)
Parameter description:

| Parameter | Type | Description | Required |
| ----------- | ----------- | -------------------------------------- | ---- |
| cas_api     | CasAPI      | The CasAPI object that was successfully initialized | Yes    |
| vault_props | CASResponse | The attribute information of a vault. You can get it by calling describe_vault in the CasAPI class | Yes |

#### Class method

All class methods can be called using **Vault. method signature**, and each method needs to pass in the initialized CasAPI object cas_api.

##### Create a vault

Method signature: `create(cas_api, name)`

Function description: Creates a vault named "name"

Parameter description:

| Parameter Name | Type | Description | Required |
| ------- | ------ | --------------- | ---- |
| cas_api     | CasAPI      | The CasAPI object that was successfully initialized | Yes    |
| name                | string | The vault name that was specified at creation time | Yes |

Response: if the creation is successful, the created vault object is returned. Otherwise, an exception is thrown (See exception description for details).


##### 2. Query a vault
Method signature: `get_vault_by_name(cas_api, vault_name)`
Function description: Gets the vault object according to the vault name
Parameter description:

| Parameter Name | Type | Description | Required |
| ---------- | ------ | --------- | ---- |
| cas_api     | CasAPI      | The CasAPI object that was successfully initialized | Yes    |
| vault_name | string | The name of the vault to get | Yes    |

Response: if the operation is successful, the vault object is returned. Otherwise, an exception is thrown (See exception description for details).

##### Delete a vault

Method signature: delete_vault_by_name(cas_api, vault_name)
Function description: Deletes the vault with the specified name
Parameter description:

| Parameter Name | Type | Description | Required |
| ---------- | ------ | --------- | ---- |
| cas_api     | CasAPI      | The CasAPI object that was successfully initialized | Yes    |
| vault_name | string | The name of the vault to delete | Yes    |

Response: If the deletion is successful, the CasResponse type response is returned with a status value of 2XX and no content is returned. Otherwise, an exception is thrown (See exception description for details).

##### List vaults

Method signature: list_all_vaults(cas_api)
Function description: Lists all the vaults owned by the current account
Parameter description:

| Parameter Name | Type | Description | Required |
| ------- | ------ | ---- | ---- |
| cas_api     | CasAPI      | The CasAPI object that was successfully initialized | Yes    |

Response: If the call is successful, the list of vaults is returned. Otherwise, an exception is thrown (See exception description for details).


#### Member method


##### Retrieve the archive

Method signature: get_archive(archive_id)
Method description: Gets the archive object with the specified ID
Parameter description:

| Parameter Name | Type | Description | Required |
| ---------- | ------ | ------------- | ---- |
| archive_id | string | The ID of the archive to get | yes |

Response: The archive object with the specified ID.
**Note**: This method does not guarantee the validity of archive_id. If the actual archive_id is invalid, all subsequent operations based on the returned archive object will fail.

##### Retrieve some archives

Method signature: retrieve_archive(archive_id, desc, byte_range, tier)
Method description: Retrieves archives
Parameter description:

| Parameter Name | Type | Description | Required |
| ---------- | ------ | ---------------------------------------- | ---- |
| archive_id | string | The ID of the archive to retrieve | yes |
| desc | string | Description of the retrieval job | no |
| byte_range | string | The range of bytes of the retrieval archive. The format is "StartByteValue-EndByteValue". If this field is not specified, the entire archive is retrieved. | No |
| tier       | string | Archive retrieval type. Enumerated values: Expedited, Standard, Bulk. It is Standard by default. | No |

Response: If the call is successful, a job object of the archive-retrieval type is returned. Otherwise, an exception is thrown (See exception description for details).

##### Get the archive inventory

Method signature: initiate_retrieve_inventory(desc)
Method description: Retrieves the archive inventory
Parameter description:

| Parameter Name | Type | Description | Required |
| ---- | ------ | ------- | ---- |
| desc | string | Description of the retrieval job | no |

Response: If the call is successful, a job object of the inventory-retrieval type is returned. Otherwise, an exception is thrown (See exception description for details).

##### Upload an archive

Method signature: upload_archive(file_path, desc)
Method description: Uploads archives from the local file system
Parameter description:

| Parameter Name | Type | Description | Required |
| ---- | ------ | --------------------------- | ---- |
| desc | string | The description of the archive. It is returned when the archive is read. | No |

##### Delete the archive

Method signature: delete_archive(archive_id)
Method description: Deletes the archive
Parameter description:

| Parameter Name | Type | Description | Required |
| ---------- | ------ | -------------- | ---- |
| archive_id | string | The ID of the archive to delete | yes |

Response: If the deletion is successful, the CasResponse type response is returned with a status value of 2XX. Otherwise, an exception is thrown (See exception description for details).

##### Get multipart upload

Method signature: list_all_multipart_uploads()
Method description: Lists all the uploaded data chunks under the current vault
Parameter description: none

Response: if the call is successful, a list of all data uploaded chunks is returned

##### Get multipart list

Method signature: get_multipart_uploader(upload_id)
Method description: Gets a multipart upload object that is in process
Parameter description:

| Parameter Name | Type | Description | Required |
| --------- | ------ | --------------------- | ---- |
| upload_id | string | Upload ID of the multipart upload in process| Yes    |

Response: If the call is successful, a MultipartUpload object is returned. Otherwise, an exception is thrown (See exception description for details).

##### Delete a vault

Method signature: delete()
Method description: Deletes the vault tagged by the current vault object
Parameter description: none

Response: If the call is successful, CASResponse is returned with a status value of 2XX. Otherwise, an exception is thrown (See exception description for details).


### Archive class

The archive class encapsulates all the basic APIs for archives, including archive retrieval and archive deletion.

#### Member variables

| Member Variable | Variable Type | Variable Description |
| ---------- | ------ | ----------------- |
| vault      | Vault  | The vault object to which the archive belongs |
| archive_id | string | Archive ID |

#### Construction method

Method signature: Archive(vault, archive_id)
Parameter description:

| Parameter Name | Type | Description | Required |
| ---------- | ------ | ----------------- | ---- |
| vault      | Vault  | The vault object to which the archive belongs | Yes |
| archive_id | string | Archive ID | Yes |

#### Member method

##### Get a vault

Method signature: get_vault()
Method description: Gets the vault object to which the current archive belongs
Parameter description: none

Response: If the call is successful, the vault object to which the current archive belongs is returned.

##### Initiate archive retrieval

Method signature: initiate_archive_retrieval(desc, byte_range, tier)
Method description: Initiates an archive retrieval job
Parameter description:

| Parameter Name | Type | Description | Required |
| ---------- | ------ | ---------------------------------------- | ---- |
| desc | string | Description of the retrieval job | no |
| byte_range | string | The range of bytes of the retrieval archive.
| tier       | string | Archive retrieval type. Enumerated values: Expedited, Standard, Bulk. It is Standard by default. | No |

Response: If the call is successful, a retrieval job is returned. Otherwise, an exception is thrown (See exception description for details).


### Job class

#### Member variables

| Member Variable | Variable Type | Variable Description |
| --------------- | ------ | ---------------------------------------- |
| id              | string | Job ID  |
| archive_id      | string | The archive ID requested for an archive retrieval job |
| archive_size    | int    | Size of the archive retrieved in the request |
| archive_etag    | string |  The SHA256 tree hash of the entire archive for an archive retrieval job                 |
| description | string | Job description |
| job_range       | string | The retrieved byte range for archive retrieval jobs in the form "StartByteValue-EndByteValue". If you don't specify a range in the archive retrieval, then the whole archive is retrieved.
| creation_date   | string | The UTC time that the job was created. It is in an ISO 8601 date format, for example, 2013-03-20T17:03:43.221Z. |
| completed       | bool   |  It is True if the job is completed. Otherwise, it is False |
| completion_date | string | The UTC time that the job was completed. It is in an ISO 8601 date format, for example, 2013-03-20T17:03:43.221Z. |
| status_code     | string | Job status code. Enumerated values: Succeeded, Failed or InProgress |
| status_message  | string | Job status message |
| tier       | string | The type of the archive retrieval job. Enumerated values: Expedited, Standard, Bulk |
| inventory_size  | int    | Size (in bytes) of the inventory associated with the request of archive inventory retrieval jobs |

#### Construction method

Method signature: Job(vault,cas_response)
Parameter description:

| Parameter Name | Type | Description | Required |
| ------------ | ----------- | -------------------------------- | ---- |
| vault | Vault | | Yes |
| cas_response | CASResponse | The object of the CASResponse type returned after describe_job is called | Yes    |


#### Class method

##### Modify the part size

Method signature: calc_part_size(size_total)
Method description: Calculates the size of each part of a file with a size of size_total
Parameter description:

| Parameter Name | Type | Description | Required |
| ---------- | ------ | --------- | ---- |
| size_total | string | Total size of the file to be segmented | Yes    |

Response: If the call is successful, the size of each part is returned. Otherwise, an exception is thrown (See exception description for details).


#### Member method

##### Get part of the file from the output

Method signature: download_by_range(byte_range, file_path, file_obj, chunk_size, block)
Method description: Downloads the contents within the specified range of bytes to the file
Parameter description:

| Parameter Name | Type | Description | Required |
| ---------- | ------ | ---------------------------------------- | ---------------------------- |
| byte_range | string | The range of bytes of the retrieval file | Yes |
| file_path  | string | File download path | file_path and file_obj cannot be None at the same time |
| file_obj   | file   | The file object to be downloaded | file_path and file_obj cannot be None at the same time |
| chunk_size | int    | The size of each chunk per read/write. It is 1 MB by default. | No |
| block      | bool   | The calling mode of the method. "True" means synchronous blocking call. "False" means asynchronous call. If the job is not completed, a DownloadArchiveError exception is thrown. | No |

Response: None If the call fails, an exception is thrown (See exception description for details).

##### Get the entire file from the output

Method signature: download_to_file(file_path, chunk_size, block)
Method description: Downloads the job output to a specified file path
Parameter description:

| Parameter Name | Type | Description | Required |
| ---------- | ------ | ---------------------------------------- | ---- |
| file_path  | string | The path to download the file | Yes |
| chunk_size | int    | The size of each chunk per read/write. It is 1 MB by default. | No |
| block      | bool   | The calling mode of the method. "True" means synchronous blocking call. "False" means asynchronous call. If the job is not completed, an DownloadArchiveError exception is thrown. It is synchronous blocking call by default.|  No |

Response: None If the call fails, an exception is thrown (See exception description for details).

### Response type

CASResponse is the Dict type of HTTPResponse. You can directly use the dict operator to get the response field. CASResponse is returned for all CasAPIs. CASResponse is also a parameter type of response returned when you initialize a vault, job or MultipartUpload by calling the describe method.

**Example**

```
cas_response = cas_api.create_vault("vault-name")
vault_props = cas_api.describe("vault-name")
vault = Vault(cas_api, vault_props)
```

