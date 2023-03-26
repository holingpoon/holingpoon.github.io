---
layout: post
title: NodeJS subscribe
---

Another interesting find during the run on [Advanced Terraform](https://www.linkedin.com/learning/advanced-terraform-2020) tutorials.

Tutorials are meant to tell you about happy paths. Here's what happens when it doesn't happen.

```
$ terraform apply s1.tfplan
...
...
Error: creating EC2 Instance: OptInRequired: In order to use this AWS Marketplace product you need to accept terms and subscribe. To do so please visit https://aws.amazon.com/marketplace/pp?sku=4fs14t8jg3y3nw7z5145rlg3n
```

AWS actually requires you to subscribe to "NodeJS 8 Web Stack" so you can keep building. Proceed with the link and click on subscribe. No need to hit "Continue to Configuration" button, we are not building resources via the UI.

But the terraform plan would turn stale, so we'll need to run the following again.

```
$ terraform plan -out=s1.tfplan
$ terraform apply s1.tfplan
```