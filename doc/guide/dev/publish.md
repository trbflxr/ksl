# Publish new release

When you are ready to release the build it's very important to do it in a proper way.

To make a release follow the steps below:

### 1. Go to repository releases page<br/> ![releases_page](../../images/updater_releases_page.png)

### 2. Depending on whether or not it's a first time you make a release you should select one of available options

* First release<br/> ![releases_first](../../images/updater_releases_first.png)
* Draft new<br/> ![releases_draft](../../images/updater_releases_draft.png)

### 3. Create a new release tag<br/> ![releases_new_tag](../../images/updater_releases_new_tag.png)

Latest release tag will be referenced by KSL updater as latest mod / extension version.

> Important: Tag have to be in format ```v*.*.*``` so KSL can parse the version properly. Example: **v1.2.5**, **v2.10.1**

### 4. Fill the release info<br/> ![releases_description](../../images/updater_releases_description.png)

1. Release title
2. Changelog
3. Additional information (optional)
4. Release [archive(s)](updater.md#release-archive)

> All the text below ```---``` will be ignored by KSL updater and the text above ```---``` will be displayed as a changelog.

At this point you can publish a new release and on the next game start KSL updater will be able to fetch it and perform an update if needed.
