<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Group Policy Objects</h1>
This tutorial outlines the implementation of Group Policy Objects in Active Directory with a focus on Account Lockouts.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

1) Prepare Active Directory Infrastructure in Azure
    - Setup Domain Controller VM (Windows Server 2022) named “DC-1”
    - Setup Client VM (Windows 10) named “Client-1”
2) Deploy Active Directory
    - Create a Domain Admin user within the domain
    - Join Client-1 to your domain (mydomain.com)
3) Create users using PowerShell
    - Setup Remote Desktop for non-administrative users on Client-1
    - Create a bunch of additional users and attempt to log into client-1 with one of the users


<h2>Deployment and Configuration Steps</h2>

<p>
<img src=""/>
</p>
<p>
Word

