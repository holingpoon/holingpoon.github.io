---
layout: post
title: Vagrant file permissions
---

In Vagrant, you have the option to mount a shared folder with two options

This would mount `/vagrant/www` where permissions can be changed outside of Vagrant, but not inside the VM.
```
config.vm.synced_folder "./www", "/vagrant/www",
  owner: "vagrant",
  group: "www-data",
  :mount_options => ["dmode=775", "fmode=664"]
```
 
This would let user change file and directory permissions within the VM.
 
```
config.vm.synced_folder "./www", "/vagrant/www",
  :nfs => true
```
