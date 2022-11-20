terraform-awscloud-lnmp
=====================================================================

本 Terraform EC2 lnmp(Linux+Nginx+MySQL+PHP)。


```hcl
module "lnmp"  {
  source  = "terraform-awscloud-modules/lnmp/awscloud"
  
  instance_name              = "Niroop_LNMP"
  instance_password          = "YPassword123"
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

```hcl
provider "awscloud" {
  profile                 = var.profile != "" ? var.profile : null
  shared_credentials_file = var.shared_credentials_file != "" ? var.shared_credentials_file : null
  region                  = var.region != "" ? var.region : null
  skip_region_validation  = var.skip_region_validation
  configuration_source    = "terraform-awscloud-modules/lnmp"
}
```

```hcl
module "lnmp" {
  source            = "terraform-awscloud-modules/lnmp/awscloud"
  version           = "1.0.0"
  region            = "cn-Hamburg"
  profile           = "Profile-Name"
  instance_name     = "Nirop_LNMP"
  instance_password = "Password123"
  // ...
}
```

provider：
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
provider：

```hcl
provider "awscloud" {
  region  = "cn-Hamburg"
  profile = "-Profile-Name"
  alias   = "HB"
}
module "lnmp" {
  source            = "terraform-awscloud-modules/lnmp/awscloud"
  providers         = {
    alicloud = awscloud.HB
  }
  instance_name     = "Niroop_LNMP"
  instance_password = "Password123"
  // ...
}
```

provider, terraform init,terraform apply, provider,



