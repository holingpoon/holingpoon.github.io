---
layout: post
title: eb deploy --staged
---

Reference: [eb deploy](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb3-deploy.html)

## On `eb deploy --staged` ##

Elastic Beanstalk has its own command line interface. For deployment, the basic command line is `eb deploy`.

There are many flags to control the deployment. Without any flags, `eb deploy` would refer to the **local** copy of git commit log, and deploy the files listed in the most recent commit, much like results from `git ls-tree -r HEAD --name-only`.

What `eb deploy --staged` does, is to include files that are saved, but not included in the commit log, in the deployment. The `--staged` flag is meant to test out deployments on test servers, to include new features that may not meant to be included into a final version.
