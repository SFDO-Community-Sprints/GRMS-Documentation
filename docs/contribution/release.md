---
layout: default
title: Release
parent: Contribution
nav_order: 6
has_children: false
---

# Release

## Mobile App
1. Create a release branch for the new version. Branch name should be like `release/vX.Y.Z`.
2. Summarize the features and/or bugs fixed in `CHANGELOG.md`.
3. Update `app.json`.
4. Push the branch and create a pull request.
5. After merged, create the tag in new release page. GitHub Actions will automatically generate the `.apk` file.
6. Attach the `.apk` file in the release page.

## Salesforce Package
1. Create a release branch for the new version. Branch name should be like `release/vX.Y.Z`.
2. Summarize the features and/or bugs fixed in `CHANGELOG.md`.
3. Update the `sfdx-project.json` and create the new package version.
```
sfdx force:package:version:create --path "force-app" -x --wait 10 --codecoverage
```
4. Install the package in your org and test it. If there's something wrong, fix it and repeat Step 3.
5. Push the branch and create a pull request.
6. After merged, promote the package version.
```
sfdx force:package:version:promote -p 04tXXXXX....
```
7. Update the installation link and package id in [Salesforce setup wiki page](https://github.com/SFDO-Community-Sprints/GrassrootsMobileSurveyApp/wiki/Salesforce-Initial-Setup).