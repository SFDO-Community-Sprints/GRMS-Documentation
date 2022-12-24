---
layout: default
title: Customize GRMS Salesforce Automation
parent: Further Customization
nav_order: 1
has_children: false
---

# Auto-Create or Update Survey Contact

This Flow will allow Salesforce to automatically find or create a Survey Client if one did not already exist. For our purposes we will be matching by last name and birthdate. Feel free to customize to what is either required or almost always filled out for your organization. You will need to figure out what you are filtering by on yours. It should be information that is captured on both the contact and field survey records.

## Definitions

* Elements: Elements are the actions you drag onto the canvas, customize to do actions, and connect to create automation.

* Variables: Variables are holding places for information within the Flow. Most will be auto created by Salesforce.

* Enter a valid value: This is Salesforce’s generic warning that you tried to select part of a variable or other resource, but it was not fully selected or has a typo (in Salesforce’s definition). When you have selected it correctly it will turn blue.  Note: Not all selections in Resource/Field/Value fields will turn blue.

## Set Up Your Flow
Under Setup, type “Flow” in the Quick Find box, then go to Flows. Click the “New Flow” button. For this Flow we will be using “Record-Triggered Flow”. That means it is going to run automatically after data is entered into Salesforce, rather than being run by users interacting with it, like with a Screen Flow.

![Record-Triggered Flow](https://user-images.githubusercontent.com/44512446/188518238-6abe81bc-b7a6-487e-aeae-83808e961ae6.png)

The starting object will be “Field Survey”. Then select “A record is created” for when the Flow should be triggered.

We are also going to set entry conditions. Select “All Conditions Are Met (AND)”, then select the “Survey Contact” field (which is a contact lookup field) as your first condition. The operator should be “Is Null”. Select “$GlobalConstant.True” for the value, and it will turn blue instead of black. This condition means that the Survey Contact field is empty.

![Set Conditions](https://user-images.githubusercontent.com/44512446/188518443-fd51df9e-9a28-4be9-822b-95cb83e94f17.png)

Since we are going to be creating other records related to the Field Survey object, you should select “Actions and Related Records” (also known as an After-Save Flow). As this Flow has some splitting and rejoining, I recommend using the Freeform layout rather than the Auto-Layout. (Note that directions from here on out assume you are using the Freeform builder.) Change from Auto-Layout to Freeform by using the drop down selector at the top of your Flow Builder screen.

![Freeform layout](https://user-images.githubusercontent.com/44512446/188518591-e7bd58b2-2d75-4711-8adf-2fcbb10e5e02.png)

## Build Your Flow
### Set Up Your First Elements
From the left sidebar, drag a Decision element onto the screen. We are going to make an outcome to make sure the fields we are using to find the contact have been filled out. Since we are filtering by the starting record to find that record, just search “record” in the Resource box. Click on “$Record” or hit Enter to get into the record and into the specific fields list. The first field we are filtering by is “Respondent Last Name”. Select the “Respondent Last Name” field, and it will turn blue instead of black. Then select “Is Null” as the operator and “$GlobalConstant.False” as the value. This means that the Respondent Last Name field has been filled out.

![Select Resource 1](https://user-images.githubusercontent.com/44512446/188518964-fc41c6eb-97ed-4014-951a-d1dfcf0934cb.png)

We are going to follow the same process to add HH Member Birthdate as another condition. If something meets both of these conditions (because we have All Conditions Are Met (AND) selected) then it would go down this path. If something does not meet both of these conditions, then it will go down the Default Outcome path. Your Decision element should now look like this:

![Decision 1](https://user-images.githubusercontent.com/44512446/188518975-1ab0bb5a-db45-4fc7-a501-f20e4f25172a.png)

Take the circle at the bottom of the start element and drag it to the decision element to connect the two. Once it is connected then there will be a line from the start element to the decision element with a bubble that says “Run Immediately”.

Now we are going to drag a Get Record onto the canvas. This is where we are going to search for the matching contact. The object should be Contact. Then under Filter Contact record the left side (Field) is the field on the contact record and the right side (Value) is where that information is saved on the Field Survey. You will use the same searching record then searching fields and selecting as you did when setting up the conditions in the outcome in the decision element. You should be using the same fields that were in your decision. Your Get Records element should look like this at this point:

![Get Record 1](https://user-images.githubusercontent.com/44512446/188519125-764053cd-880c-46dd-8b63-f415d960aa05.png)

Scroll down on your Get Record element. We only want to store the first record since we do not have processing for possible duplicates. Then let Salesforce automatically store the field and create a variable for us to use. The variable name will be based on your Get Records element name. After this has been saved, connect your decision element to your Get Records element. You will want to connect the “Yes fields are filled out” outcome and not the “Default Outcome”.

Don’t forget to save your Flow frequently since it does NOT auto-save. Save will overwrite the current version where as Save As  allows you to either create a new version or save it into a different Flow. After you activate the Flow you can only use Save As. 

We are going to create another decision element. This is for checking if the Get Contact element found a record or not. 
Search for the Get Matching Contact variable (or what your Get Record element was called) in the Resource selection. Select it then once it has a period at the end where you can see the fields click away from the Resource box. That will select the variable in general rather than a specific field in the variable. Then the operation will be Is Null and the value False. For maximum clarity you can rename the Default Outcome to something else such as "No Match".

### Branching Out
From here we are splitting into two paths. The first is for if there was no contact found and this Flow needs to create both the Contact record and the Client/User Relationship record. The second path is for if the contact was found and so we need to check to make sure a Client/User Relation record exists and create it if not.

We are starting out on the path for if there was no contact found. Drag in a Create Records elements. We are creating one record and using separate resources and literal values. Here we have the first name and last name in the left-hand side (Field) and pulling that information from the Field Survey in the right-hand side (Value). In this case we are pulling from resources (in this case the resources are variables).

![Create Records 1](https://user-images.githubusercontent.com/44512446/188519566-5efd99d8-d4ab-45d4-8123-3b68970c91a9.png)

Next we are populating the GRMS Contact Type picklist. Here rather than filling it in with a Resource we using a literal value. Flow knows this is a picklist so will show the picklist options for the field under Picklist Values when clicking into the Value box. We are going to select Survey Client.

![Create Record 2](https://user-images.githubusercontent.com/44512446/188519652-48047c7a-cd3d-429e-971a-78262b12d45d.png)

You can add as many fields are you would like. Try adding fields like Birthdate, Email, Home Phone, and Mobile Phone so they will be added on your new Contact. Next, we need to connect the decision outcome “No Match” to the Create Client Contact element - if no contact was found we will create one.

![Branch1](https://user-images.githubusercontent.com/44512446/188519743-d7a429bc-5dcf-4bce-ae26-58c5f979438f.png)

Now we are going to do something different. On the left side select Manager. Then click on New Resource and from there select the Formula option. You should then see a New Resource like the one above. Name it ContactIdFormula and change the Data Type to Text. Within the formula box, type the following formula: 

IF(ISBLANK({!Get_Matching_Contact.Id}), {!Create_Client_Contact}, {!Get_Matching_Contact.Id})

What this is allowing us to do is have one create client/user relationship element rather than two. The system will dynamically know which Contact Id to fill in. It is looking at the Id of the Get Matching Contact variable and if that is not filled out then it will fill in the Id of the Create Client Contact element. If it is filled in then it will use that Id. You can use the “Insert a resource” box to easily get the relevant field for your Flow. If you named your named elements something different to what we did then the variable names will also be different:

IF(ISBLANK( [Enter variable for Get Matching Contact Id here] ), [Enter variable for Create New Client/Contact here] , [Enter variable for Get Matching Contact Id here again])

![Formula 1](https://user-images.githubusercontent.com/44512446/188519983-9f81afa4-533e-4458-934b-60a8abb43206.png)

We are going to use another New Create Records element. This time we are Creating a Field Worker and Client Relationship Record. We only need to set two fields on this record. The GRMS Client will be the Contact Id formula we just created. Then the GRMS User will be the User Contact on the Field Survey record.

![Create Record 2](https://user-images.githubusercontent.com/44512446/188520087-5f9af396-42f0-4e8a-87da-e4decea8048d.png)

Now we will be using an Update Records to update the Field Survey record with the Client Contact ID. Since we are using a Record Triggered Flow we can use the first “Use the field survey that triggered the flow” option. We always want to update the record and the field we want to update is Survey Contact. We will again use our Contact Id Formula in the Value column to do that.

![Update Records 1](https://user-images.githubusercontent.com/44512446/188520156-9d0d0f9a-dc42-4219-a3e0-5980ec5f6236.png)

At this point this is all going down from the No Match outcome so you can connect all of the newly created elements together. Here’s what your flow should look like: 

![Branch 1 Built](https://user-images.githubusercontent.com/44512446/188520199-378d3069-dcea-49f1-b055-5ad37eae57f3.png)

### Building the Second Branch
We need to build out the Yes, a contact was found route. We will be using a Get Records element first to see if there is an existing relationship between the user and client so the object for this element should be Field Worker and Client Relationship. We want to filter to having the GRMS User matching the User Contact on the Field Survey and having the GRMS Client matching the contact we found in the Matching Contact get records element. Set up your Condition Requirements on the element for those matches:

![Get Records 2](https://user-images.githubusercontent.com/44512446/188520475-ddb7d42d-daa0-4a2e-ba3d-d63706a881f3.png)

For the remaining field choices on the the Get Records element, we are again only storing the first record and automatically storing fields.

Next we are creating a new decision to check if there is an existing user/client relationship record. For the resource, use the Field Worker and Client Relationship variable from the Get Record element. The operator is Is Null and the value is False. Rename the Default Outcome to "No Existing Record".

![Decision 2](https://user-images.githubusercontent.com/44512446/188520646-60bc4a4e-c6e2-4659-9dd4-d80d560ac882.png)

### Connecting the Branches
Let's get all the elements connected. First connect the Yes match decision down to the Find Client/User Relationship Record Get Records element. That will then go down to the new decision. Connect the No Existing Record outcome to the Create Record element you created in your first branch - the one that creates a User Client Relationship record. We can use this element in both branches. Then connect the Yes, existing record was found outcome to the final update surveys element. Here is what your connected elements should look like: 

![Branches 1](https://user-images.githubusercontent.com/44512446/188520770-5d3c49a8-9217-4afd-a550-11d06102bbd5.png)

You are all set! When you are ready for it go live click Save and then Activate in the upper right hand corner. 



