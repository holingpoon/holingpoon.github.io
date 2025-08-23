---
layout: post
title: How to upgrade Drupal 11
---

`$ brew install php` `# Needs PHP 8.4`

`$ brew services start php` `# Starts PHP 8.4`

`$ pwd` `# should be in drupal directory`
 
`$ composer require drupal/core-recommended:11.2.3 drupal/core-composer-scaffold:11.2.3 drupal/core-project-message:11.2.3 --update-with-all-dependencies`

At this point will have more updates. Lots of deprecation (why is all caps GLOBALS still in use?), but `composer` will do its job collecting the right packages. 

`$ ddev start` 

It's starting, then asking to upgrade the Docker images.

And it's voila, you are back in the Drupal installation, going your merry way.
 