---
layout: default
title: Getting Your Field Workers Started
nav_order: 4
has_children: true
---
# Onboarding Field Workers

After completing the [Getting Started](https://github.com/SFDO-Community/GrassrootsMobileSurveyApp/wiki/#getting-started) steps you can enable a field worker to use the mobile app as follows. You may have already completed some of these steps in the setup but this is a chance to make sure you have everything setup correctly.
1. Create a Salesforce Contact for your field worker
   * Follow the same instructions in [Create Field Worker Contact Records](./Salesforce-Initial-Setup#create-field-worker-contact-records) as you did when you created a field worker Contact for yourself.
![Login Email field](https://user-images.githubusercontent.com/1404346/127728081-20fdc583-617d-44b3-9eba-ce5c27af5fc0.png)

2. Add your field worker as a "user" in Heroku/Auth0
   * Log in to the Heroku account that you created in [Heroku Initial Setup](./Heroku-Initial-Setup) and click on the app that you created.
![Heroku Resources](https://user-images.githubusercontent.com/1404346/128602802-64bcc7ee-42b5-4d96-bdae-194fd2bbb0ad.png)

   * Follow first the steps in [Store Field Worker Credentials in Auth0](./Heroku-Initial-Setup#store-field-worker-credentials-in-auth0) to get to the main Auth0 page for the app.
   * Follow all the steps in [Create a Mobile App Login for a Field Worker](./Heroku-Initial-Setup#create-a-mobile-app-login-for-a-field-worker) except enter your field worker's email address instead of your own.

3. Send your field worker instructions on how to install and use the mobile app, including the new password that you have just created for them.