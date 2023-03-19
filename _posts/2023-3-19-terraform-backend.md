---
layout: post
title: Unconfigure S3 Backend in Terraform
---

This is an interesting find.

TLDR; Terraform was looking for backend that's been destroyed in the last tutorial, I ended up manually create S3 bucket so Terraform can unconfigure a previous configuration.


I was working on tutorial on [Advanced Terraform](https://www.linkedin.com/learning/advanced-terraform-2020), 
and I decided to reuse my main directory instead of using indivdual directories per lesson. I ended up running into the following conflict:
```
$ terraform init
Initializing modules...
Downloading registry.terraform.io/terraform-aws-modules/ec2-instance/aws 2.21.0 for ec2_cluster...
- ec2_cluster in .terraform/modules/ec2_cluster

Initializing the backend...
╷
│ Error: Backend configuration changed
│
│ A change in the backend configuration has been detected, which may require migrating
│ existing state.
│
│ If you wish to attempt automatic migration of the state, use "terraform init
│ -migrate-state".
│ If you wish to store the current configuration with no changes to the state, use
│ "terraform init -reconfigure".
```

The interesting part is, running `terraform init -migrate-state` does not help

```
$ terraform init -migrate-state
Initializing modules...

Initializing the backend...
Terraform has detected you're unconfiguring your previously set "s3" backend.
╷
│ Error: Error inspecting states in the "s3" backend:
│     S3 bucket does not exist.
│
│ The referenced S3 bucket must have been previously created. If the S3 bucket
│ was created within the last minute, please wait for a minute or two and try
│ again.
│
│ Error: NoSuchBucket: The specified bucket does not exist
│ 	status code: 404, request id: NPN4KRWC0JM0027C, host id: y5tilULjD1r39XQAftTMsBbEDjxHdHuofU2grV0U5i334GDQhEZZJJ4P/BulEpvR5fB2MC5SsF3boJBXuU3GiA==
│
│
│ Prior to changing backends, Terraform inspects the source and destination
│ states to determine what kind of migration steps need to be taken, if any.
│ Terraform failed to load the states. The data in both the source and the
│ destination remain unmodified. Please resolve the above error and try again.
│
│
╵
```

Turns out that Terraform is looking for the S3 bucket which was deleted at the end of the last exercise in `terraform destroy`. 
I ended up manually recreate the S3 bucket in order to unset the configuration. I found out that information via `terraform plan`

```
$ terraform plan -out=s1.tfplan
╷
│ Error: Backend initialization required, please run "terraform init"
│
│ Reason: Unsetting the previously set backend "s3"
│
│ The "backend" is the interface that Terraform uses to store state,
│ perform operations, etc. If this message is showing up, it means that the
│ Terraform configuration you're using is using a custom configuration for
│ the Terraform backend.
│
│ Changes to backend configurations require reinitialization. This allows
│ Terraform to set up the new configuration, copy existing state, etc. Please run
│ "terraform init" with either the "-reconfigure" or "-migrate-state" flags to
│ use the current configuration.
│
│ If the change reason above is incorrect, please verify your configuration
│ hasn't changed and try again. At this point, no changes to your existing
│ configuration or state have been made.
╵
```

After manual recreation of the S3 bucket, the initialization worked

```
$ terraform init -migrate-state
Initializing modules...

Initializing the backend...
Terraform has detected you're unconfiguring your previously set "s3" backend.


Successfully unset the backend "s3". Terraform will now operate locally.

Initializing provider plugins...
- Reusing previous version of hashicorp/aws from the dependency lock file
- Using previously-installed hashicorp/aws v4.47.0

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

