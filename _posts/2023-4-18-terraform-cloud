---
layout: post
title: Terraform Cloud Fun
---

So...you know what's strange with Terraform Cloud? Terraform Cloud doesn't work with some of the hashicorp/aws module settings. 

For example, Terraform Cloud would complain about not being able to fetch shared configuration file and shared credential file 
when it's specified in the .tf files. Either find a way to upload the shared files onto Terraform Cloud, or just create a
variable set on Terraform Cloud and store the AWS credentials that way. I ended up using the second method, still interested
in figuring out how to get the first way to work.
