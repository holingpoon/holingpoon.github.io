---
layout: post
title: eb deploy --staged
---

A cool party trick you can use for `eb deploy`.

Reference: [eb deploy](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb3-deploy.html)

## `eb deploy` ##

Elastic Beanstalk has its own command line interface. For deployment, the basic command line is `eb deploy`.

There are many flags to control the deployment. Without any flags, `eb deploy` would refer to the **local** copy of git commit log, and deploy the files listed in the most recent commit, much like results from `git ls-tree -r HEAD --name-only`.

## `eb deploy --staged` ##

What `eb deploy --staged` does, is to include files that are saved, but not included in the commit log, in the deployment. 

The `--staged` flag is meant to test out deployments on test servers, to include new features that may not meant to be included into a final version.

## Best Practices ##

- If the test feature is meant to be tested, by all means do the test deployment with `eb --staged`
- There are other ways to push credentials onto an Elastic Beanstalk instance, which includes pulling files from an S3 bucket implemented with proper IAM policies, or AWS Secrets Manager, or...just don't use `eb --staged` for that purpose.
