# Publishing WP Plugin on Github

## Setup the updater

1. Create a `release` branch
1. If no GitHub remote yet: Create a public repo on Github under the Tenseg org and name it `public` in the plugin project
1. Copy the [updater folder](https://github.com/YahnisElsts/plugin-update-checker?tab=readme-ov-file) into the root of the plugin
1. Add code like the following to the bottom of the main plugin file

```php
/**
 * Plugin Updates
 */
function tg_{slug}_plugin_updates() {
 require dirname( __FILE__ ) . '/plugin-updater/plugin-update-checker.php';
 $myUpdateChecker = \YahnisElsts\PluginUpdateChecker\v5\PucFactory::buildUpdateChecker(
  'https://github.com/tenseg/tg-404-site-checker',
  __FILE__,
  '{slug}'
 );
 $myUpdateChecker->setBranch( 'release' );
}
add_action( 'admin_init', 'tg_{slug}_plugin_updates' );
```

## How to Push an Update

To release an update of a plugin or theme on Github

1. Bump version and tested up to in header and both readme files
2. Add release notes to both readme files
3. Commit update on main and push to internal remotes
4. Push to Github
    1. `git push public main` in command line
5. On Github create a pull request from main to release branch
6. Confirm the merge

At this time the update will be showing on websites. But for the sake of creating a release log in Github… Go to Releases > Draft a new release. The information should be:

* Create a new tag that is the version number
* Target is “release” branch
* Title is version number
* The description should, among other things, list the release notes that are in the readme files.
