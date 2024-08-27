---
title: Salesforce Initial Setup
parent: Getting Started
nav_order: 1
---
# Salesforce Initial Setup
## **Install the Grassroots Survey Salesforce Package**
The `Grassroots Survey` package contains metadata like custom fields and custom objects that are used in the mobile app. 

Follow the appropriate link below to install the `Grassroots Survey` package in a Sandbox, Developer Edition, or Trailhead Playground instance of Salesforce.

* Latest version
  * [Production, Sandbox, or Developer Org](https://install.salesforce.org/products/grms/latest)
  * Trailhead Playground: Follow the instructions at [Install Apps and Packages in Your Trailhead Playground](https://trailhead.salesforce.com/en/content/learn/modules/trailhead_playground_management/install-apps-and-packages-in-your-trailhead-playground) and use package Id `04t6g000008fj0mAAA`.

Click on the **Install Grassroots Mobile Survey (GRMS) - View Details** button on the Salesforce.org MetaDeploy page for install. On the next page, you may select your org type using the dropdown arrow on the **Log In to Install** button.
![Screen Shot 2022-12-10 at 11 18 06 AM](https://user-images.githubusercontent.com/44512446/206865783-4298aa62-c70e-47d6-a82e-45c3c5ec6a98.png)

## **Install the Sample Surveys Unmanaged Package**

The Sample Surveys package is intended to provide some of the fields a new Mobile App administrator may want to include.

Keep in mind that the Grassroots Mobile Survey App was designed to be customizable and flexible to meet the needs of nonprofits that differ widely in how they gather information and how they want to organize and report on it.

The Sample Surveys Unmanaged Package is an optional install on Metadeploy, but we highly recommend installing it. We have prepared two types of surveys, Home Care and Disaster Relief, with fields and page layouts that you can use as is, or pick and choose which fields are relevant for your organization. Or, maybe you'll install, see how the pages work, and then proceed to create totally different surveys for your organization.

To install, make sure it is seleted on the Metadeploy screen.


After the installation is complete, you can see the `Grassroots Survey` application in the Salesforce application launcher ("waffle menu" in upper left). The following table summarizes the package components that are useful to be aware of as you proceed to the next steps in the Salesforce initial setup:

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

## **Create an Integration User**

[Create an integration user](https://help.salesforce.com/articleView?siteLang=en_us&id=000331470&type=1&mode=1) in your org. Make sure the integration user profile has Read access to the Contact object and record types and Create access to GRMS objects.
* You can assign the `Grassroots Survey App Admin` Permission Set to the integration user (or any other user) to open up full permissions on the objects installed by the `Grassroots Survey` Salesforce package.

Make sure you record the username and password of the integration user because they are needed later in Heroku setup. Its security token is also needed if the integration user's profile doesn't have Login IP restrictions.

## **Assign a Permission Set to the Integration User and System Admin**

In Setup, type Permission Sets into the QuickFind box. Click on Permission Sets. Choose Grassroots Survey App Admin.

![Permission Set](https://user-images.githubusercontent.com/44512446/180663570-47f4917a-ecbf-4971-b0f7-e2349131ad07.png)

Assign this Permission Set to the Integration User (the User you created as part of the GRMS installation). Assign it also to anyone on the staff that will be working with the Field Surveys, including the organization's System Administrator.

Click Manage Assignments. Here you can add or remove assignments for this permission set.

![Admin Perms Set](https://user-images.githubusercontent.com/44512446/180663581-18fd591a-c3f7-497d-bf4c-92bc1f6d7ad9.png)

## **Configure Custom Objects, Record Types, Layouts, and Custom Fields**
### **Field Survey Object Changes**

#### **Add a Survey Client Lookup to the Field Survey Object**

1.  Go to `Setup` > `Object Manger` > `Field Survey` > `Fields & Relationships`
2.  Click on New, then Lookup Relationship and choose Contact for Related to. 
3.  Fill in Survey Client for the field label.
4.  Create a Lookup Filter where the Survey Client: Contact Type = Survey Client like the screenshot below. This will limit the lookups for this field to just Survey Clients.
![Survey Client Filter](https://user-images.githubusercontent.com/44512446/204109840-3856d790-f6b2-4945-a2b6-d9117d148258.png)

5. On the next page, specify the profiles that should have access to this field. Click Next.
6. Choose which page layouts you would like this field to appear on. The default is all Field Survey object layouts. Click Next.
7. Choose the Contact layouts that you'd like this related list of surveys to appear on. Click on Save.

Here's what the completed field looks like. Note that you may want to shift where the field is on your page layout later on.

![Survey Client Lookup](https://user-images.githubusercontent.com/44512446/180664224-d51f5b61-f9c7-423f-b4af-e78f6052237a.png)

#### **Enable Optional Features**
These will ensure that you have the reporting functionality and the activity and history tracking capability. Navigate to the Field Survey object in Object Manager in your Salesforce Org's Setup area. Click on Details, then click Edit. Add the boxes ticked below in the screenshot.

![Optional Features](https://user-images.githubusercontent.com/44512446/180665078-2d857c0f-b878-4a0e-9efe-60c3de01a0e7.png)


#### **Create a Record Type**
Most organizations need several surveys for use in the field, for example: New Client, Health Visit, Paperwork Visit, Student Success Visit, etc. For each distinct kind of survey that will have its own fields and picklists and will need its own page layout, create a record type. 

If you are using the Sample Survey pack, it comes with two record types - Disaster Relief and Homecare. _(Pro Tip: Keep Homecare and Disaster Relief Survey record types in your org and modify to meet your needs if they meet your fieldwork scenarios.)_
  
<img src="https://user-images.githubusercontent.com/1404346/94515195-ff196300-025d-11eb-94a9-931424fd4172.png" width="80%" />

#### **Assign Field Survey Record Types to Profiles**

Assign GRMS Record Types to Sys Admin and your Integration User. Note that if you have the Sample Survey Pack installed, you still need to assign the two record types that come with it to profiles. 
![Assign Record Types](https://user-images.githubusercontent.com/44512446/180664780-ca8cf9a5-a091-49f4-8ffc-386af4d26bcd.png)

1. Go to `Setup` > `Users` > `Profiles`
2. Choose either the System Administrator or you Integration User's profile
3. Click on `Object Settings` > `Field Surveys`
4. Assign the Record Types for the surveys that you are going to use.

#### **Create Fields**
Begin by making a list of all the fields you'll need that should be on the survey. Think about what data you need to collect and what type of fields you need to do that. Add these fields to the Field Survey object. 

Keep in mind the [mobile app field limitations](#limitations-with-respect-to-the-mobile-app) listed below when creating fields for your surveys.

#### **Modify Page Layouts**
   * **You need to add at least one editable field to an editable section on the default Field Survey Layout for your mobile app to load your record types.**
   * Your fields will be added to the page layouts in the order you create the fields. This will likely not be the order you want them to appear on your survey. You’ll want to organize and rearrange your page layouts so they make sense for your staff who are out in the field collecting data. 
   * Include Sections on your page layouts, and give these names, for example: Personal Info, Communication Prefs, Address, Health Needs, Disaster Needs, or Referrals.
   * Only sections that are editable on the page layout are displayed in the mobile app. For the example below, the [Information] section is not displayed on the mobile app because it's not an editable section in the page layout. 
 
![Mobile Layout](https://user-images.githubusercontent.com/44512446/206868191-077fc614-6aeb-4f28-a3a4-61fc31e34416.png)

Changes to your field survey layouts are synced to the mobile app after mobile app login, or by the `Reload Metadata and Survey` button on the [Settings] screen in the mobile app as shown here:

  <img src="https://user-images.githubusercontent.com/1404346/168547098-a19ae7b3-9603-44d4-9213-ace55697f6e0.png" width="250"/>

#### **Assign Field Survey Page Layouts**
Assign the layouts associated with each record type to the appropriate profiles.

![FS Page Layout Assign](https://user-images.githubusercontent.com/44512446/180664630-f5a08e28-4bff-492d-a5d1-13f0381bfa73.png)

#### **Adjust the Field Survey Object Compact Layout**
1. Find Compact Layout in the sidebar on the Field Survey object in Object Manager. The field that is at the top of a Compact Layout for a record type will be the field that shows in the list of available surveys in the mobile app. The rest of the fields will show at the top of a Field Survey record page in Salesforce.
2. Rearrange the fields for your usage and delete any fields showing that you don't need.

![Compact Layout](https://user-images.githubusercontent.com/44512446/204106104-938404d7-fd6a-4e9e-acd8-3052f91c073d.png)

## **Contact Object Changes**

### **Verify that the Login Email field and Contact Type field are on the Contact Page Layouts**

If either one of these is not on the page layout, add the Login Email field and the Contact Type field to the Contact Page Layout. The field is already created. You just need to put it on the page.

1. In Setup, Click Object Manager
2. Find the Contact object
3. Click Page Layouts
4. Click and Drag the Login Email and Contact Type to the Page Layouts.
5. These two fields may already be on the Field Worker and Client Page Layout, but would still need to be added to the regular Contact Layout, if you are using that page layout.
6. Save

![Login Email on Layout](https://user-images.githubusercontent.com/44512446/180665339-602d8cbf-a3de-40a2-bec4-7a76b1e2779b.png)

### **Adjust the Related Lists**
Include Field Surveys and Client Relationships in the Contact Related List. This way, we can see who is conducting surveys, and who is being surveyed. Be sure to Click Save.

![Related Lists on Contact](https://user-images.githubusercontent.com/44512446/204109695-49433168-d678-44dc-a66b-0bc865812c55.png)

To change the visible fields, you can click on the wrench and add the fields that you want to see on Related Lists when you go to the Contact object.

![Adjust Related Lists](https://user-images.githubusercontent.com/44512446/183319492-34571056-f1f3-4bf0-9481-fc5ae7e19fa4.png)

## **Set up Field Worker and Client Relationships Object**

This is the object where we associate your survey field workers with their "caseload." The mobile phone will be able to populate each field worker's "clients" so that the field workers don't have to scroll too far to find the people they are responsible for.

### **Update the Type Field Picklist Values**
1. Go to `Setup` > `Object Manager` > `Field Worker & Client Relationships` > `Type` Custom Field
2. Scroll down to the Values section and click on New. 
3. Add values that will suit your organization's use for Survey Client relationships such as Mother, Child, Regular Client, Drop In, etc.
4. Deactivate the placeholder Relation 1, Relation 2, etc values.

### **Create Field Worker Contact Records**

The Grassroots Survey package has the Contact Type `(GRMS_ContactType__c)` picklist field with the following values:
* `Field Worker`: identifies field workers (your staff who collect survey data)
* `Survey Client`: identifies clients (contacts who engage with the field worker). 

In this step you will add yourself as a field worker in Salesforce. This is a necessary step for you to be able to demo, test, and help your field workers sign in to the mobile app later. Field workers are represented in Salesforce as Contact records with the `Field Worker` picklist value for the Contact Type field.

1. Create a contact record that has the `Field Worker` Contact Type, with any name you like (either yours or a placeholder name like Sally Fieldworker). 

2. Enter your email address in the `Login Email` field. The value of this field is used in Heroku/Auth0 as the login username for the mobile app.  **Note: Login email is case sensitive on the mobile app.**

3. Create additional Contact records with a Contact Type of 'Field Worker' for other staff who will use the mobile app. The Field Workers, whether they are disaster relief workers, teachers in classrooms, or health professionals making house calls, are the people assessing the situation on the ground, using our mobile app that works even without the internet.

![Contact Record](https://user-images.githubusercontent.com/44512446/180665863-a9e72121-c776-4fe2-81f0-bd79949d8d76.png)

### **Create Client Contact Records**
If you already have a list of clients, you can create Contact records for them in advance. Follow the instructions above for creating Field Worker Contact records, making sure to give them the Contact Type picklist value of 'Survey Client'.

### **Link Survey Clients and Survey Users in the Field Worker and Client Relationships Object**
You can create a client list for your field workers by entering records in the User and Client Relationships object. This is a junction object that links survey client and field worker Contacts. Once you have created these linked Contact records, your field workers will have assigned survey clients available in the Survey Client field on the mobile app. 

Click on the New button on the Field Worker and Client Relationships object. Note the following as you create records:
* Relationship Number is automatically generated. As is the record owner.
* Field Worker will be the Contacts with the Contact Type field set to Field Worker.
* Client will be the Contacts with the Contact Type field set to Survey Client.
* Type picklist field can be customized to meet your organization's needs as noted above in the Update the Type Field Picklist Values section. 

## **Limitations with Respect to the Mobile App**

Be mindful of the following limitations of the Field Survey object as it's used in the mobile app:
 * Read-only fields are not supported and are invisible in the mobile app.
 * Multi-select Picklist fields are not currently supported and are invisible in the mobile app.
 * Lookups to non-Contact fields are not supported and are invisible on the mobile app.
 * The `Survey Date (GRMS_SurveyDate__c)` field doesn't appear in the mobile app, but the value of this field is automatically set to the date when you create the field survey locally on the mobile device.

## **Next Step**
Now your Salesforce org is configured for use with the mobile app! Go to [Heroku Initial Setup](/Heroku-Initial-Setup.md) to set up the handshake between Salesforce and the mobile app.
