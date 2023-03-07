Resources and data sources are basic extensible datasets in Terraform that allow you to manage resources.

## Writing Resources

A resource describes a class of resource entities allowing for CRUD operations, typically CVM instances, disks, databases, TKE clusters, and COS buckets.

This document takes the CVM instance with the following simple configuration as an example:
- Name: `my-cvm`

- AZ: Guangzhou Zone 4

- Model: SA2.MEDUIM2

- Image: TencentOS Server 3.2 (Final)

- Network: `vpc-xxxxxxxx`

- Subnet: `subnet-xxxxyyyy`

- Billing mode: Pay-as-you-go

- Whether a public IP is assigned: Yes

- Public network bandwidth: 10 Mbps


   You can use the high-level configuration syntax HCL for description. Below is the sample code:

   ``` hcl
   resource "tencentcloud_instance" "cvm1" {
     instance_name              = "my-cvm"
     availability_zone          = "ap-guangzhou-4"
     instance_type              = "SA2.MEDIUM2"
     instance_charge_type       = "POSTPAID_BY_HOUR"
     image_id                   = "img-9qrfy1xt"
     allocate_public_ip         = true
     internet_max_bandwidth_out = 10
   }
   ```

   When you run the `terraform apply` command for the first time, the declared resource will initiate the creation process. After the creation, if you modify the configuration in the code and run `terraform apply` again, the update process will be initiated. Running the `terraform destroy` command will initiate the termination process.


### Writing resource code

To make the above HCL code effective, you need to register at TencentCloud Provider, find the `Provider/ResourceMap` field in [tencentcloud/provider.go](https://github.com/tencentcloudstack/terraform-provider-tencentcloud/blob/master/tencentcloud/provider.go), add the `tencentcloud_instance` resource structure, and define the parameter schema based on HCL. Below is the sample code:
``` go
package tencentcloud

import (
  "github.com/hashicorp/terraform-plugin-sdk/helper/schema"
  "github.com/hashicorp/terraform-plugin-sdk/terraform"
)

func Provider() *schema.Provider {
  return &schema.Provider{
    ResourcesMap: map[string]*schema.Resource{
      "tencentcloud_xxx": { /* Other declared resources */ },
      "tencentcloud_yyy": { /* Other declared resources */ },
      "tencentcloud_instance": {
        Schema: map[string]*schema.Schema{
          "instance_name": {
            Optional: true, // Optional field
            Type:     schema.TypeString, // Field type
            Description: "Instance Name.",
          },
          "availability_zone": {
            Required: true, // Required field
            Type:     schema.TypeString,
            ForceNew: true, // If this field is modified and the modification is submitted, the resource will be terminated and recreated, as the server instance cannot switch the AZ.
            Description: "Instance available zone.",
          },
          "instance_type": {
            Optional: true,
            Type:     schema.TypeString,
            Description: "Instance Type.",
          },
          "instance_charge_type": {
            Optional: true,
            Type:     schema.TypeString,
            Description: "Instance charge type.",
          },
          "image_id": {
            Required: true,
            Type:     schema.TypeString,
            Description: "Instance OS image Id.",
          },
          "allocate_public_ip": {
            Optional: true,
            Type:     schema.TypeBool, // Boolean type
            Description: "Specify whether to allocate public IP.",
          },
          "internet_max_bandwidth_out": {
            Optional: true,
            Type:     schema.TypeInt, // Integer type
            Description: "Specify maximum bandwith.",
          },
        },
      },
    },
  }
}
```

After declaring the resource and parameter schema, you also need to define the CRUD logic triggered by `apply`, `plan`, or `destroy` in Terraform. The SDK for Terraform (v1) defines four CRUD methods:
- `Create`, which is called if `terraform apply` is run for creation.

- `Read`, which is called if `terraform plan / import` is run for remote state sync.

- `Update`, which is called if `terraform apply` is run for update.

- `Delete`, which is called if `terraform destroy` is run.


   Add the four methods to the `schema.Resource` structure. Below is the sample code:

   ``` go
   package tencentcloud
   
   import (
     "github.com/hashicorp/terraform-plugin-sdk/helper/schema"
     "github.com/hashicorp/terraform-plugin-sdk/terraform"
   )
   
   func Provider() *schema.Provider {
     return &schema.Provider{
       ResourcesMap: map[string]*schema.Resource{
         "tencentcloud_xxx": { /* Other declared resources */ },
         "tencentcloud_yyy": { /* Other declared resources */ },
         "tencentcloud_instance": {
           Create: resourceTencentCloudInstanceCreate,
           Read:   resourceTencentCloudInstanceRead,
           Update: resourceTencentCloudInstanceUpdate,
           Delete: resourceTencentCloudInstanceDelete,
           Schema: map[string]*schema.Schema{
             // The declaration written above (omitted)
           },
         },
       },
     }
   }
   
   func resourceTencentCloudInstanceCreate (d *schema.ResouceData, m interface{}) error {
     instanceName := d.Get("instance_name").(string)
     instanceType := d.Get("instance_type").(string)
     // ...
     
     // Run `terraform apply` for resource creation
     instanceId := createInstance(&param{
       Name: &instanceName,
       Type: &instanceType,
       // ...
     })
     
     // Set a unique ID for the created resource
     d.SetId(instanceId)
   
     // Sync the remote state again after resource creation for consistency check
     return resourceTencentCloudInstanceRead(d, m)
   }
   
   func resourceTencentCloudInstanceRead (d *schema.ResouceData, m interface{}) error {
     // Run `terraform plan` after resource creation/update
     
     instanceId := d.Id() // The ID set in `Create`
     instanceInfo := getInstance(instanceId)
     
     d.Set("instance_name", instanceInfo.Name)
     d.Set("instance_type", instanceInfo.Type)
     
     return nil
   }
   
   func resourceTencentCloudInstanceUpdate (d *schema.ResouceData, m interface{}) error {
     // Run `terraform apply` to update existing resources
     
     updateParam := &param{}
     
     // Check whether fields are updated, and if not, update them in combinations
     if d.HasChange("instance_name") {
       name := d.Get("instance_name").(string)
       updateParam.Name = &name
     }
     
     if d.HasChange("instance_type") {
       insType := d.Get("instance_type").(string)
       updateParam.Type = &insType
     }
     // ...
     updateInstance(d.Id(), updateParam)
     
     // Sync the remote state again after resource creation for consistency check
     return resourceTencentCloudInstanceRead(d, m)
   }
   
   func resourceTencentCloudInstanceDelete (d *schema.ResouceData, m interface{}) error {
     // Run `terraform destroy`
     destroyInstance(d.Id())
     
     return nil
   }
   ```

   As you can see, the values of the HCL fields can be obtained by referencing the `d.Get` parameter. `d.Set` can write back (sync) these values. In addition, after each resource is created, you need to call `d.SetId` to set the unique resource index by which the specific resource instance can be located.  
After the main logic structure is set up, the four functions can be called after Terraform runs `plan apply destroy`. Then, you can initiate TencentCloud API calls to manipulate resources.
CVM has the following CRUD APIs:

- [RunInstances](https://www.tencentcloud.com/document/product/213/33237): Purchases an instance.

- [DescribeInstances](https://www.tencentcloud.com/document/product/213/33258): Queries the list of instances.

- [ModifyInstancesAttribute](https://www.tencentcloud.com/document/product/213/33246): Modifies an instance attribute.

- [TerminateInstances](https://www.tencentcloud.com/document/product/213/33234): Returns an instance.


   You can pass in the parameters obtained from HCL to the required parameters of the CVM API for call initiation. Below is the sample code:

   ``` go
   package main
   
   import (
     cvm "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/cvm/v20170312"
   )
   
   func resourceTencentCloudInstanceCreate(d *schema.ResourceData, meta interface{}) error {
     // Read the values of the fields from HCL
     instanceName       := d.Get("instance_name").(string)
     instanceType       := d.Get("instance_type").(string)
     imageId            := d.Get("image_id").(string)
     instanceChargeType := d.Get("instance_charge_type").(string)
     zone               := d.Get("availability_zone").(string)
     allocatePublicIp   := d.Get("allocate_public_ip").(bool)
     internetBandWith   := int64(d.Get("internet_max_bandwidth_out").(int))
     
     client, _ := cvm.NewClient(credential, "ap-guangzhou")
     request := cvm.NewRunInstancesRequest()
     // Create the parameters required by CVM in combinations
     request.InstanceName       = &instanceName
     request.InstanceType       = &instanceType
     request.ImageId            = &imageId
     request.InstanceChargeType = &instanceChargeType
     request.Placement          = &cvm.Placement {
       Zone: &zone,
     }
     request.InternetAccessible = &cvm.InternetAccessible {
       InternetMaxBandwidthOut: &internetBandWith,
       PublicIpAssigned:        &allocatePublicIp,
     }
       
     // Initiate the call
     id, err := client.RunInstances(request)
     if err != nil{
       return err
     }
     
     // Set the ID returned by the creation as the resource ID
     d.SetId(id)
     
     // Write back the state
     return resourceTencentCloudInstanceRead(d, meta)
   }
   ```

   After implementing `Create`, implement `Read`, `Update`, and `Delete`:

   ``` go
   package main
   
   import (
     cvm "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/cvm/v20170312"
   )
   
   func resourceTencentCloudInstanceRead(d *schema.ResourceData, meta interface{}) error {
     // The ID set in `Create` or obtained during import
     id := d.Id()
     
     client, _ := cvm.NewClient(credential, "ap-guangzhou")
     request, _ := cvm.NewDescribeInstancesRequest()
     request.InstanceIds = []*string{&id}
     response, err := client.DescribeInstances(request)
     if err != nil{
       return err
     }
     if len(response.Response.InstanceSet) == 0 {
       return fmt.Errorf("instance %s not exists.", id)
     }
     instance := response.Response.InstanceSet[0]
     
     d.Set("instance_name", instance.InstanceName)
     d.Set("instance_type", instance.InstanceType)
     // `d.Set` writes back fields such as `image_id`, `instance_charge_type`, and `availability_zone` (omitted).
     
     return nil
   }
   
   func resourceTencentCloudInstanceUpdate(d *schema.ResourceData, meta interface{}) error {
     id := d.Id()
     client, _ := cvm.NewClient(credential, "ap-guangzhou")
     request, _ := cvm.NewModifyInstancesAttributeRequest()
     request.InstanceIds = []*string{&id}
   
     // Check whether the fields are changed and add the parameters
     if d.HasChange("instance_name") {
       name := d.Get("instance_name").(string)
       request.InstanceName = &name
     }
     
     // Process other `HasChange` fields (omitted)
     
     _, err := client.ModifyInstanceAttribute(request)
     if err != nil{
       return err
     }
     
     return resourceTencentCloudInstanceRead(d, meta)
   }
   
   func resourceTencentCloudInstanceDelete(d *schema.ResourceData, meta interface{}) error {
     id := d.Id()
   
     client, _ := cvm.NewClient(credential, "ap-guangzhou")
     request, _ := cvm.NewTerminateInstancesRequest()
     request.InstanceIds = []*string{&id}
     _, err := client.TerminateInstances(request)
     if err != nil{
       return err
     }
     return nil
   }
   ```

   At this point, you have implemented the resource containing the name, field declaration, and CRUD logic in TencentCloud Provider.


### Implementing the import logic

After implementing the resource CRUD successfully, you can implement the resource import logic. The command for importing a single resource is in the format of `terraform import <type>.<index> <id>`, such as:
``` bash
terraform import tencentcloud_instance.cvm1 ins-abcd1234
```

As you can see, there is only the `ins-abcd1234` input for resource import. As indicated in the implemented `Read` method, when the ID is specified, you can use the ID to query the detailed configuration of a remote resource and automatically sync the configuration locally. Therefore, you only need to declare `Importer` in `schema.Resource` to indicate that the resource can be imported. Further sync will be taken over by `Read`:
``` go
package tencentcloud

import (
  "github.com/hashicorp/terraform-plugin-sdk/helper/schema"
  "github.com/hashicorp/terraform-plugin-sdk/terraform"
)

func Provider() *schema.Provider {
  return &schema.Provider{
    ResourcesMap: map[string]*schema.Resource{
      "tencentcloud_xxx": { /* Other declared resources */ },
      "tencentcloud_yyy": { /* Other declared resources */ },
      "tencentcloud_instance": {
        Create: resourceTencentCloudInstanceCreate,
        Read:   resourceTencentCloudInstanceRead,
        Update: resourceTencentCloudInstanceUpdate,
        Delete: resourceTencentCloudInstanceDelete,
        Schema: map[string]*schema.Schema{
          // The declaration written above (omitted)
        },
        // In most cases, you only need to add `schema.ImportStatePassthrough`.
        Importer: &schema.ResourceImporter{
          State: schema.ImportStatePassthrough,
        },
      },
    },
  }
}
```

## Data Source

Data sources represent read-only entities for query only. No matter how many times they are called, existing resources will not be affected, such as CVM instance list, image list, AZ list, database list, parameter template, and audit log. Theoretically, any data that can be found via APIs are data sources. As indicated above, the CVM image is displayed as `TencentOS Server 3.2 (Final)`, but the parameter passed in to the API is its ID `img-9qrfy1xt`. To get the ID based on the image name, you can use the data source to query and reference the image ID:
``` javascript
data "tencentcloud_images" "fav_os" {
  filters = {
    image_name: "TencentOS Server 3.2",
    image_type: "PUBLIC_IMAGE"
  }
}

resource "tencentcloud_instance" "cvm1" {
  image_id = data.tencentcloud_images.fav_os.images.0.image_id
}
```

As shown above, write `image_id` into the reference of `data.tencentcloud_images.fav_os`. Then, Terraform will read the data source information first and then calculate the value. Compared to a static method, a data source can effectively organize resources with dependencies.

### Writing a data source

A data source is implemented in a similar way to a resource. You need to register at TencentCloud Provider, find the `Provider/DataSourceMap` field in the source code of [tencentcloud/provider.go](https://github.com/tencentcloudstack/terraform-provider-tencentcloud/blob/master/tencentcloud/provider.go), add the `tencentcloud_images` structure (the names of all data sources must end with `s`), and define the parameter schema based on HCL:
``` go
package tencentcloud

import (
  "github.com/hashicorp/terraform-plugin-sdk/helper/schema"
  "github.com/hashicorp/terraform-plugin-sdk/terraform"
)

func Provider() *schema.Provider {
  return &schema.Provider{
    DataSourceMap: map[string]*schema.Resource{
      "tencentcloud_xxxs": { /* Other declared data sources */ },
      "tencentcloud_yyys": { /* Other declared data sources */ },
      "tencentcloud_images": {
        Schema: map[string]*schema.Schema{
          "filters": {
            Optional: true,
            Type:     schema.TypeMap, // Specify the `Map` type
            Description: "Query filter",
          },
          // Saves the result in JSON locally
          // TencentCloud Provider requires that every data source should have `result_output_file`.
          "result_output_file": {
            Optional: true,
            Type: schema.TypeString,
            Description: "Used for store as local file.",
          },
          "result": {
            Computed: true, // `Computed` indicates that the field will be updated passively.
            Type:    schema.TypeList,
            Description: "",
            Elem: &schema.Resource{
              Schema: map[string]*schema.Schema{
                "id": {
                  Type: schema.TypeString,
                  Computed: true,
                  Description: "Image Id.",
                },
                "name": {
                  Type: schema.,
                  Computed: true,
                  Description: "Image name.",
                },
              },
            },
          },
        },
      },
    },
  }
}

```

Compared to a resource, a data source requires implementing only the `Read` method:
``` go
package tencentcloud

import (
  "encoding/json"
  "github.com/hashicorp/terraform-plugin-sdk/helper/schema"
  "github.com/hashicorp/terraform-plugin-sdk/terraform"
)

const ImgNameFilterKey = "image-name"

func Provider() *schema.Provider {
  return &schema.Provider{
    DataSourceMap: map[string]*schema.Resource{
      "tencentcloud_xxxs": { /* Other declared data sources */ },
      "tencentcloud_yyys": { /* Other declared data sources */ },
      "tencentcloud_images": {
        Schema: map[string]*schema.Schema{ /* Omitted */},
        Read: func(d *schema.ResourceData, meta interface{}) {
          // Declare the `Client` and `request`
          client, _ := cvm.NewClient(credential, "ap-guangzhou")
          request := cvm.NewDescribeImagesRequest()
          
          // Get `Filters` of `Map` type
          filters := d.Get("filters").(map[string]interface{})
          
          // Check `filters["name"]` and add parameters
          if name, ok := filters["name"].(string); ok {
            request.Filters = append(request.Filters, &cvm.Filter{
              Name: &ImgNameFilterKey,
              Values: []*string{&name}
            })
          }
          
          // Initiate the call
          response, err := client.DescribeImages(request)
          if err != nil{
            return err
          }
          
          // Assemble and write the `result` field
          imageSet := response.Response.ImageSet
          result := make([]map[string]interface{}, 0, len(imageSet))
          for i := range imageSet {
            item := imageSet[i]
            result = append(result, map[string]interface{}{
              "id": *item.Id,
              "name": *item.Name,
            })
          }
          d.Set("result", result)
          
          // If `result_output_file` has a definition, write the result into the specified file.
          if v, ok := d.GetOk("result_output_file"); ok {
            writeToFile(v.(string), result)
          }
          return nil
        }
      },
    },
  }
}

```

At this point, you have written the `tencentcloud_images` and can use the data source to query specified OS images.

## Writing an Acceptance Test

To ensure that your newly added resource or data source can work properly, you need to write an acceptance test as instructed in [Writing Test Case](https://www.tencentcloud.com/document/product/1172/52381).