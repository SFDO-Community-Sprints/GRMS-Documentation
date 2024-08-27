--- 
title: Architecture Overview
nav_order: 2
---
#  Architecture Overview

This mobile app utilizes a Heroku app with Auth0 as a login API endpoint to sync the offline survey data to your org using a Salesforce integration user license. The mobile app authenticates users in Auth0 and retrieves a Salesforce access token to download metadata and upload records. A configurable Salesforce package manages the surveys and the mobile app users in your org. 

<img width="911" alt="Architecture Overview" src="https://user-images.githubusercontent.com/1404346/106978014-bf7bfe00-679e-11eb-8019-160e5cdd37b3.png">

## 1. Mobile app
- Generates survey screens based on your Salesforce survey page layouts. 
- Uploads survey records stored locally on your device to your Salesforce org.
- Built on the [Expo platform](https://expo.io/). 

## 2. Heroku Login API app with Auth0 add-on
- [@SFDO-Community-Sprints/GrassRootsSurveyHerokuAuth0LoginApi](https://github.com/SFDO-Community-Sprints/GrassRootsSurveyHerokuAuth0LoginApi) 
- Manages IDs of mobile app users. 
- Provides a login API and Salesforce access token to the mobile app. 

## 3. Salesforce package
- [@SFDO-Community-Sprints/GrassRootsSurveySalesforcePackage](https://github.com/SFDO-Community/GrassrootsSurveySalesforcePackage)
- Provides object settings needed in the mobile app.
- Survey types and fields, layouts, and localization settings are customizable.

## 4. Data Model
The following table summarizes the package components. Additional Information is on our [Data Model page](contribution/data-model.html).

| Name | Description | API Name |
| ---- | ----------- | -------- |
| Field Survey | Custom Object | `GRMS_Survey__c` |
| Field Worker and Client Relationship | Custom Object| `GRMS_FieldWorkerClientRelation__c` |
| Contact Type | Contact Custom Field | `GRMS_ContactType__c` |
| Field Worker | Contact Type Picklist Value | `Field Worker` |
| Survey Client | Contact Type Picklist Value | `Survey Client` |
| Login Email | Contact Custom Field | `GRMS_LoginEmail__c` |
| Field Worker and Client Layout | Contact Page Layout | |
| Field Survey Layout | Field Survey Page Layout | |
| Grassroots Survey App Admin | Permission Set | `GRMS_App_Admin` |

## 5. Additional Architecture Information
* [State Management](https://github.com/SFDO-Community/GrassrootsMobileSurveyApp/wiki/State-Management)
* Mobie Application [Screens](https://github.com/SFDO-Community/GrassrootsMobileSurveyApp/wiki/Screens)
* [Localization](https://github.com/SFDO-Community/GrassrootsMobileSurveyApp/wiki/Localization)
