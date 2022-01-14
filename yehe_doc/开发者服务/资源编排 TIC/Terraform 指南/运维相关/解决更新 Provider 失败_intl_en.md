## Error Description
The following error message is returned when a provider is downloaded or updated:
```bash
Initializing the backend...

Initializing provider plugins...
- Checking for available provider plugins on https://releases.hashicorp.com...

Error installing provider "tencentcloud": openpgp: signature made by unknown entity.

Terraform analyses the configuration and state and automatically downloads
plugins for the providers used. However, when attempting to download this
plugin an unexpected error occured.

This may be caused if for some reason Terraform is unable to reach the
plugin repository. The repository may be unreachable if access is blocked
by a firewall.

If automatic installation is not possible or desirable in your environment,
you may alternatively manually install plugins by downloading a suitable
distribution package and placing the plugin's executable file in the
following directory:
    terraform.d/plugins/darwin_amd64

```

## Problem Locating
The update failed due to a lower Terraform version as illustrated at the [official website](https://discuss.hashicorp.com/t/terraform-updates-for-hcsec-2021-12/23570).

## Troubleshooting Procedure
Upgrade Terraform to 0.11.15 or later.
