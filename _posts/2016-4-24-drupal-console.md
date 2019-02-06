---
layout: post
title: Drupal Console and CentOS
---

URL: [https://github.com/hechoendrupal/DrupalConsole/issues/1842#issuecomment-214076492](https://github.com/hechoendrupal/DrupalConsole/issues/1842#issuecomment-214076492)

It seems that submitting a comment is trivial, but the thread discusses an issue where Drupal Console runs into Segmentation Fault on CentOS, particularly in Bluehost services. The amount of relief that the resolution is reachable is immeasurable. To repeat:

In `/usr/lib/php.ini`, comment out the following line

`zend_extension="/usr/local/IonCube/ioncube_loader_lin_5.6.so"`

The running the following line works with output shown:

```
$ ./drupal.phar init --override
Copied files
User home path: /home/holingpo/.console/
1 - aliases.yml
2 - chain/create-data.yml
3 - chain/form-sample.yml
4 - chain/quick-start-db-env.yml
5 - chain/quick-start-db.yml
6 - chain/quick-start.yml
7 - chain/sample.yml
8 - chain/site-drop-restore.yml
9 - chain/site-install.yml
10 - chain/update-gitbook.yml
11 - commands.yml
12 - config.yml
13 - phpcheck.yml
14 - router.php
15 - site.mode.yml
16 - sites/sample.yml


Bash or Zsh: Add this line to your shell configuration file:

source "$HOME/.console/console.rc" 2>/dev/null

Fish: Create a symbolic link
ln -s ~/.console/drupal.fish ~/.config/fish/completions/drupal.fish
```
The full thread of the discussion is available via URL at beginning of this post.
