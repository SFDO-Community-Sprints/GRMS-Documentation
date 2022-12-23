---
title: Heroku Initial Setup
parent: Getting Started
nav_order: 2
---

* [Create a Heroku Account](#prerequisite)
* [Deploy the Heroku App](#deploy-the-heroku-app)
* [Store Field Worker Credentials in Auth0](#store-field-worker-credentials-in-auth0)

Heroku is the app that links Saleforce to our mobile phones. Heroku is our handshake, our go-between, our connector. Heroku makes it possible to use one Salesforce license for many field workers.

## Prerequisite
* Go to https://www.heroku.com/home and sign up for a Heroku account.
**Note**: Heroku no longer has a free tier as of November 28, 2022. You will need to subscribe to the lowest level tier, called Eco and Basic.($5 USD/month).
* Once you set up the Heroku account, configure [Multi-Factor Authentication for Heroku](https://devcenter.heroku.com/articles/multi-factor-authentication) to secure your account further. `There are two ways you can enable MFA: from Account Settings or by responding to the MFA enablement reminder on Dashboard. As part of the enablement process, you register at least one MFA verification method.`

## Deploy the Heroku App
Click the [Deploy to Heroku] button below to start creating the Heroku app.

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/SFDO-Community-Sprints/GrassRootsSurveyHerokuAuth0LoginApi)

Give your app a name and enter it in the `App name` field (or, leave this field blank to let Heroku generate a cute name for you). Remember the name of your Heroku app because your field workers will need to use it in their first-time mobile app setup.

Next enter the details of your Salesforce integration user (the one you set up [here](./Salesforce-Initial-Setup#create-an-integration-user)) in the `Config Vars` section. If needed, you can generate a new security token by logging into Salesforce as the integration user and following the instructions [here](https://help.salesforce.com/articleView?id=sf.user_security_token.htm&type=5). Then click the [Deploy app] button on the bottom of the page.

![Deploy Button](https://user-images.githubusercontent.com/1404346/105129737-0d4f0000-5b29-11eb-8ccb-184e3d253687.png)


<img src="https://user-images.githubusercontent.com/1404346/118213194-6c55cd80-b4a8-11eb-8d19-e0a3323f80a4.png" width="50%">

## Store Field Worker Credentials in Auth0

After the app is successfully deployed, click [Manage App] to open the settings page. If you don't see a [Manage App] button, go to the main Heroku page and then click on your Heroko app's name.

### Application Settings

Click on the Resources tab and then open the Auth0 app by clicking on its icon.

<img width="700" alt="Heroku Resources" src="https://user-images.githubusercontent.com/1404346/104868672-67b05b00-5987-11eb-892e-b99d2897bb25.png">

Select [Applications] in the Applications section in the left sidebar menu and then select [Default App]. 

<img width="700" alt="Auth0 App Setting" src="https://user-images.githubusercontent.com/1404346/118213607-3e24bd80-b4a9-11eb-8118-2439e431a506.png">

Scroll to the bottom of the page and expand the 'Advanced Settings.''

<img width="700" alt="Auth0 advanced settings" src="https://user-images.githubusercontent.com/1404346/104868940-0a68d980-5988-11eb-9e89-b12f800be003.png">

Select the [Grant Types] tab, check the box for **Password**, and click the [SAVE CHANGES] button.

### Create a Mobile App Login for a Field Worker

Now you are ready to add yourself as a "user" in Auth0 so that the mobile app can recognize you as a field worker. (You will also go through this same process every time you need to add a field worker later.)

Select [User Management] > [Users] in the left sidebar menu and then click the [+ CREATE USER] button.

<img width="600" alt="auth0-user-management" src="https://user-images.githubusercontent.com/13836716/128413604-74575f4c-2527-4fa9-b809-01baaef24590.png">

Enter the same email address you specified in the `Login Email` field of your field worker Contact. Create a new password, write it down somewhere secure for safekeeping, and enter it in the `Password` and `Repeat Password` fields.

* Remember that the email **must** be the same as the `Login Email` field value on your [Field Worker Contact record](./Salesforce-Initial-Setup#create-field-worker-contact-records), because this is how the mobile app recognizes field workers who log in.

<img width="400" alt="Add user" src="https://user-images.githubusercontent.com/1404346/104869948-9c71e180-598a-11eb-92ab-d6bb9f26fa74.png">

Next check for an email from Auth0 with a subject like "Verify your email" asking you to verify your account. Click the [VERIFY YOUR ACCOUNT] button to do this.

* Remember that your field workers will receive a similar potentially confusing email when you add them as Auth0 users too, and you will need to communicate their passwords to them.

## Next Step
You can go to the final setup step to prepare and onboard the mobile app. See [Mobile Environment Setup](./Mobile-Environment-Setup).