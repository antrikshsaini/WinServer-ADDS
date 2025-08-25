# WinServer-ADDS

### **Hands-On with Windows Server 2022: Setting Up Active Directory Domain (ADDS), OUs, Groups, and Policies \| VM Ware** {#hands-on-with-windows-server-2022-setting-up-active-directory-domain-adds-ous-groups-and-policies-vm-ware}

### **🔹 Introduction** {#introduction}

In today's IT landscape, hands-on skills with **Windows Server and
Active Directory** are critical for system administrators, security
analysts, and IT professionals. As part of my learning and
skill-building journey, I designed and configured a complete **Windows
Server 2022 environment** from scratch.

This project covers everything from server installation to configuring
**Active Directory Domain Services (ADDS)**, creating users and groups,
implementing **Organizational Units (OUs)**, and applying **principle of
least privilege access controls**.

By the end of this article, you'll see how I:

- Installed and configured Windows Server 2022 on VMware

- Set up ADDS with a custom domain.

- Created OUs, groups, and users.

- Applied folder-level permissions using least privilege.

- Configured user restrictions (logon hours, computer access, account
  > expiration).

- Automated software installation at logon.

### **🛠️ Prerequisites** {#prerequisites}

Before starting this project, make sure you have the following:

- **VMware Workstation/Player** (or any virtualization
  > software) --- Used to create and run the Windows Server 2022 virtual
  > machine.

- **Windows Server 2022 ISO Image** --- Installation media required to
  > set up the server. *(Can be downloaded from Microsoft's official
  > evaluation site)*

- **Basic Networking Knowledge** --- IP addressing and subnetting
  > understanding.

- **Admin Privileges** on your local machine to configure the
  > environment.

### **⚙️ 1. Setting up Windows Server 2022** {#setting-up-windows-server-2022}

I started by creating a fresh installation of **Windows Server 2022** in
VMware with the following specifications:

- **RAM**: 2--4 GB

- **Storage**: 40--60 GB

- **Network Adapter**: LAN-Segment \#1

- **Server Name**: DC01

- **IP Configuration**: 192.168.1.200/24 with DNS set to 192.168.1.200

After installation, I also installed **VMware Tools** to ensure smooth
performance and integration.

![](media/image11.png){width="6.5in" height="4.958333333333333in"}

Set-up IP address **192.168.1.200/24 DNS 192.168.1.200**

![](media/image1.png){width="6.5in" height="3.638888888888889in"}

Run -\> ncpa.cpl -\> Ethernet -\> Properties -\> internet Protocol
TCP/IP

![](media/image46.png){width="6.5in" height="3.4722222222222223in"}

### **🏢 2. Installing Active Directory Domain Services (ADDS)** {#installing-active-directory-domain-services-adds}

Once the server was ready, I installed and configured **Active Directory
Domain Services**.

- Domain created: **antriksh.ca** *(replace with yourfirstname.ca)*

- Organizational Unit: **Montreal**

- Security Groups: **AMG** and **PMG**

Next, I created four users and assigned them to groups:

- AMSTD1, AMSTD2 → assigned to **AMG**

- PMSTD1, PMSTD2 → assigned to **PMG**

Click Add Roles and Features -\> Next -\> Next -\> Select Active
Directory Domain Services -\> Next -\> Next -\> Next -\> Install

![](media/image6.png){width="6.5in" height="3.3194444444444446in"}

Promote this to domain controller

![](media/image16.png){width="6.5in" height="5.111111111111111in"}

Add Forest

![](media/image3.png){width="6.5in" height="3.7777777777777777in"}

No DNS Dlegation needed because you are the Domain and Parent user

Click NEXT

![](media/image8.png){width="6.5in"
height="4.611111111111111in"}![](media/image9.png){width="6.5in"
height="4.694444444444445in"}![](media/image7.png){width="6.5in"
height="4.680555555555555in"}![](media/image24.png){width="6.5in"
height="4.875in"}

**Powershell script can be used tmp1511.tmp**

\#

\# Windows PowerShell script for AD DS Deployment

\#

Import-Module ADDSDeployment

Install-ADDSForest \`

-CreateDnsDelegation:\$false \`

-DatabasePath \"C:\Windows\NTDS\" \`

-DomainMode \"WinThreshold\" \`

-DomainName \"antriksh.ca\" \`

-DomainNetbiosName \"ANTRIKSH\" \`

-ForestMode \"WinThreshold\" \`

-InstallDns:\$true \`

-LogPath \"C:\Windows\NTDS\" \`

-NoRebootOnCompletion:\$false \`

-SysvolPath \"C:\Windows\SYSVOL\" \`

-Force:\$true

Create an OU= **Montreal**

Go to Tools and Active Directory Users and Computers

![](media/image23.png){width="6.5in" height="4.291666666666667in"}

Right click blank space New -\> Organization Unit -\> Montreal

![](media/image52.png){width="6.5in" height="4.819444444444445in"}

Create 2 groups called **\[AMG,PMG\]**

Right Click -\> New -\> Group

![](media/image17.png){width="6.5in" height="4.569444444444445in"}

Using Powershell

New-ADGroup -Name \"PMG\" -path \"OU=Montreal,DC=antriksh,DC=ca\"
-GroupCategory Security -GroupScope Global

![](media/image27.png){width="6.5in" height="2.5416666666666665in"}

Create 4 Users **\[AMSTD1,AMSTD2,PMSTD1,PMSTD2\]**

![](media/image2.png){width="6.5in" height="3.638888888888889in"}

**Using Powershell**

New-ADUser -name \"AMSTD2\" -GivenName \"AMSTD\" -Surname \"AMSTD2\"
-DisplayName \"AMSTD2\" -SamAccountName \"AMSTD\" -UserPrincipalName
\"AMSTD2@antriksh.ca\" -path \"OU=Montreal,DC=antriksh,DC=ca\"
-PasswordNeverExpires \$true -AccountPassword (Read-Host -AsSecureString
\"Please input the password\") -Enabled \$true

New-ADUser -name "AMSTD2" -GivenName "AMSTD" -Surname "AMSTD2"
-DisplayName "AMSTD2" -SamAccountName "AMSTD" -UserPrincipalName
"AMSTD2@antriksh.ca" -path "OU=Montreal,DC=antriksh,DC=ca"
-PasswordNeverExpires \$true -AccountPassword (Read-Host -AsSecureString
"Please input the password") -Enabled \$true

Get-ADUser -Filter \* -SearchBase \"OU=Montreal,DC=antriksh,DC=ca\"

![](media/image4.png){width="6.5in"
height="3.611111111111111in"}![](media/image43.png){width="6.5in"
height="4.416666666666667in"}![](media/image22.png){width="6.5in"
height="4.625in"}

### **👥 3. Adding More Users and Applying Restrictions** {#adding-more-users-and-applying-restrictions}

To make the environment more realistic, I created **3 additional users
per group**. These accounts were configured with different restrictions:

- One user allowed only to log in between **09:00--16:00**.

- One user restricted to join only **PC01**.

- One user with **account expiration**.

- One user **disabled**.

This demonstrated how administrators can enforce **access policies** and
**account lifecycle management** in AD.

Assign AMSTD1,2 to AMG

Assign PMSTD1,2 to PMG

Add-ADGroupMember -Identity "PMG" -Members PMSTD1,PMSTD2

![](media/image13.png){width="6.5in"
height="3.9027777777777777in"}![](media/image38.png){width="6.5in"
height="3.875in"}

AMSTD1 allowed to work only Mon to fri 7 to 5

![](media/image25.png){width="6.5in" height="3.4583333333333335in"}

AMSTD2 can logon on to computer Contracter-PC01

Contracter should not be on same VLAN netwrok

![](media/image19.png){width="6.5in" height="3.8333333333333335in"}

If person on holiday , disable their account, Right click on User and
Disable account

PKI, Probation period ends

![](media/image31.png){width="6.5in" height="3.4166666666666665in"}

### **Showcase On User End**

**Download Windows 10 and Install on New Virtual Machine**

[**[https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise]{.underline}**](https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise)

**Change settings**

![](media/image47.png){width="6.5in" height="3.5277777777777777in"}

**Logon On Windows 10 PC01 using AMSTD1**

**User is allowed only in the morning from 09:00 -16:00**

![](media/image45.png){width="6.5in" height="4.069444444444445in"}

**PMSTD1 user whose probation period is expired**

![](media/image15.png){width="6.5in" height="5.152777777777778in"}

User cannot access the PC, example contractor

**User account is restricted to join any PC than PC01**

![](media/image32.png){width="6.5in" height="4.361111111111111in"}

### **📂 4. Implementing Least Privilege with Folder Permissions** {#implementing-least-privilege-with-folder-permissions}

To test access control, I created a folder structure on **C:\Data**:

- Subfolders: Morning, Evening

Then applied the principle of **least privilege**:

- **AMG** → Full control of *Morning* folder; denied *Evening* folder

- **PMG** → Full control of *Evening* folder; denied *Morning* folder

**Create a new folder in local Disk C:\\ Data \[data\]**

**Within Data Create 2 sub folders called Evening , morning**

![](media/image35.png){width="6.5in" height="3.4583333333333335in"}

Disable Inheritance, Morning folder remove
Users([[Antriksh.ca]{.underline}](http://antriksh.ca))

![](media/image37.png){width="6.5in"
height="3.611111111111111in"}![](media/image39.png){width="6.5in"
height="2.9166666666666665in"}

Now we can remove Users

![](media/image30.png){width="6.5in" height="6.583333333333333in"}

Add AMG and PMG

![](media/image36.png){width="6.5in" height="5.458333333333333in"}

Assign the principle of least privilege \[ AMG → Full control to
Morning\] \[PMG → Full Deny to Morning Folder\]

![](media/image18.png){width="6.479166666666667in"
height="6.28125in"}![](media/image50.png){width="5.885416666666667in"
height="6.302083333333333in"}

Assign the principle of least privilege \[PMG → Full Allow Evening

If not in the list you are deny by default

![](media/image33.png){width="6.5in" height="4.361111111111111in"}

**Check permissions**

![](media/image42.png){width="6.5in"
height="3.7777777777777777in"}![](media/image48.png){width="6.5in"
height="4.527777777777778in"}![](media/image12.png){width="6.5in"
height="4.597222222222222in"}

Run \\dc01

Can see shared folder over network

![](media/image21.png){width="6.5in" height="3.5972222222222223in"}

Map Network drive to see the folder

![](media/image10.png){width="6.5in"
height="3.6666666666666665in"}![](media/image29.png){width="6.5in"
height="3.6527777777777777in"}

Current user is AMSTD1 can access only Morning Folder

What happened if click on Evening Folder

![](media/image49.png){width="6.5in" height="3.5in"}

Now go to DC01 Server manager -\> Files and Storage -\> Shares -\> Data
-\> right click properties

![](media/image53.png){width="6.5in" height="3.7083333333333335in"}

Enable Enumeration

![](media/image40.png){width="6.5in" height="4.277777777777778in"}

Therefore the folder which does not have permission will disappear

![](media/image28.png){width="6.5in" height="3.7916666666666665in"}

### **💡 Bonus: Automating Google Chrome Installation** {#bonus-automating-google-chrome-installation}

**How to install Google Chrome software on Users Computer on Logon**

As a bonus, I configured a **logon script** to install Google Chrome on
user machines when they log in for the first time.

This step highlights how administrators can **automate software
deployment** in an enterprise environment --- ensuring all users have
the required applications without manual installation.

Create folder on DC01 give permissions , download chrome msi and paste
in that folder

\\DC01\Software Deployment

Create policy in server manger

Go to Tools -\> Group Policy -\> got to Montreal OU

![](media/image51.png){width="6.5in" height="4.180555555555555in"}

Right click Montreal and create GPO

![](media/image5.png){width="6.5in" height="3.5in"}

There are 2 choices to deploy either User policies means wherever user
logs in it will install chrome first, Computer means it will install on
particular pc

Install on User so that it follows you

![](media/image20.png){width="6.5in" height="4.208333333333333in"}

Assign -\> will force the user to install either like it or not

Publish -\> user can install the software if needed

For now select assign

Right click on blank space -\> New -\> Package -\> Select chrome
installer -\> Open

![](media/image44.png){width="6.5in"
height="3.0555555555555554in"}![](media/image26.png){width="6.5in"
height="4.569444444444445in"}

Install at Logon.

Right click Properties

![](media/image14.png){width="6.5in" height="4.013888888888889in"}

Go to power shell, do update group policy manually otherwise it will
take 2 hour to take effect

Gpupdate /force

![](media/image34.png){width="6.5in"
height="3.5972222222222223in"}![](media/image41.png){width="6.5in"
height="5.138888888888889in"}

## **🏁 Conclusion** {#conclusion}

This lab project gave me a strong, practical understanding of how
**Windows Server 2022 and Active Directory** work in a controlled
environment. From installing and configuring the domain controller to
managing organizational units, groups, and user policies, I was able to
apply **real-world IT administration practices** such as least
privilege, time-based logon restrictions, and account lifecycle
management.

The experience not only reinforced my knowledge but also showcased my
ability to manage and secure enterprise-level infrastructure. Going
forward, I plan to extend this project by exploring **Group Policy
Objects (GPOs), security hardening techniques, and automation with
PowerShell**.

If you're a beginner looking to get started with Windows Server or an IT
professional brushing up on your skills, I hope this walkthrough
provides insight into what's possible with a hands-on approach.
