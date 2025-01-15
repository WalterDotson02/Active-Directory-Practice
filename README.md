# Active-Directory-Practice

![image](https://github.com/WalterDotson02/Failed-RDP-Sentinel/blob/56ec5c86bafbb2068c9ff3f77360f91ff3fece60/Images/HoneyPot.png)

Demonstration of 

<h2>Description</h2>


<h2>Learning Objectives:</h2>  

* Configuration & Deployment of Virtual Machines, Windows Server, and Active Directory
* Hands-on experience and working knowledge of a Virtualized Lab Environment
* Create and Manage Users and Groups
* Join Client Machines to the Domain
* Gain Familiarity with PowerShell Automation for AD Tasks

<h2>Technologies + Requirements</h2>

* Virtualization Software (Oracle VirtualBox)
* Active Directory Domain Services (AD DS)
* Powershell
* Customized Powershell Script authored by Josh Madakor

<h2>Step 1: Download and Install Oracle</h2>

![image](https://github.com/user-attachments/assets/7419e070-3074-4d0a-ad8b-ee7de816ab17)

[Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)


<h2>Step 2: Download ISOs for Windows Server 2019 and Windows 10</h2>

[Windows 10 Installation Media](https://www.microsoft.com/en-us/software-download/windows10)

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Download%20Windows%20Installation%20Media.png)

[Windows Server 2019](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Download%20Windows%20Server%202019.png)

<h2>Step 3: Create Virtual Machine for Domain Server</h2>

* Open VirtualBox
* Select <b>New</b>
* Name VM as "DC"
* Change <b>Version</b> to "Other Windows (64-bit)"

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Server%20VM%201.png)

* Change <b>Base Memory</b> and <b>Processors</b> to an amount your computer can handle without taking too many resources

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Change%20Server%20VM%20Memory.png)

* Continue until VM is created
  > We will change configuration in the Settings during the next step

* Right Click our new VM <b>DC</b> 
* Select <b>Advanced</b>
* Change <b>Shared Clipboard</b> and <b>Darg'n'Drop</b> to <b>Bidrectional</b>
  > Not necessary but allows a cleaner experience
* Select <b>Network</b>
* Select <b>Adapter 2</b> 
* Check the box for <b>Enable Network Adapter</b>
* Select <b>Internal Network</b> from the drop-down menu for <b>Attached to</b>
* Click <b>OK</b>

<h2>Step 4: Turn On VM and Login to Administrator Account </h2>

* Turn On <b>DC</b> Virtual Machine
* Select <b>Next</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Server%20setup%201.png)

* Select <b>Install Now</b>
* Select <b>Windows Server 2019 Standard Evaluation (Desktop Experience)</b>
  > This allows us to have a Graphical User Interface
* Select <b>Next</b>
* Select <b>Custom: Install Windows only (advanced)</b>
* Select <b>Next</b>
* Allow time for Installation
  > Installation may take a while and will require a restart of the VM
* Set password as "Password1" for convenience

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Server%20admin%20setup.png)

* Select <b>Finish</b>
* Login to Administrator Account
  > You may have to use built in inputs or commands

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Ctrl%20%2B%20Alt%20%2B%20Del.png)

<h2>Step 5: Set up IP Addressing</h2>

* Open Network Settings

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Open%20Network%20Settings.png)

* Select <b>Change adapter options</b>
* Right Click <b>Ethernet</b>
* Click <b>Rename</b>
* Rename adapter to "_INTERNET_"
* Right Click <b>Ethernet 2</b>
* Click <b>Rename</b>
* Rename adapter to "X_Internal_X"
* Right Click <b>X_Internal_X</b>
* Click <b>Properties</b>
* Open <b>Internet Protocol Version 4 (TCP/IPv4)</b>
* Click radio button for <b>Use the following IP address</b>
* Input <b>IP address</b> as "172.16.0.1"
* Input <b>Subnet mask</b> as "255.255.255.0"
* Click radio button for <b>Use the following DNS server address</b>
* Input <b>Preferred DNS server</b> as "127.0.0.1"
  > 127.0.0.1 is also known as the "Loopback Address"
* Click <b>OK</b>

<h3>Rename PC</h3>

* Right Click <b>Windows Start Button</b>
* Click <b>System</b>
* Scroll Down and Click <b>Rename this PC</b>
* Change name to "DC"
* Click <b>Next</b> 
* Click <b>Restart Now</b>
* Click <b>Continue</b> 

<h2>Step 7: Install Active Directory Domain Services</h2>

* Open <b>Server Manager</b>
* Click <b>Add roles and freatures</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Add%20role%20and%20Featues.png)
  
* Click <b>Next</b> 
* Click <b>Next</b> 
* Click <b>Next</b> 
* On <b>Server Roles</b> click radio button for <b>Active Directory Domain Services</b>
* Click <b>Add Features</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Add%20ADDS%20feature.png)

* Turn Firewall State OFF for <b>Domain Profile Private Profile</b> and <b>Public Profile</b>
* Click <b>Next</b> 
* Click <b>Next</b> 
* Click <b>Next</b> 
* Click <b>Install</b> 

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Add%20ADDS%20feature%202.png)

<h3>Configure ADDS</h3>

* Click Flag Icon
* Click <b>Promote this server to a domain controller</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Promote%20Server.png)

* Click radio button for <b>Add a new forest</b>
* Name the <b>Root domain name</b> "mydomain.com"
* Click <b>Next</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Domain.png)

* Change password to "Password1"
* Click <b>Next</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Domain%202.png)

* Unclick the box for <b>Create DNS delegation</b>
* Click <b>Next</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Domain%203.png)

* Click <b>Next</b> 
* Click <b>Next</b> 
* Click <b>Next</b> 
* Click <b>Install</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Domain%204.png)
  > This will sign you out and restart the VM

* Click <b>Close</b> 

<h2>Step 8: Create Dedication Domain Admin Account</h2>

* Login back in to Administrator account
  > You should notice the Domain name shows on login screen
* Click <b>Windows Start Button</b> 
* Click arrow for <b>Windows Administrative Tools</b> folder
* Open <b>Active Directory Users and Computers</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Admin%20Account.png)

* Right click <b>mydomain.com</b>
* Click <b>New</b>
* Click <b>Organizational Unit</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Admin%20Account%202.png)

* Name Organization Unit "_ADMINS"
* Click <b>OK</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Admin%20Account%203.png)

* Right click <b>_ADMINS</b>
* Click <b>New</b>
* Click <b>User</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Admin%20Account%204.png)

* Make an account with your First and Last name
* Change <b>User logon name</b> to "a-(first inital)(last name)
  > ex: "a-mdotson"
* Click <b>Next</b> 

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Admin%20Account%205.png)

* Uncheck box for <b>User must change password at next logon</b>
* Check box for <b>Password never expires</b>
* Click <b>Next</b> 

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Admin%20Account%206.png)

* Right click New Admin User account
* Click <b>Properties</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Admin%20Account%207.png)

* Click <b>Member Of</b> header tab
* Click <b>Add</b>
* Type "Domain Admins"
* Click <b>Check Names</b>
  > This confirms the object name exists and will correct any errors
* Click <b>OK</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Admin%20Account%208.png)

* CLick <b>Windows Start Button</b>
* Click <b>User Icon</b>
* CLick <b>Sign Out</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Sign%20Out.png)

<h2>Step 9: Add Remote Access Role</h2>

* CLick <b>Other User</b>
* Login to new Domain Admin Account

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Login%20to%20Admin%20User%20.png)

* Open <b>Server Manager</b>
* Click <b>Add roles and freatures</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Add%20role%20and%20Featues.png)
  
* Click <b>Next</b> 
* Click <b>Next</b> 
* Click <b>Next</b> 
* On <b>Server Roles</b> click radio button for <b>Remote Access</b>
* Click <b>Next</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Add%20Remote%20Access%20Role.png) 

* Click <b>Next</b> 
* Click <b>Next</b>
* Check box for <b>Routing</b>
* Click <b>Add Features</b> 
* Click <b>Next</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Add%20Remote%20Access%20Role%202.png) 

* Click <b>Next</b>
* Click <b>Next</b>
* Click <b>Install</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Add%20Remote%20Access%20Role%203.png) 











<h3>Sample</h3>

* Select Sample log saved to Desktop (failed_rdp.log) and click <b>Next</b>

<h3>Record Delimiter</h3>

* Look over sample logs and click <b>Next</b>

<h3>Collection Paths</h3>

* Type: Windows
* Path: "C:\ProgramData\failed_rdp.log

<h3>Details</h3>

* Name and describe the custom log (FAILED_RDP_WITH_GEO) before pressing the <b>Next</b> button
* Click Create

![image](https://github.com/WalterDotson02/Failed-RDP-Sentinel/blob/main/Images/custom_log.png)

<h2>Step 10: Query + Extract Fields from Custom Log</h2>

* Navigate to the newly established workspace (honeypot-law) in Log Analytics Workspaces -> Logs
* We then can run a query and extract the different data filtering by different fields such as latitude, longitude, destinationhost, etc.
  > As of March 31st, 2023, Microsoft has disabled the creation of new custom fields and has migrated to KQL. You can learn more about it here
* Copy/Paste the following query into the query window and Run Query

```
FAILED_RDP_WITH_GEO_CL 
| extend username = extract(@"username:([^,]+)", 1, RawData),
         timestamp = extract(@"timestamp:([^,]+)", 1, RawData),
         latitude = extract(@"latitude:([^,]+)", 1, RawData),
         longitude = extract(@"longitude:([^,]+)", 1, RawData),
         sourcehost = extract(@"sourcehost:([^,]+)", 1, RawData),
         state = extract(@"state:([^,]+)", 1, RawData),
         label = extract(@"label:([^,]+)", 1, RawData),
         destination = extract(@"destinationhost:([^,]+)", 1, RawData),
         country = extract(@"country:([^,]+)", 1, RawData)
| where destination != "samplehost"
| where sourcehost != ""
| summarize event_count=count() by timestamp, label, country, state, sourcehost, username, destination, longitude, latitude
```
> Kusto Query Language (KQL) is used to query and extract logs from data stored in Azure Log Analytics or Azure Data Explorer. KQL is a powerful and expressive query language that allows you to perform advanced data analysis, filtering, aggregation, and visualization. With some practice composing questions and simple instructions, the language is meant to be simple to read and use.

![image](https://github.com/WalterDotson02/Failed-RDP-Sentinel/blob/main/Images/LAW%20KQL%20script%20for%20log.png)

<h2>Step 11: Create World Attack Map in Microsoft Sentinel</h2>

* Access Microsoft Sentinel to view the Overview page and available events
* Click on Workbooks and <b>Add workbook</b> then click Edit
* Delete default widgets (three dots -> remove)
* Click <b>ADD</b>-><b>Add query</b>
* You can Copy/Paste the previous query or this one into the query window and Run Query

```
FAILED_RDP_WITH_GEO_CL 
| extend username = extract(@"username:([^,]+)", 1, RawData),
         timestamp = extract(@"timestamp:([^,]+)", 1, RawData),
         latitude = extract(@"latitude:([^,]+)", 1, RawData),
         longitude = extract(@"longitude:([^,]+)", 1, RawData),
         sourcehost = extract(@"sourcehost:([^,]+)", 1, RawData),
         state = extract(@"state:([^,]+)", 1, RawData),
         label = extract(@"label:([^,]+)", 1, RawData),
         destination = extract(@"destinationhost:([^,]+)", 1, RawData),
         country = extract(@"country:([^,]+)", 1, RawData)
| where destination != "samplehost"
| where sourcehost != ""
| summarize event_count=count() by latitude, longitude, sourcehost, label, destination, country
```
* When results appear, select <b>Map</b> from the <b>Visualization</b> drop-down box.
* Choose <b>Map Settings</b> to make additional adjustments
  > Most settings should be auto-configured from the script above
  
![image](https://github.com/WalterDotson02/Failed-RDP-Sentinel/blob/main/Images/Sentinel%20KQL%20script.png)

<b>Layout Settings</b>

* <b>Location info using</b>: Latitude/Longitude
* <b>Latitude</b>: latitude
* <b>Longitude</b>: longitude
* <b>Size by</b>: event_count

<b>Color Settings</b>

* Coloring Type: Heatmap
* <bColor by</b>: event_count
* <b>Aggregation for color</b>: Sum of Values
* </b>Color palette</b>: Green to Red

<b>Metric Settings</b>

* <b>Metric Label</b>: label
* <b>Metric Value</b>: event_count
* Click <b>Apply</b> button and <b>Save and Close</b>
* Save as "Failed RDP International Map" in the same region and under the resource group (honeypot-lab)
* Keep refreshing the map to show more inbound failed RDP attacks
  > Note: Only unsuccessful RDP attempts will be shown on the map, not any additional attacks the VM might be facing.
  
  ![image](https://github.com/WalterDotson02/Failed-RDP-Sentinel/blob/main/Images/Failed%20RDP%20Map.png)

  > Event Viewer showcasing failed RDP logon efforts. Event ID: 4625
  
  ![image](https://github.com/WalterDotson02/Failed-RDP-Sentinel/blob/main/Images/Event%20Manager.png)

  > Data processing from a custom Poweshell script using a third party API
  
  ![image](https://github.com/WalterDotson02/Failed-RDP-Sentinel/blob/main/Images/ISE%20failed%20attempts.png)

<h2>Step 12: Shut Down Resources</h2>.

> CRUCIAL: DON'T SKIP !

* Look for "Resource groups" -> name of resource group
* Key in the name of the resource group (honeypot-lab) to verify removal of resources
* Select the <b>Apply force delete for selected Virtual machines and Virtual machine scale sets</b> box
* Click <b>Delete</b>

![image](https://github.com/WalterDotson02/Failed-RDP-Sentinel/blob/main/Images/Screenshot%202025-01-14%20092133.png)

> Resources will use free credits if they are not eliminated, and costs may start to accrue.



