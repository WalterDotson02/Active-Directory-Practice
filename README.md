# Active-Directory-Practice

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/active_directory_diagram.jpg)

This repository offers a straightforward, step-by-step guide to setting up an Active Directory Domain Services (AD DS) environment in a home lab using Oracle VirtualBox. It walks you through the process of configuring a Windows Server 2019 virtual machine to act as a domain controller, so you can create a realistic, enterprise-level directory service for hands-on learning and testing.

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
* Click <b>Settings</b>
* Select <b>Advanced</b>
* Change <b>Shared Clipboard</b> and <b>Darg'n'Drop</b> to <b>Bidrectional</b>
  > Not necessary but allows a cleaner experience
  
![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Server%20VM%202.png)
  
* Select <b>Network</b>
* Select <b>Adapter 2</b> 
* Check the box for <b>Enable Network Adapter</b>
* Select <b>Internal Network</b> from the drop-down menu for <b>Attached to</b>
* Click <b>OK</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Server%20VM%204.png)

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
* Change <b>User logon name</b> to "a-(first inital)(last name)"
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


* Click <b>Tools</b>
* Click <b>Routing and Remote Access</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Routing%20and%20Remote%20Access.png) 

* Right click <b>DC (local)</b>
* Click <b>Configure and Enable Routing and Remote Access</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Routing%20and%20Remote%20Access%202.png)

* Click the radio button for <b>Network address translation (NAT)</b>
* Click <b>Next</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Routing%20and%20Remote%20Access%203.png)

* Click <b>_INTERNET_</b>
* Click <b>Next</b>
  > If radio button for <b>Use this public interface to connect to the Internet</b> is not available, sometimes it takes the previous step some time to sync so go back to the "Click <b>Tools</b>" step
  
![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Routing%20and%20Remote%20Access%204.png)

* Click <b>Next</b>

<h2>Step 10: Add and Configure DHCP Server Role</h2> 

* Click <b>Add roles and freatures</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Add%20role%20and%20Featues.png)
  
* Click <b>Next</b> 
* Click <b>Next</b> 
* Click <b>Next</b> 
* On <b>Server Roles</b> click radio button for <b>DHCP Server</b>
* Click <b>Add Features</b>
* Click <b>Next</b>
* Click <b>Next</b>
* Click <b>Install</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Add%20DHCP%20Role%202.png)
  

* Click <b>Tools</b>
* Click <b>DHCP</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Configure%20DHCP.png)

* Click the carrot for <b>dc.mydomain</b> 
* Right click <b>IPv4</b> 
* Click <b>New Scope</b> 

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Configure%20DHCP%202.png)

* Set <b>Name</b> to "172.1.0.100-200"
* Click <b>Next</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Configure%20DHCP%203.png)

* Set <b>Start IP address</b> to "172.16.0.100"
* Set <b>End IP address</b> to "172.16.0.200"
  > This allows up to 101 IP addresses to be made
* Set <b>Length</b> to "24"
* Click <b>Next</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Configure%20DHCP%204.png)

* Click <b>Next</b>
* Click <b>Next</b>
* Click <b>Next</b>
* Set <b>IP address</b> to "172.16.0.1"
* Click <b>Add</b>
* Click <b>Next</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Configure%20DHCP%205.png)

* Right click <b>dc.mydomain</b> 
* Click <b>Authorize</b> 

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Configure%20DHCP%206.png)

* Right click <b>dc.mydomain</b> 
* Click <b>Refresh</b> 

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Configure%20DHCP%207.png)

<h2>Step 12: Allow Browsing</h2> 

  > You normally wouldn't allow browsing on an AD DS but it's needed to download the PowerShell script for this lab


* Click <b>Configure this local server</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Allow%20Browsing.png)

* Click <b>Local Server</b>
* Click <b>On</b> next to <b>IE Enhanced Security Configuration</b>
* Click the radio button for <b>OFF</b> for <b>Administrators</b>
* Click the radio button for <b>OFF</b> for <b>Users</b>
* Click <b>OK</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Allow%20Browsing%202.png)


<h2>Step 13: Create User Accounts</h2>

* Open <b>Internet Explorer</b>
* Install <b>Microsoft Edge</b>
  > Internet Explorer is no longer supported enough for next step
  
![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Install%20Edge.png)

* Open [Create Accounts Script](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbm1iamctOWJGSUk4ZU5Ec3h1bDA0QXRoM2dxZ3xBQ3Jtc0tsMVZmVDZ5bVJYT1ZwWDFaeUFDQ01uY3lJNE9YSF9zTDZuUGZFTHJQaE05Sm42T091UWw1UXdXTFg2VTRqMFZkOHIyOXpNMVktU0VNTWs4dFlJQmdVQ3JEd3g1YUMwR1FLQnBsRm9Wai1DSDkzMHBpcw&q=https%3A%2F%2Fgithub.com%2Fjoshmadakor1%2FAD_PS%2Farchive%2Frefs%2Fheads%2Fmaster.zip&v=MHsI8hJmggI)
  > Script made by Josh Madakor
  > This script will automate the creation of over 1000 user accounts
* Download folder <b>AD_PS-master</b>
* Extract folder <b>AD_PS-master</b> to Desktop

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Extract%20Script%20to%20Desktop.png)

* Open <b>AD_PS-master</b>
* Open <b>names</b> .txt file
* Insert your name at top of the .txt file <b>Microsoft Edge</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Add%20name%20to%20note.png)

* Click <b>Windows Start Button</b>
* Click carrot for <b>Windows PowerShell</b>
* Right click <b>Windows PowerShell ISE</b>
* Click <b>More</b>
* Click <b>Run as administrator</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Open%20PowerShell%20ISE.png)

* Click <b>File</b>
* Click <b>Open</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Open%20PowerShell%20ISE%202.png)

* Click <b>Desktop</b>
* Click <b>AD_PS-master</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Open%20PowerShell%20ISE%203.png)

* Click <b>1_CREATE_USERS</b>
* Click <b>Open</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Open%20PowerShell%20ISE%204.png)

* In the PowerShell Terminal run command: "Set-ExecutionPolicy Unrestricted"

```
Set-ExecutionPolicy Unrestricted

```

* Click <b>Yes to All</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Set%20ISE%20Unrestricted.png)

* In the PowerShell Terminal run command: "cd C:\Users\[Admin User Logon Name]\Desktop\AD_PS-master"
  > This changes the directory to folder <b>AD_PS-master</b> so the script can pull the names for the new user accounts

```
cd C:\Users\[Admin User Logon Name]\Desktop\AD_PS-master

```

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Change%20ISE%20Directory.png)

* Click the Green <b>Run Button</b>
* Click <b>Run Once</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Run%20ISE.png)

* Wait for the script to finish creating the users


* Click <b>Windows Start Button</b>
* Click carrot for <b>Windows Administrative Tools</b>
* Open <b>Active Directory Users and Computers</b>
* Click carrot for <b>mydomain.com</b>
* Open <b>_Users</b> Organizational Unit
* Confirm that you can see the new user accounts

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Confirm%20Users%20were%20made.png)

<h2>Step 14: Create Client VM</h2>

* Open <b>Oracle VM VirtualBox Manager</b>
* Click <b>New</b>
* Name new VM "Client1"
* Click <b>Next</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM.png)

* Change <b>Base Memory</b> and <b>Processors</b> to an amount your computer can handle without taking too many resources

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM%202.png)

* Right click <b>Client1</b>
* Click <b>Settings</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM%203.png)

* Select <b>Advanced</b>
* Change <b>Shared Clipboard</b> and <b>Darg'n'Drop</b> to <b>Bidrectional</b>
  > Not necessary but allows a cleaner experience

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM%204.png)

* Select <b>Network</b>
* Select <b>Internal Network</b> from the drop-down menu for <b>Attached to</b>
* Click <b>OK</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM%205.png)

<h2>Step 15: Install Windows 10</h2>


* Turn On <b>DC</b> Virtual Machine
* Select <b>Next</b>
* Select <b>Other</b> from the drop down menu for <b>DVD</b>
* Click <b>Windows10ISO</b> from where you stored the download
* Click <b>Open</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM%206.png)

* Select <b>Next</b>
* Select <b>Install Now</b>
* Select <b>I don't have a product key</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM%207.png)

* Select <b>Windows 10 Pro</b>
* Select <b>Next</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM%208.png)

* Check the box for <b>I accept the license terms</b>
* Select <b>Next</b>
* Select <b>Custom: Install Windows only (advanced)</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM%209.png)

* Select <b>Next</b>
* Allow time for Installation
  > Installation may take a while and will require a restart of the VM
* Continue through Windows setup until the <b>How would you like to set up?</b> screen
* Click <b>Set up for personal use</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM%2010.png)

* Select <b>Offline account</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM%2011.png)

* Select <b>Limited Experience</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM%2012.png)

* Name Local account "user"
* Click <b>Next</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM%2013.png)

* Select <b>Next</b>
  > There is no need for a password

* Select <b>Accept</b> on <b>Choose privacy settings for your device</b> screen

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Create%20Client%20VM%2014.png)

<h2>Step 16: Connect Client VM to Domain</h2>

* Login to User Account

* Open <b>Settings</b>
* Click <b>About</b>
* Click <b>Rename this PC (advanced)</b>
* Click <b>Change</b>
* Name <b>Computer name</b> "Client1"
* Click radio button for <b>Domain</b>
* Name <b>Domain</b> "mydomain.com"
* Click <b>OK</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Change%20Client%20PC%20name.png)

* Enter <b>User Name</b> as [First Name Inital][Last Name]
  > Example: mdotson
* Enter <b>Password</b> as "Password1"
* Click <b>OK</b>

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Login%20to%20Domain.png)

* Click <b>OK</b>
* Click <b>OK</b>
* Click <b>Close</b>
* Click <b>Restart Now</b>
* Click <b>Other user</b> on login screen
* Login in to recently created account 

![image](https://github.com/WalterDotson02/Active-Directory-Practice/blob/main/images/Login%20to%20Domain%202.png)
