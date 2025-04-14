<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Group Policy Objects</h1>
This tutorial outlines the implementation of Group Policy Objects in Active Directory with a focus on Account Lockouts.<br />

<h2>Prerequisites</h2>
Configure an on-premises Active Directory within Azure VMs using my previous project as a reference --> https://github.com/BrianRivera22/configure_AD/blob/main/README.md

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

1) Setup an Account Lockout within your Active Directory Infrastructure   
    - Configure Account Lockout Threshold in Group Policy
    - Lock yourself out of a user account to ensure the policy works (fun!)
2) Enable and Disable Accounts
    - unlock user account
    - observe ability to enable, disable, and reset passwords for users within Active Directory Users & Computers
3) Observe Logs within Event Viewer
    - Observe the logs on the client Machine


<h2>Deployment and Configuration Steps</h2>

<h4>1. Setup an Account Lockout within your Active Directory Infrastructure</h4>
<p>
<img src="https://github.com/BrianRivera22/AD_GPO/blob/main/AD%20Group%20Policy%20Objects/1.png"/>
</p>
<p>
Log into DC-1 as "mydomain.com\jane_admin", Go to Start -> Run -> gpmc.msc

Edit the Default Domain Policy

<p>
<img src="https://github.com/BrianRivera22/AD_GPO/blob/main/AD%20Group%20Policy%20Objects/2.png"/>
</p>
<p>
Double click on Account Lockout Threshold and set the amount of log in attempts to 5 and then click Apply.

<p>
<img src="https://github.com/BrianRivera22/AD_GPO/blob/main/AD%20Group%20Policy%20Objects/3.png"/>
</p>
<p>
Log into Client-1 as "mydomain.com\jane_admin" and employ the Group Policy Object (GPO) by enterong "gpupdate /force" into PowerShell. Make sure to open PowerShell as administrator. Then log off the VM.

Once updated, try logging into client-1 as any one of the users within the domain, but put in the wrong password 6 times. A lockout message should appear.

<h4>2. Enable and Disable Accounts</h4>
<p>
<img src="https://github.com/BrianRivera22/AD_GPO/blob/main/AD%20Group%20Policy%20Objects/4.png"/>
</p>
<p>
Back in dc-1, open Active Directory Users & Computers, in _EMPLOYEES find the user that we locked out (ben.cab) in this case and unlock their account.

<p>
<img src="https://github.com/BrianRivera22/AD_GPO/blob/main/AD%20Group%20Policy%20Objects/5.png"/>
</p>
<p>
After the account is unlocked, try logging into client-1 as that user.

We can also easily reset a users password here by right clicking their name.

<h4>3. Observe Logs within Event Viewer</h4>
<p>
<img src="https://github.com/BrianRivera22/AD_GPO/blob/main/AD%20Group%20Policy%20Objects/6b.png"/>
</p>
<p>
Using client-1 (as any user), go to Start and search for Event Viewer (eventvwr.msc) but open it as an administrator. We can use "mydomain.com\jane_admin" here. 

Note: This can also just be done directly on the domain controller without this step.

<p>
<img src="https://github.com/BrianRivera22/AD_GPO/blob/main/AD%20Group%20Policy%20Objects/7.png"/>
</p>
<p>
Event Viewer allows us to view security logs. On the left hand side go to Windows Logs -> Security

Right click on Security and click Find. Enter in the user name we were trying to log in as with the wrong password earlier. We can view the failed log in attempts we made.
