### Hands-On with Windows Server 2022: Setting Up Active Directory Domain (ADDS), OUs, Groups, and Policies | VM Ware

### 🔹 Introduction

In today’s IT landscape, hands-on skills with Windows Server and Active Directory are critical for system administrators, security analysts, and IT professionals. As part of my learning and skill-building journey, I designed and configured a complete Windows Server 2022 environment from scratch.

This project covers everything from server installation to configuring Active Directory Domain Services (ADDS), creating users and groups, implementing Organizational Units (OUs), and applying principle of least privilege access controls.

By the end of this article, you’ll see how I:

*   Installed and configured Windows Server 2022 on VMware
    
*   Set up ADDS with a custom domain.
    
*   Created OUs, groups, and users.
    
*   Applied folder-level permissions using least privilege.
    
*   Configured user restrictions (logon hours, computer access, account expiration).
    
*   Automated software installation at logon.
    

### 🛠️ Prerequisites

Before starting this project, make sure you have the following:

*   VMware Workstation/Player (or any virtualization software) — Used to create and run the Windows Server 2022 virtual machine.
    
*   Windows Server 2022 ISO Image — Installation media required to set up the server. (Can be downloaded from Microsoft’s official evaluation site)
    
*   Basic Networking Knowledge — IP addressing and subnetting understanding.
    
*   Admin Privileges on your local machine to configure the environment.
    

### ⚙️ 1. Setting up Windows Server 2022

I started by creating a fresh installation of Windows Server 2022 in VMware with the following specifications:

*   RAM: 2–4 GB
    
*   Storage: 40–60 GB
    
*   Network Adapter: LAN-Segment #1
    
*   Server Name: DC01
    
*   IP Configuration: 192.168.1.200/24 with DNS set to 192.168.1.200

### 

After installation, I also installed VMware Tools to ensure smooth performance and integration.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeI3YvZDIQvsZ2ZLzGbGFGEvuGDFZ04qBI4xjzkObISAS5aXVrve4aJNWjF49XYFCOtC4hby3ASTJJTocweoQaWUEtfDgJjbKT29XUmd7TGOuturHxOXbwHqpTRvrtWRblHkWqy?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Set-up IP address 192.168.1.200/24 DNS 192.168.1.200

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeDTop65j-XX7GMllERLNUd8g3M2BRQxLwIGtkgIhSwWlbbpqbGI8YQ2hvAACi6AmidJziJXxr0VEI-KDLXtUzR26B_1fcpZHo4IuAV7FKbhgiWFYgHACGdZ79HGasVhUPKyB_j9A?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Run -> ncpa.cpl -> Ethernet -> Properties -> internet Protocol TCP/IP

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf0srTEsfBFz7IB1Vy0jzsheeR0BZOfnZVHkIcrXxrK6D7jrl6iCuxW7k7OfY_iVibL_RUdQxlsFI9dBpaTvIHsTpxA7xzL5FD5SqlQYV9elRQWbth9utdaHfJp3x1zdYn1Iv-m?key=W2xKHEZUw2tbSB0Cqnh7hQ)

### 🏢 2. Installing Active Directory Domain Services (ADDS)

### 

Once the server was ready, I installed and configured Active Directory Domain Services.

*   Domain created: antriksh.ca (replace with yourfirstname.ca)
    
*   Organizational Unit: Montreal
    
*   Security Groups: AMG and PMG
    

Next, I created four users and assigned them to groups:

*   AMSTD1, AMSTD2 → assigned to AMG
    
*   PMSTD1, PMSTD2 → assigned to PMG
    

Click Add Roles and Features -> Next -> Next -> Select Active Directory Domain Services -> Next -> Next -> Next -> Install

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcFDq3Cxqj-lWo8_9I71BcJ_Ox9wX9VunIlqiXJPE17AUxSxWA8OIAMX8XlifaqU6ETyruOYUKGhidYbrOLwNwVG21zga5VTcxkJZ8G7-WOfnHRsfwcQ0rEPd0RB0antxCpWO_39w?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Promote this to domain controller

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfjNBevXror5cbEu12HR2VgECTkynlozOHHlKQ4GuBtwo3YqaJVIqn6gdxaPYZXlyb9t-wIvH6-muCoa6BfX-_tOaujg20RT1lg57OCI7UUeKeaxP6fc7Pd-iK6699HFbJbfnZhZQ?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Add Forest

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcleaKtd8ZPckmEAV8sSOULXMi591YnOWSMjEHCzA3cLim5kvwPE767aQJgZZnzN7DHMCYdXBMI10KG_nIKFb04afH0h5V-0R3dE4oL_klb2HsIDJBLvqROAMR4sK2JzE8v-yvsNw?key=W2xKHEZUw2tbSB0Cqnh7hQ)

No DNS Dlegation needed because you are the Domain and Parent user

Click NEXT

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfzGUOaK6wicZtWc6TMweIY3tDAJnKaV2lOIifVrlnhy935_c3ZHMCNrd0bNdkigR6Qwu_effUyeX1vf79KxJSsoH4YjGK0b7-nnOz_WLhMQ9S7igJT-BjKIfKbl02H675h5MhlXg?key=W2xKHEZUw2tbSB0Cqnh7hQ)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfbk9jdTAlP1k2WTdvHnqE63Z502aGdMRqHpwlbBf5hAH28iG92STH9wnKEYi9zzDmGpgZxd5s17SChk014tWK_MKvzg0or3tA3ZTT2RhdiChTS9tE--6CVLvVHPKztnlv8B7-7wA?key=W2xKHEZUw2tbSB0Cqnh7hQ)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeKXhu0OU7IXqEAzTis5F096jzSnYM7j7cGMfYr3ijOL0RNlkOkJkYhmTTamhVNu_n6jnK2-zLrQCFVTmTx7Q4Zi_fdZtfqWd0pyGkscvOfsrGgS9AuCr9WhJLLtosNL7-OtAkCUA?key=W2xKHEZUw2tbSB0Cqnh7hQ)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf0T7mclfaOexHA5BHXCjzUOru33tLX7l9Sd1yEye0A5sBkHkQyXJJDbhqBqWqb3roYW_8teQJWNm5unoa7lR4tWjdf7EmLoKaWSTgiR3LHtQ8YhYE_IfSqn-jbeyccHk7xaeFF_Q?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Powershell script can be used tmp1511.tmp

#

\# Windows PowerShell script for AD DS Deployment

#

Import-Module ADDSDeployment

Install-ADDSForest \`

\-CreateDnsDelegation:$false \`

\-DatabasePath "C:\\Windows\\NTDS" \`

\-DomainMode "WinThreshold" \`

\-DomainName "antriksh.ca" \`

\-DomainNetbiosName "ANTRIKSH" \`

\-ForestMode "WinThreshold" \`

\-InstallDns:$true \`

\-LogPath "C:\\Windows\\NTDS" \`

\-NoRebootOnCompletion:$false \`

\-SysvolPath "C:\\Windows\\SYSVOL" \`

\-Force:$true

Create an OU= Montreal

Go to Tools and Active Directory Users and Computers

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXebZNJ05MT7kWl2yERc6AUIuPc0vGhTPeZ94H4DuFRiAzjzPdye9cjglRXOoDds_mtI1s7NKAba8tvVkN85PLAJ_qge0Up2K92G4i98rDVpkUPOej5ad9QQiSyjsGDGGGl8pdRgcQ?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Right click blank space New -> Organization Unit -> Montreal

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdpMkuBbm8roZe_Mwwiv431guJHb_mXEdZG_59NMPYwx4rMobTx8FK6TgejKucXKVd6cC2vsghS7cGMQO2fLqJOM4VhS018ej-cow1Y1NTqMhQ3f-c6xueutQGD_aAY78smsD3TyA?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Create 2 groups called \[AMG,PMG\]

Right Click -> New -> Group

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe6mExgwLTiacbcbHxLmdVWTOJm8ZfMAnjd68tTFK9tEWh3Q674yAX_tpHUh3dJUORcw34fqC7de8isoazWBHICg1h8kAUtJ1ECzaxdvKZm71x7CNuz3tIF4qdF6I_iU0Bjhw_DhA?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Using Powershell

New-ADGroup -Name "PMG" -path "OU=Montreal,DC=antriksh,DC=ca" -GroupCategory Security -GroupScope Global

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeX6LgydtJSwi53pTdUnyKPDAqZV-nR5A0ITQsa12znKB5fFgrI6c5UG1q2jK782X_r4jPhBkplcgWqVDoUcDJzSWzLmQQknzqcmXwT8PMkiuIJ6UyhBOOj4rtJVY24xn3eqsWX?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Create 4 Users \[AMSTD1,AMSTD2,PMSTD1,PMSTD2\]

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdRa7uGyj2hwkedVB13lkesvks1ijQMoNLP8umQKLBA2j1CUJP2ZxDSYCJqTD7zwfg2tIRxWSO54TDogDPE3SNr4bnlTQlCIP3-whkvPryzJJO17skOdvIHgyLYspc2lLMj5TE2zA?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Using Powershell

New-ADUser -name "AMSTD2" -GivenName "AMSTD" -Surname "AMSTD2" -DisplayName "AMSTD2" -SamAccountName "AMSTD" -UserPrincipalName "AMSTD2@antriksh.ca" -path "OU=Montreal,DC=antriksh,DC=ca" -PasswordNeverExpires $true -AccountPassword (Read-Host -AsSecureString "Please input the password") -Enabled $true

New-ADUser -name “AMSTD2” -GivenName “AMSTD” -Surname “AMSTD2” -DisplayName “AMSTD2” -SamAccountName “AMSTD” -UserPrincipalName “AMSTD2@antriksh.ca” -path “OU=Montreal,DC=antriksh,DC=ca” -PasswordNeverExpires $true -AccountPassword (Read-Host -AsSecureString “Please input the password”) -Enabled $true

Get-ADUser -Filter \* -SearchBase "OU=Montreal,DC=antriksh,DC=ca"

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe1m9lz604MPzN3viXDoRgtDPMdpODOn_c6J2C6Y5cwScEd-2Sg6zFc1hpFZOvXDt0oHEebsgTxd--PpQE1E42K6tczxV9kKL_lX0IeNRsYfQh6CRXuMuK2GqPBAFXXLnnYjki3sQ?key=W2xKHEZUw2tbSB0Cqnh7hQ)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdhJrk-47MHQVcYfRB6PfprsS7Pk10JmVjI-w4LWLuvqx_BS5yb-7babrLHIp344BRhrPYiMZmRzLwXHOmHlCY7Z4LR1A84hNc8eTAwEp3FFTGEf-cYHD6WSqX6YU1lmUzzdpdLMQ?key=W2xKHEZUw2tbSB0Cqnh7hQ)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc92WY-gWEXInOXWFrQlz6J2UV3HZwVdiVeSdfN2UjOQAwjk1n0YLeKVyDlVv-PZe2O27ml7yfyaYZRtgGh9Tyn4UjghvllJR8NSNGMtvwE7NqLEj0ANuFy1fGVrLRpIwLoi5UR?key=W2xKHEZUw2tbSB0Cqnh7hQ)

### 👥 3. Adding More Users and Applying Restrictions

### 

To make the environment more realistic, I created 3 additional users per group. These accounts were configured with different restrictions:

*   One user allowed only to log in between 09:00–16:00.
    
*   One user restricted to join only PC01.
    
*   One user with account expiration.
    
*   One user disabled.
    

This demonstrated how administrators can enforce access policies and account lifecycle management in AD.

Assign AMSTD1,2 to AMG

Assign PMSTD1,2 to PMG

Add-ADGroupMember -Identity “PMG” -Members PMSTD1,PMSTD2

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdekCLxpLY9wyKrbvm9YKlYkuC_C89L4sf36ULBZay_vINW5WmJtXeQntijy39zGYjSB2J5048E8W74h5oQpyN6XW95W8Gm3JI0NqvntHDViBSc2ImyHPuFhcySPsuIyQ84aAVi7g?key=W2xKHEZUw2tbSB0Cqnh7hQ)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcS_SCCKuWNiigq8PLFp9gaEONmgk9nq6I7s2eex0ibm-M9OQ1NQLF-x4eSzegJbx5vcuNyAZNTKtxQ7On-QHF7j3yS7AHJQ_3ddNDOh1KEkfjzRgroIBUOyHULR3HKNo1JfDOg?key=W2xKHEZUw2tbSB0Cqnh7hQ)

AMSTD1 allowed to work only Mon to fri 7 to 5

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdeJg2UEW8hDeJoGtd97DXx6SVnp9E-FAvc3-7kAeBEgBsh4zZDFFOo9T3ZYOtvyv0-m5kngIWwLd_kyt9n72Zzpb7owrEvWAMnDH1q_KhHTTdkuUd-NA-fqQxLFVv5KwBqT-7Z2A?key=W2xKHEZUw2tbSB0Cqnh7hQ)

AMSTD2 can logon on to computer Contracter-PC01

Contracter should not be on same VLAN netwrok

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcpM8ibO8qmHVzgO6FrBIJirABGNE6wImmNwZayfexI8zwjmuYDtNOx9W1-lytNCY-OXCcinDRwwTcUuQhJrcgXZgGva9l3mNX9tvbUqVRy4bzLpSK8v8zxhLCYoS7nPRUrW1yCQQ?key=W2xKHEZUw2tbSB0Cqnh7hQ)

If person on holiday , disable their account, Right click on User and Disable account

PKI, Probation period ends

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc_j5oilDfZWkuvAMqR64I4tTdxXa0Uq-k5RbmWCFRJVYivXvwdOD2s2niLyaAfUcY1c4Gr_y6VDVtKyslJQS55EliDMXypUPCBzHaHXTCtrDDFGXMt0r1SnqXh0tuQVdmAbTS6?key=W2xKHEZUw2tbSB0Cqnh7hQ)

### Showcase On User End

### 

Download Windows 10 and Install on New Virtual Machine

[https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise](https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise)

Change settings

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf4S5jqWjDql5gyD7nUJEmVjGaLjF8p3zhph5pMVbc5kfHDuJWTPhJIzd4jHjraysueiV6zeUy_etEZzGygNg_nsi714NFn1Z-M8Mhdik6YUToV8BdYnpWLUMDQp1YSTNEYOFK19w?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Logon On Windows 10 PC01 using AMSTD1

User is allowed only in the morning from 09:00 -16:00

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcWmDRYAjeyqZw0BfkjyLRXI9dxUgb4UIBrp7vfmtBuaURoct73_VYTXEkvHJ25Ey68fyIwh_gRU25Hnq_V9PeN9MiVsrkfWEkwE2CpU9TD8aU7WAgEo0roJc5Zf45zUP1oOb5JEg?key=W2xKHEZUw2tbSB0Cqnh7hQ)

PMSTD1 user whose probation period is expired

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdES9EHuhKXe6EdqnjJQfq0mKCzS2QaW7U5cJGnezXnf4hiViceYYVnCYaUrprwehJ0arOiXBfMaJaxH3z5F3xMA3-ldQl6j00JJ59a4h5pyQ9frjnzRfOO9kIcZNaKkBGaB7oifA?key=W2xKHEZUw2tbSB0Cqnh7hQ)

User cannot access the PC, example contractor

User account is restricted to join any PC than PC01

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXczrndcog-3Y6YPwCveRzW3mZLejXUJ98gJqALJoj6qIazSZb4L3jP_X996tyrajNQ7hfVjcCALJ_BrVG0qc-VMceGEsc5W2JLDrsR8Nvn2581V6Vn1QHhKvKyAIFnHXhOoUvDbUw?key=W2xKHEZUw2tbSB0Cqnh7hQ)

### 📂 4. Implementing Least Privilege with Folder Permissions

### 

To test access control, I created a folder structure on C:\\Data:

*   Subfolders: Morning, Evening
    

Then applied the principle of least privilege:

*   AMG → Full control of Morning folder; denied Evening folder
    
*   PMG → Full control of Evening folder; denied Morning folder
    

Create a new folder in local Disk C:\\ Data \[data\]

Within Data Create 2 sub folders called Evening , morning

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXemhpu3oXyfPOgxoJsd6chKR8d-Xh4QabeWcFPnm5zDzG52toRh_kmA7097-l9vjyQl-JqBZth2UbRgmMN_ON1YZlkUHeNin3Rsn4ijiOuwJnZVypzH-fxqZNtbCeoh8dL7ZP2Z?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Disable Inheritance, Morning folder remove Users([Antriksh.ca](http://antriksh.ca))

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcDcMGaHBmidVVBmyt-dizAkUpFRFvw0KhIubXX2-TjDQThXtx3unj5eSdtgInnPYAEqKIWM-X6ewm2GtO3aAoeyOT681b_sGAJboTyWtW8tAYS2spx1EKBpWlnOwugurWYhKIgOw?key=W2xKHEZUw2tbSB0Cqnh7hQ)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdHg153dBKOGcvxWmH8uDav2OhGEVNk39GKfrutMP9497bFriESW33YXdjpoJKbyzAHR2-4h3vgLT6Ha7T1BIgJxMsKrZvzr5S7dVpRNob0MsqmM4gCDYlJODwwQJltjSxf80Z-Uw?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Now we can remove Users

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeJHfFiQQ0BHkDPIAdCXzsS3Tlaqc4FKcP0lS0xvb_xiPMxNEQlykFePgaRfOuNuX0ZV7bz2pKXeW66a4UxdOuBXHQ79wzKca5JOhvualxTw5TlsCFriRtsH9sVoqw89B3mXTD_Lg?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Add AMG and PMG

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfKlA1ovCVsBrn8BHgQLxsg5NMFcfbI0mtf6MpBIxzihPuM1jIBpkjWJggOlO6a2235s5cZdn-QCyTbfvVSAWQvGGAr4SQWqmViQLhpgvjwkY1uO6M6im2j_dKS9MFT3xRq47GM?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Assign the principle of least privilege \[ AMG → Full control to Morning\] \[PMG → Full Deny to Morning Folder\]

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc1DTvQmu-yhDIwnk0SpLyXLPfEqMK5kpWWmXXWwgZQmp4wl2MP4RvHlLY6buZ7rQGXap82lhFm7dpw6-X51shzy822nm_WFNIuvDmvVOeoUcYcFhGGafKCK2zzfG--w30CXtNqBg?key=W2xKHEZUw2tbSB0Cqnh7hQ)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeepHSQs4X7ksxn0rUpTLv4EqpFe8c6oE-7tmAq30fui2hDHdfVHtq4kMdMpVKm7vqZ_yok02UygrvBtw8ntXD-TjnnVRSiLQNr7N-QqaqaHFqFNJjp7NCVmj-flhT4S85vFVV-zw?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Assign the principle of least privilege \[PMG → Full Allow Evening

If not in the list you are deny by default

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfrao3VYt4bLFxIEerz5oHjl5Jb9OCBVLEc2FnWks5rL8o90ZZ5RW-kSXR2MyWmJCAIYa1Hoj8-UxvP9jECPlfmT3zlKarpTpEUkMxEijYoIU0pXTo7O81cMFf5DniGBLnaCiUXvw?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Check permissions

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfhN581ouLDoBCnjvIJIN0US6SAeg9t_uS94BXhuWdrMwkUqnLF-oVm6xibv216pYYj2P7y9o05se5TGjcj4eeNF-oMBU7vjUwqJy70lC1aeDAPqKQWqwkVV3x7i6e9WNPiDGChnQ?key=W2xKHEZUw2tbSB0Cqnh7hQ)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfmlDHVH3H5bxSJXQzahHrGs-BJz2nV_A4gQwlxHMvCn4hnh22cpL31AlC2lIx_xiOr5dERK9bspYDfaNHmyUAq52Tm30uJTFfWF8wQdwgheb-As9Ue73cnDl0scwFUDv1aM2eVyg?key=W2xKHEZUw2tbSB0Cqnh7hQ)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXex5MdrtY8O8tD9-WRpP-g4LE4Qm3GM4bzMqE8ZGb_PBn_QiAlPi-fTpVPZjCvLY1MraOjKutHxHxDc5NRxvd9FdlzFlN-jlpLpUh4h1NnNSgCydGWbtdUgIezhw7L025Y5NRZ0Vw?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Run \\\\dc01

Can see shared folder over network

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXec0xN6AXwVyFP003yYqQ4TUAflZ9D1HiWsWwhXfWoE0b4MTohyqg4IJ8o1dMNRXLE6SriMcQcl1u3zCDGR4Pr9aFIiN96tL50PwRhD6BRVkju9I2qkcA6Aq7AVMfNDleO1iIOxew?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Map Network drive to see the folder

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcJk1QaRdunPIhEveGfEbajvlvEd1xJmgTTI_Mh85UoK--NIekrSeaQsOfrcEauzd0XT11nGX5LRL5yaKFVyVPsLMEfKawcTEKSnySoHITIvYYlyTGFGcODC-_jnqRSfJEZWVspkA?key=W2xKHEZUw2tbSB0Cqnh7hQ)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfVMGcLaeqAj2xZOqws7FI4E8IPzHfki1AwwNUaEGwfQZlw-O2Xza3piJglANro2ATHuPDdWb_dUtxgRUX5TP4IPhyrXFB3VIOcX8ZjhA9cfigk7nw-7_DhFM8Z2swiag1wU-XVuQ?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Current user is AMSTD1 can access only Morning Folder

What happened if click on Evening Folder

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc7PzeWgpb2z0tmdJuV-GCmsAYryEoSvPxfMyY0r8iqXlUE8ArIlvZZkTpXf6cLc6MME7dDY5iUJVLSyulIjGGgsYf6o-EAq0nKSY_0f9bQPECA6qdLdxcKmJuTXbRKuw6nAJ9hww?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Now go to DC01 Server manager -> Files and Storage -> Shares -> Data -> right click properties

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfvicOlsg4BilvU6Bn_YVMYxwhtOLfZ7AdPCbb_xVX_JV9enVUjAHh82bpEGKp6PUte14mSnFcBwKrYPNq5zH7WvNMmB0dW5MI4FdVgkVaAvk2elp1gYfSq0uBlN9HDxmZwhwSY8A?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Enable Enumeration

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeS0q3TuRp0cycWLL-fEW99E4dxvRMUzbm4zY_RbP-lc3VMtJTuuE2b7Jejo-G2igXOQl9KEafaGcPJX1TN-RGtmOd2bdV3wSiVyIqKIwBxl8IYZ-77GnKxYk1G1fDdShcA5SDU?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Therefore the folder which does not have permission will disappear

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd2vy3mbg9Ll1xfzTwGyhJSmTxmVyw0ASdzhAM2Xl-o40Wd3RcssC0O-d6a5wVluUlQV6aNUIKBw4S237Bbl5h4Thc1OkKyRbhZwNEIUlGljd0s_llVw7h6U4NvZjnhf84qTR8aBw?key=W2xKHEZUw2tbSB0Cqnh7hQ)

### 💡 Bonus: Automating Google Chrome Installation

### 

How to install Google Chrome software on Users Computer on Logon

As a bonus, I configured a logon script to install Google Chrome on user machines when they log in for the first time.

This step highlights how administrators can automate software deployment in an enterprise environment — ensuring all users have the required applications without manual installation.

Create folder on DC01 give permissions , download chrome msi and paste in that folder

\\\\DC01\\Software Deployment

Create policy in server manger

Go to Tools -> Group Policy -> got to Montreal OU

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcXTO6KyYZFUQpq4R6Zu49xp_x0j3WNdhKeUkomntmb0ntgk5DfarWWdovxYqdGPTBSH6ROKXJQbYlWnqZh1lx7Pl3wu7RbFkwGN328wwYaeEKzTYwrQL-PvBpg1vRm9SoQx7bTLg?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Right click Montreal and create GPO

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfB0mh0DMPIELeaPlUVFyt7rLqVoX2IQPFsia0mIAhx5iihuyTFC0-xB1pR0oEMPU_qcZq8QCDSZudBmjdQ3qZd26vt9SdOMK3zgx3konqlCJQuypJH1HTPE27AyLDlkZf_W8ISbg?key=W2xKHEZUw2tbSB0Cqnh7hQ)

There are 2 choices to deploy either User policies means wherever user logs in it will install chrome first, Computer means it will install on particular pc

Install on User so that it follows you

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd-eso9eSrKJ_gvNDc60o8sSs-I34RKxYqsRXMsOZ1eKc-VbioVwsPMHFE8Ioc_nnrNrQBoungNgizFIV3PPZFqhuSc7lhjk0qkIpKEAQ3eCYb9pVHvoNRcMCIoYaQL13taa3cW?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Assign -> will force the user to install either like it or not

Publish -> user can install the software if needed

For now select assign

Right click on blank space -> New -> Package -> Select chrome installer -> Open

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf9MLVxlKUQu6lOXmPiX2aqmInxWhbl06IAuHRIV69P9wlE_iAtuquctVJcLJZmVCqgg2y80TQ595YGpWKVCWM6hl14VlkbFndLLzfu_869B21vI7smgl6uyB58G2maNothvyQJ2w?key=W2xKHEZUw2tbSB0Cqnh7hQ)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcpbGyMIWT230p5lNUwrDyh2CILz8XpazhL2JOUsWc9gdQDQ3r_jruc_ojPiQ_HbQ8X-ZlW5YEXUtG3k14aABPax1S-Ph1Ic_Od3fZwByIKB40cXRwcoyXtDl8O2SFVM4Eab-3p_w?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Install at Logon.

Right click Properties

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfphYESoMcT8qzI1Rcc5PggqPOEnT_0Htu0RmmB3kumAKmGkELgrOQGTxAR-t3hYHrtvXJtzDUG245EXAg8-lwf4wOteRCjoTQI7zxYW-oWcRhVM8OKcdgfMcNsrHMG73vKpaOZ7g?key=W2xKHEZUw2tbSB0Cqnh7hQ)

Go to power shell, do update group policy manually otherwise it will take 2 hour to take effect

Gpupdate /force

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXck2aIGx3ZnYiaK-LZ779-WiCBKV240GeSNTvA5bWBv6eS7L8hfmO0CR74wL_SxlG-Xf78DRyFg1sl1YijrRGnHzhKJo2hXRqMPiQ49utA7Qz2G7kDG76Ba-ZBN50DQV1oS_CKEPQ?key=W2xKHEZUw2tbSB0Cqnh7hQ)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeC8W_v07yyo4cFg5eZZ2Uq1IVfvpEP-D_sNVoyowvCah2poZU8uYnfTG9Doh0DKbV-XcnucGven9_zT6ZT3R38jcxgRa-aR3PpPbt5vJSM9_3Q3EEs1nYq5NdQtjklvxgtI9Oapg?key=W2xKHEZUw2tbSB0Cqnh7hQ)

## 🏁 Conclusion

### 

This lab project gave me a strong, practical understanding of how Windows Server 2022 and Active Directory work in a controlled environment. From installing and configuring the domain controller to managing organizational units, groups, and user policies, I was able to apply real-world IT administration practices such as least privilege, time-based logon restrictions, and account lifecycle management.

The experience not only reinforced my knowledge but also showcased my ability to manage and secure enterprise-level infrastructure. Going forward, I plan to extend this project by exploring Group Policy Objects (GPOs), security hardening techniques, and automation with PowerShell.

If you’re a beginner looking to get started with Windows Server or an IT professional brushing up on your skills, I hope this walkthrough provides insight into what’s possible with a hands-on approach.
