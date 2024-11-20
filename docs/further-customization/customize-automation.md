---
layout: default
title: GRMS Base Flow Pack
parent: Further Customization
nav_order: 1
has_children: false
---
When you install GRMS from Salesforce.org's [MetaDeploy page](https://install.salesforce.org/products/grms/latest), you have the option of installing a set of flows to help streamline your work with the app. The flows included are detailed below.

## Create Relationships from List View Flow

**Flow Label:** 	Create Relationships from List View

**API Name:** 	Create_Relationships_from_List_View

**Type:** 		Screen Flow

**Ver:** 		V1

**Description:** 	This  is a bulk assignment Salesforce flow designed for efficiently assigning field workers to new survey recipients or clients. This flow receives Contact IDs as input from a list view, for example, and will let the user select a field worker and the relationship type from picklists. The field workers in the Org are the Contacts where the GRMS__ContactType__c value is “Field Worker”. The relationship types include but are not limited to “Mother” “Child” and “Regular Client”. Once the user makes the necessary selections, GRMS__FieldWorkerClientRelation__c (Field Worker and Client Relationship) records will be created to establish the relationship between the clients and the field workers.


### Flow Design Screenshot

![CreateRelationshipsScreen1](https://github.com/user-attachments/assets/9906aa33-1b65-4352-8018-34674b879437)

### Flow Dialog Screens

![CreateRelationshipsDialog1](https://github.com/user-attachments/assets/dec928ca-861f-430d-b79b-5160bdc07577)

![CreateRelationshipDialog2](https://github.com/user-attachments/assets/c0c12a1a-6dac-404a-bad7-372e08b07bb6)

## Case Load Migration Flow Flow

**Flow Label:** 	Case Load Migration Flow

**API Name:** 	Case_Load_Migration_Flow

**Type:** 		Screen Flow

**Ver:** 		V1

**Description:** 	A screen flow to migrate a case load between field workers, either by re-assigning to a different field worker or copying a case load to a different field worker. The field workers in the Org are the Contacts where the GRMS__ContactType__c value is “Field Worker”. Once the user makes the necessary migrate or copy selection, GRMS__FieldWorkerClientRelation__c (Field Worker and Client Relationship) records will either be cloned and assigned or updated and moved to the new field worker. 


### Flow Design Screenshot

![CaseLoadMigrationScreenshot](https://github.com/user-attachments/assets/78963a7b-9028-4d4b-833a-64796fe665db)

### Flow Dialog Screens

![CaseLoadMigrationDialog1](https://github.com/user-attachments/assets/c9afebfd-9f67-409b-850f-b4d9a3185a1c)

![CaseLoadMigrationDialog2](https://github.com/user-attachments/assets/98fa26db-b3c7-45d4-844e-1f804c61db6c)






