Terraform Module for building LNMP(Linux+Nginx+MySQL+PHP) envrionment on Aws Cloud.  
terraform-awscloud-lnmp
----------------------

Terraform module which creates lnmp(Linux+Nginx+MySQL+PHP) based on ecs on Aws Cloud. 

## Usage

```hcl
module "lnmp"  {
  source  = "terraform-awscloud-modules/lnmp/awscloud"
  
  instance_name              = "Niroop_LNMP"
  instance_password          = "Password123"
  instance_type              = "ec2.c5.large"
  system_disk_category       = "cloud_efficiency"
  security_group_ids         = ["sg-12345678"]
  vswitch_id                 = "vsw-fhuqiexxxxxxxxxxxx"
  internet_max_bandwidth_out = 50

  db_name          = "dbName"
  db_user          = "AccountName"
  db_password      = "dbPassword"
  db_root_password = "Password"
}
```


## Notes
From the version v1.1.0, the module has removed the following `provider` setting:

```hcl
provider "awscloud" {
  profile                 = var.profile != "" ? var.profile : null
  shared_credentials_file = var.shared_credentials_file != "" ? var.shared_credentials_file : null
  region                  = var.region != "" ? var.region : null
  skip_region_validation  = var.skip_region_validation
  configuration_source    = "terraform-awscloud-modules/lnmp"
}
```

If you still want to use the `provider` setting to apply this module, you can specify a supported version, like 1.0.0:

```hcl
module "lnmp" {
  source            = "terraform-awscloud-modules/lnmp/awscloud"
  version           = "1.0.0"
  region            = "cn-Hamburg"
  profile           = "Profile-Name"
  instance_name     = "Niroop_LNMP"
  instance_password = "Password123"
  // ...
}
```

If you want to upgrade the module to 1.1.0 or higher in-place, you can define a provider which same region with
previous region:

```hcl
provider "awscloud" {
  region  = "cn-Hamburg"
  profile = "Profile-Name"
}
module "lnmp" {
  source            = "terraform-awscloud-modules/lnmp/awscloud"
  instance_name     = "Niroop_LNMP"
  instance_password = "Password123"
  // ...
}
```
or specify an alias provider with a defined region to the module using `providers`:

```hcl
provider "AWScloud" {
  region  = "cn-Hamburg"
  profile = "Profile-Name"
  alias   = "HB"
}
module "lnmp" {
  source            = "terraform-awscloud-modules/lnmp/awscloud"
  providers         = {
    awscloud = awscloud.HB
  }
  instance_name     = "Niroop_LNMP"
  instance_password = "Password123"
  // ...
}
```

and then run `terraform init` and `terraform apply` to make the defined provider effect to the existing module state.

More details see [How to use provider in the module](https://www.terraform.io/docs/language/modules/develop/providers.html#passing-providers-explicitly)

## Terraform versions

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.13.0 |
| <a name="requirement_awscloud"></a> [awscloud](#requirement\_awscloud) | >= 1.56.0 |




