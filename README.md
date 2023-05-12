<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Network File Shares and Permissions using Active Directory</h1>
In this tutorial we will be sharing out resources over the network and creating file shares to allow read, write, or deny access to individual users or groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Deployment and Configuration Steps</h2>

<p>
Firstly make sure you have completed the previous Active Directory lab or you will not be able to complete this lab. In this lab you are required to have Active Directory running in Azure on a virtual machine (DC-1) and a client machine running in Azure on a virtual machine (Client-1) and joined to the domain.
<p>
<img src="https://imgur.com/vGk8Xd9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To start this tutorial off, we are going to create some sample file shares with various permissions. First connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin) then connect/log into Client-1 as a normal user (mydomain\"someuser"). Then, on DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”.
</p>
<br />

<p>
<img src="https://imgur.com/ObVMO2X.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
We are next going to set permissions for these folders. Right click on "read-access" folder and click properties. Next click on share, then in the search bar type "Domain Users" then add. Then set permissions level to read, so we have add this folder to the domain users group and user will only be able to have read access. See image above.
</p>
<br />

<p>
<img src="https://imgur.com/4dDCGlh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next do the same thing for the "write-access" folder but the permissions level should be "Read/Write". See image above.
</p>
<br />

<p>
<img src="https://imgur.com/EVXlBSW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
For "no-access" the group is going to be in "Domain Admins" and the permission level is Read/Write (Domain Users do not have access to Domain Admins). We are going to skin accounting for now.
</p>
<br />

<p>
<img src="https://imgur.com/ZlkqJJB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we are going to attempt to access file shares as a normal user. On Client-1 navigate to the shared folder by pressing windows key + R, then type "\\dc-1". Try to access the folders you just created. Which folders can you access? Which folders can you create stuff in?.
</p>
<br />


<p>
<img src="https://imgur.com/0VkQi32.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Moving on, we are now going to create an “ACCOUNTANTS” Security Group, assign permissions, and test access. Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS” in Active Directory Users and Computers. To do this make an folder if you dont all ready have one named, "_SECURITY_GROUPS" then right click in the folder -> New -> Groups-> Security Group -> Name: ACCOUNTANTS -> Ok.
</p>
<br />


<p>
<img src="https://imgur.com/aIap3YJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now on the “accounting” folder you created earlier, set the following permissions: Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”.
</p>
<br />


<p>
<img src="https://imgur.com/PZYwWYD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On Client-1, as "someuser", try to access the accountants folder. It should fail becuase the user that you are logged into does not have permission, so now we are going to give the user permission, first log out of Client-1 as <someuser>.
</p>
<br />


<p>
<img src="https://imgur.com/V1UTplR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To add your Client-1 user access to accountants navigate to DC-1 and open Active Directory Users and Computers if it is not already open. Then double click "ACCOUNTANTS" -> members -> add -> Type in users name that you are logging into on Client-1 -> Ok.
</p> 
<br />


<p>
<img src="https://imgur.com/RPwQsgR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, log back in to Client-1 and try opening accounting in \\dc-1, it should work. Congratulations, you have now finished the tutorial!
</p>
<br />

