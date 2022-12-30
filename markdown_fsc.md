![](../Images/)
#R6.1  Playbook
---
Category  | Details
:-------------      | :-------------
Release             | 6.1
Release Name        | 
Sandbox Type        | Production
Date Created        | 2021.05.17
Change Log          | - Initial Document Creation

---
##Table of Contents
- Assumptions
- Prerequisites
- Reference Articles
- Open Items
   
---
##Assumptions
- Release 1.0 - 6.0 has been deployed to
- Skedulo is on Booking Grid Version 
- Production is on Spring '21 Release (API 51.0)

---
##Prerequisites 
- _System Administrator Profile_ and login access to Production
- [SFDX CLI](https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_install_cli.htm), [sfpowerkit plugin](https://github.com/Accenture/sfpowerkit), [SFDMU plugin](https://github.com/forcedotcom/SFDX-Data-Move-Utility) installed and configured on workstation
- Org authorization via [Salesforce CLI](https://github.com/forcedotcom/SFDX-Data-Move-Utility) for newly refreshed sandbox

---
##Reference Articles
- [Spring '21 Release Notes](https://help.salesforce.com/articleView?id=release-notes.salesforce_release_notes.htm&type=5&release=230)

---
##Open Items
- [ ] Customer Community Login Licenses 
- [ ] Destructive changes for **Client (Account)** fields that are tagged **To Delete**

##Presteps<br>

---
- [ ] [1] - ``Rename picklist value`` (1 min)
1.	Navigate to **Setup > Object Manager > Product**
2. Select **Fields and Relationships**
3. Search and select **Product Family** field
4. Scroll Down to **Product Family Picklist Values** 
5. Click Edit on **Product1** (API- Pfizer) and rename label to **Product**<br>
![](../images/setup-product2_family.png)<br><br> 
7. **Save**

---

###Deployment

- [ ] [1] - ``Deploy  source package to `` (10 min)

```
sfdx force:source:deploy -u OrgAlias -c -p path -w 30 --testlevel=RunLocalTests

```
- [ ] [2] - ``Deploy pre-reg source package to `` (5 min)

```
sfdx force:source:deploy -u OrgAlias -c -p path -w 30 --testlevel=RunLocalTests
```

- [ ] [3] - ``Deploy access-mgmt source package to production`` (5 min)

```
sfdx force:source:deploy -u OrgAlias -c -p access-mgmt -w 30 --testlevel=RunLocalTests
```


---
###Post Deployment 

- [ ] [1] - ``Edit Layout in Buttons,Links and Actions`` **Event Inventory Report**
1. Navigate to **Setup > Object Manager > Shipment Object > Button, Links and Buttons**
2. Click on **New_Inventory** and click **Edit Layout** button
 ![](../images/setup-Object_shipmentButton.png)<br><br>
3. Verify the field **Product** is not in the layout and is part of the Asset Fields available to be used.
![](../images/setup-Object_shipmentButton_layout2.png)<br><br>
4. **Save** the layout
5. Verify that the **Product** is not present in the list under Predefined Field Values
![](../images/setup-Object_shipmentButton_DeleteProduct2.png)<br><br>



- [ ] [2] - ``Custom Code Settings for Batch Execution`` (2 min)
1.	Navigate to **Setup > Custom Code > Custom Settings**
2. Click on **Manage** next to **Enable/Disable Setting**
3. Click **Edit** on **profile**
 ![](../images/setup-custom_settings_EnableDisableStorage.png)<br><br>
4. Click check box **Skip Storage Location** <br><br>
  ![](../images/setup-custom_settings_EnableDisableProfile_StorageLocation.png)<br><br>
5. **Save**
6. Repeat step 3, 4 and 5 for Profile **System Administrator**<br><br>

- [ ] [3] - ``Custom Value Settings for Name Value Pair`` (1 min)
1. Navigate to **Setup > Custom Code > Custom Settings**
2. Click on **Manage** on **Name Value Pair**
3. Click **New**
4. Add value  **Warning** for Name and **110** for Value
   ![](../images/setup-custom_settings_NameValuePair.png)<br><br>
5. **Save**

[Back to Top](#table-of-contents)