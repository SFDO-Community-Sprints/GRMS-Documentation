---
layout: default
title: Further Customization
nav_order: 4
has_children: true
---

# Editing Localization

## Localization in Salesforce

Because the mobile app accesses Salesforce through the special integration user, Salesforce's standard translation mechanism cannot be used. Instead, `GRMS_Localization__mdt` custom metadata records are used to display localized labels for record types, section labels and field labels.

<img src="https://user-images.githubusercontent.com/1404346/94517581-3a6a6080-0263-11eb-8416-a7efa9822451.png" width="80%" >


## App-Embedded Localization

See the [src/config/locale/](https://github.com/SFDO-Community-Sprints/GrassRootsMobileSurveyApp/tree/master/src/config/locale) folder.