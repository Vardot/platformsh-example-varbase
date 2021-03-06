# Varbase Project Template for Platform.sh

This project provides a starter kit for Varbase 8.8.x projects hosted on [Platform.sh](http://platform.sh). It
is very closely based on the [Varbase Composer project](https://github.com/Vardot/varbase-project).

This template builds Drupal 8 using the "Drupal Recommended" Composer project.  It also includes configuration to use Redis for caching, although that must be enabled post-install in `.platform.app.yaml`.

Drupal is a flexible and extensible PHP-based CMS framework.

## Services

* PHP 7.3
* MariaDB 10.4
* Redis 6

## Post-install

1. Run through the Drupal installer as normal.  You will not be asked for database credentials as those are already provided.

2. Once Drupal is fully installed, edit your `.platform.app.yaml` file and uncomment the line under the `relationships` block that reads `redis: 'rediscache:redis'`.  Commit and push the changes.  That will enable Drupal's Redis cache integration.  (The Redis cache integration cannot be active during the installer.)

## Customizations

The following changes have been made relative to Drupal 8 "Recommended" project as it is downloaded from Drupal.org or Packagist.  If using this project as a reference for your own existing project, replicate the changes below to your project.

* The `.platform.app.yaml`, `.platform/services.yaml`, and `.platform/routes.yaml` files have been added.  These provide Platform.sh-specific configuration and are present in all projects on Platform.sh.  You may customize them as you see fit.
* An additional Composer library, [`platformsh/config-reader`](https://github.com/platformsh/config-reader-php), has been added.  It provides convenience wrappers for accessing the Platform.sh environment variables.
* Drush and Drupal Console have been pre-included in `composer.json`.  You are free to remove one or both if you do not wish to use them.  (Note that the default cron and deploy hooks make use of Drush commands, however.)  The Drupal Redis module also comes pre-installed but not enabled by default.
* The `settings.platformsh.php` file contains Platform.sh-specific code to map environment variables into Drupal configuration. You can add to it as needed. See the documentation for more examples of common snippets to include here.  It uses the Config Reader library.
* The `settings.php` file has been heavily customized to only define those values needed for both Platform.sh and local development.  It calls out to `settings.platformsh.php` if available.  You can add additional values as documented in `default.settings.php` as desired.  It is also setup such that when you install Drupal on Platform.sh the installer will not ask for database credentials as they will already be defined.

## References

* [Drupal](https://www.drupal.org/)
* [Varbase](https://www.drupal.org/project/varbase)
* [Vardot](https://www.drupal.org/vardot)
* [Drupal on Platform.sh](https://docs.platform.sh/guides/drupal9/deploy.html)
* [PHP on Platform.sh](https://docs.platform.sh/languages/php.html)
