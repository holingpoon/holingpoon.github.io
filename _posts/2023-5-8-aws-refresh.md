---
layout: post
title: AWS Can't Refresh
---

I feel sad. Specifically, how AWS needs a full window reload in order to show updated information on most things.

Another day at the land of Terraform, I updated an existing IAM policy so I can remove some of the permissions that are too broad.

After `terraform apply` was successful. Reloading the IAM list updates the policy, 
but when you're inside the policy page...the changes does not show up until you refresh the browser window.

That's it, I got nothing.
