---
layout: post
title: Resizing EBS for EC2
---

This have been covered everywhere, I'm adding things I did to troubleshoot my problem.

## The Problem ##

Usually, this is not a problem. EC2 instances usually comes with properly sized instances. My use case, however, is Neo4J, where databases take up space rather quickly.  This means either I need to mount another volume on the instance that accommodates the database, or...we increase the size of the root volume. 

## Increase disk size ##

- Find EBS volume for your EC2 instance
- Modify the volume and increase the size in GB. Click Modify to save changes.
- SSH into EC2 instance
- `lsblk` to list the block devices
- `sudo growpart /dev/xvda 1` to grow size of `/`
- Restart the EC2 instance to take effect
- Check to see if it worked with `df -h`

## Note ##
Don't forget to remove files that has been taking up space. If your volume is at 100% capacity, `growpart` would return that the device is out of space. 

## Best Practices ##

- This is the quick and dirty fix. If you are serious about AWS costs and making sure all the resource are right sized, and consider mounting less costly AWS resources such as S3 as an EFS.

## References ##
- [Tutorial: how to extend AWS EBS volumes with no downtime](https://hackernoon.com/tutorial-how-to-extend-aws-ebs-volumes-with-no-downtime-ec7d9e82426e)
- [Extending a Linux File System After Resizing a Volume](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html)