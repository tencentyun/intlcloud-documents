
This document describes the directory structure and lifecycle of Terraform TencentCloud Provider.

## Directory Structure
```
├─terraform-provider-tencentcloud                    Root directory
│  ├─main.go                                         Program entry file
│  ├─AUTHORS                                         Author information
│  ├─CHANGELOG.md                                    Change log
│  ├─LICENSE                                         License information
│  ├─debug.tf.example                                Example debugging configuration file
│  ├─examples                                        Directory of example configuration files
│  │  ├─tencentcloud-eip                             Example EIP TF files
│  │  ├─tencentcloud-instance                        Example CVM TF files
│  │  ├─tencentcloud-nat                             Example NAT Gateway TF files
│  │  ├─tencentcloud-vpc                             Example VPC TF files
│  │  └─ ...                                         Directory of more examples
│  ├─tencentcloud                                    Core provider directory
│  │  ├─basic_test.go                                Basic unit test
│  │  ├─config.go                                    Public configuration file
│  │  ├─data_source_tc_availability_zones.go         Availability zone query
│  │  ├─data_source_tc_availability_zones_test.go
│  │  ├─data_source_tc_nats.go                       NAT Gateway list query
│  │  ├─data_source_tc_nats_test.go
│  │  ├─data_source_tc_vpc.go                        VPC query
│  │  ├─data_source_tc_vpc_test.go
│  │  ├─...                                          More data sources
│  │  ├─helper.go                                    Some public functions
│  │  ├─provider.go                                  Core provider file
│  │  ├─provider_test.go
│  │  ├─resource_tc_eip.go                           EIP resource manager
│  │  ├─resource_tc_eip_test.go
│  │  ├─resource_tc_instance.go                      CVM instance resource manager
│  │  ├─resource_tc_instance_test.go
│  │  ├─resource_tc_nat_gateway.go                   NAT Gateway resource manager
│  │  ├─resource_tc_nat_gateway_test.go
│  │  ├─resource_tc_vpc.go                           VPC Gateway resource manager
│  │  ├─resource_tc_vpc_test.go
│  │  ├─...                                          More resource managers
│  │  ├─service_eip.go                               Encapsulated EIP-related service
│  │  ├─service_instance.go                          Encapsulated CVM-instance-related service
│  │  ├─service_vpc.go                               Encapsulated VPC-related service
│  │  ├─...
│  │  ├─validators.go                                Public argument validation function
│  ├─vendor                                          Dependent third-party libraries
│  ├─website                                         Web-Related files
│  │  ├─tencentcloud.erb                             Left sidebar file
│  │  ├─docs                                         Source file directory of Markdown documents
│  │  │  ├─d                                         Data-Related documents (data_source_*)
│  │  │  │  ├─availability_zones.html.md
│  │  │  │  ├─nats.html.markdown
│  │  │  │  ├─vpc.html.markdown
│  │  │  │  ├─...
│  │  │  ├─index.html.markdown
│  │  │  ├─r                                         Resource-Related documents (resource_*)
│  │  │  │  ├─instance.html.markdown
│  │  │  │  ├─nat_gateway.html.markdown
│  │  │  │  ├─vpc.html.markdown
│  │  │  │  └─...
```
The structure is divided into five main parts:

- **main.go**: plugin entry.
- **examples**: example directory, which contains examples that can be used directly.
- **tencentcloud**: plugin directory to store service code, where:
    - `provider.go`: is the plugin root used to describe plugin attributes, such as the configured key, list of supported resources, and callback configuration.
    - `data_source_*.go`: defines some resources for read calls, mainly query APIs.
    - `resource_*.go`: defines some resources for write calls, including APIs for resource CRUD.
    - `service_*.go`: contains some public methods under broad resource categories.
- **vendor**: contains dependent third-party libraries.
- **website**: contains documents as importance as examples.

## Provider Lifecycle

The Terraform execution process is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/b0a1ac2b36b2addb227c9da911760adb.png)

- `1 - 4`: looks for the provider and loads the tencentcloud plugin.
- `5`: reads your configuration file to get the resources you declared and their states.
- `6`: calls different functions (Create/Update/Delete/Read) based on the resource state.
 - **Create**
Terraform determines adding a new resource configuration to a `.tf` file as `Create`.
 - **Update**
Terraform determines modifying one or more arguments of a resource already created in a `.tf` file as `Update`.
 - **Delete**
Terraform determines deleting the resource configuration already created in a `.tf` file or running the `terraform destroy` command as `Delete`.
 - **Read**
`Read` is a resource query operation that checks whether a resource exists and updates the resource attributes locally.
 - **tencentcloud-sdk-go**
`tencentcloud-sdk-go` is a TencentCloud API SDK for Go and used to call TencentCloud APIs for resource management.
