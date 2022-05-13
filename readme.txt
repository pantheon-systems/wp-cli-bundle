Managing the Fork

Unless otherwise specified, development should start off the previous release tag. For example if we were to create a 2.7.0 release, you'd create a branch off of tag v2.6.0-pantheon2. Release branches should be prepended with `release-`.

A .patch file should be created containing any modifications that need to be made to this repo or any dependencies. Place your .patch file in /patches. See release-2.6.0 branch for reference.

Steps for Release:

1. Install dependencies: composer install --no-dev --no-progress --no-interaction
2. Add your patch to the patches key in composer.json here: https://github.com/pantheon-systems/wp-cli-bundle/blob/release-2.6.0/composer.json#L64
3. Apply your patch by running: composer update.
4. Commit your changes and push up to your branch.
5. With your branch checked out locally, create and push a tag: git tag vX.X.X-pantheonX && git push origin vX.X.X-pantheonX (where X.X.X is the matching WP-CLI version number, and pantheonX is incremented based on the previous release here: https://github.com/pantheon-systems/wp-cli-bundle/releases)
6. Use the GitHub GUI to create a release from the tag you pushed.
7. Locally, build the Phar file: php -dphar.readonly=0 utils/make-phar.php wp-cli.phar --version=$CLI_VERSION. Be sure to replace $CLI_VERSION with the desired version.
8. Rename the Phar so the pattern matches wp-cli-X.X.X-pantheonX.phar.
9. Locally, run this command to generate the shasum: shasum -a 512 $PHAR_NAME.phar > $PHAR_NAME.phar.sha512. Be sure to replace $PHAR_NAME with the name of your Phar file.
10. Attach the files generated from steps 7 & 8 to the release you created in step 6.
