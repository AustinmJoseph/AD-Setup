<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory set up on Azure</h1>
This tutorial shows how active directory is set up on Windows virtual machines within Azure.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
  
<h2>Domain Setup </h2>

First, let’s set up the domain controller.

I went to Azure, created a resource group, and named it AD-Lab. I also created a separate virtual network called ABV-Lab. Then, I created a virtual machine named DC-1, selected Windows Server 2022 as the image, and placed it in the virtual network we just created.

Next, I went into DC-1’s network settings and set its IP address to static.

After that, I created another virtual machine, ensuring it was imaged with regular Windows 10 (not Server) and that it was on the same subnet.

I then retrieved DC-1’s public IP address, signed into it, and disabled the firewall. I disabled the Domain, Private, and Public profile firewalls.

Then, I changed Client-1’s DNS configuration to use DC-1’s IP address, restarted Client-1, and signed into it.

After signing into Client-1, I tested connectivity to ensure it could ping the domain controller. To double-check, I ran “ipconfig /all” to verify that the DNS server was set to DC-1’s private IP address.

![ade1](https://github.com/user-attachments/assets/34c65dcb-8407-45da-9886-8085c1cb303b)
![a2](https://github.com/user-attachments/assets/b01629df-7494-425b-b2f7-10f8d5da7119)
![aze3](https://github.com/user-attachments/assets/63d6ec00-a5f4-4444-96d1-1c5960417f9c)
![ade4](https://github.com/user-attachments/assets/813dafa1-2406-4e6a-93c0-8d446106e118)
![ade5](https://github.com/user-attachments/assets/2a6f0944-9a8b-4eab-89ae-e26fbc04a26e)
![ade6](https://github.com/user-attachments/assets/811493e1-bacd-48ae-bf3b-c3a978702bb6)
![ade7](https://github.com/user-attachments/assets/198fa827-5e32-4044-976d-03574397e6cc)
![ade8](https://github.com/user-attachments/assets/653cbedf-5ad2-43e4-b2bc-7177164a1313)
![ade9](https://github.com/user-attachments/assets/6cd18429-1e97-4234-bce7-562a32de73af)
![ade10](https://github.com/user-attachments/assets/6ccf71b4-3c6f-408d-bd4a-9041c1c72044)
[ade11](https://github.com/user-attachments/assets/365784ee-5dcb-4f6a-a6c3-93bf3170671c)
![ade12](https://github.com/user-attachments/assets/1d8997fa-4cb0-429e-976b-79d635b37992)
![ade13](https://github.com/user-attachments/assets/2866823c-8537-4185-bbfb-aa29333a5b22)
![ade14](https://github.com/user-attachments/assets/cd0259c7-f128-4945-854d-5df28f43d2b6)
![ade15](https://github.com/user-attachments/assets/754bd832-081d-49b4-b6a9-4e6a43ff7ad9)
![ade15 (1)](https://github.com/user-attachments/assets/a1cd5411-3e7a-4728-9e3d-b8c612a169ab)
![ade19](https://github.com/user-attachments/assets/ae2e1e60-05c9-4672-8b86-01ceea2d1b32)
![ade20](https://github.com/user-attachments/assets/b965231b-2526-4e64-8490-bb4c6a76dfad)
![ade21a](https://github.com/user-attachments/assets/0f9d6466-f550-456c-b41e-530fa67b591b)

<h2>Installing Active Directory </h2>

Now that we have the domain and Client-1 set up, let’s install Active Directory.

Go to Add Roles and Features in Server Manager, select Active Directory Domain Services, and click Next until you reach the install screen. After the installation finishes, click the flag with the yellow sign and select Promote this server to a domain controller. Choose to add a new forest and set the forest name as myadlab.com.

I kept it simple by using Password1 for the domain controller options. Uncheck DNS delegation and click Next until you reach the Install button. Allow the installation to complete, and the server will automatically restart.

Once the VM has restarted, log in as a domain user. In Remote Desktop, I used myadlab.com\labuser and Cyberlab123! as the password.

<h2> Creating a Domain Admin and adding Client-1 as a user </h2>

Now that Active Directory is installed, we are going to set up a Domain Admin and add Client-1 as a user of rhe domain.

Go to DC-1, open Users and Computers, and navigate to myadlab.com. Right-click > New > Organizational Unit, and name it _EMPLOYEES. Repeat the process to create another Organizational Unit named _ADMINS.

Now that these folders are set up, go to the _ADMINS folder, right-click > New > User. You can enter any name and logon name you’d like—just make sure to remember them. I used Peter Parker as the name and Not_Spiderman as the logon name, leaving the password as Cyberlab123!.

Next, we need to make Peter an admin. Click on Peter’s name, go to Properties > Member Of > Add, then type Domain Admins and click Check Name. It should refresh—make sure to click Apply, and now Peter is a Domain Admin.

Since Peter is now a Domain Admin, we can sign out of Lab User and use Peter’s account for everything else.

Now, sign into Client-1, open Settings, and click Rename PC (Advanced). Then, click Change, select Member of Domain, enter your domain name, and log in with the admin account (Peter Parker). The PC should welcome you into the domain, and you will need to restart it.

Go back to DC-1, open Active Directory Users and Computers, and check under Computers to ensure that Client-1 is listed.

This setup was necessary to configure Active Directory for future labs that will require it.



 


