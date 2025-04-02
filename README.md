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

---

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
![firewall](https://github.com/user-attachments/assets/f9f7ea4f-9f86-4da5-a5fd-fc4183cd350d)
![ade14](https://github.com/user-attachments/assets/cd0259c7-f128-4945-854d-5df28f43d2b6)
![ade15](https://github.com/user-attachments/assets/754bd832-081d-49b4-b6a9-4e6a43ff7ad9)
![ade15 (1)](https://github.com/user-attachments/assets/a1cd5411-3e7a-4728-9e3d-b8c612a169ab)
![ade19](https://github.com/user-attachments/assets/ae2e1e60-05c9-4672-8b86-01ceea2d1b32)
![ade20](https://github.com/user-attachments/assets/b965231b-2526-4e64-8490-bb4c6a76dfad)
![ade21a](https://github.com/user-attachments/assets/0f9d6466-f550-456c-b41e-530fa67b591b)

---

<h2>Installing Active Directory </h2>

Now that we have the domain and Client-1 set up, let’s install Active Directory.

Go to Add Roles and Features in Server Manager, select Active Directory Domain Services, and click Next until you reach the install screen. After the installation finishes, click the flag with the yellow sign and select Promote this server to a domain controller. Choose to add a new forest, I set mine as myadlab.com. What ever you chose make sure to remember it.

I kept it simple by using Password1 for the domain controller options. Uncheck DNS delegation and click Next until you reach the Install button. Allow the installation to complete, and the server will automatically restart.

Once the VM has restarted, log in as a domain user. In Remote Desktop, I used myadlab.com\labuser and Cyberlab123! as the password.

---

![ade1](https://github.com/user-attachments/assets/8130b164-6baa-4302-87c1-77664d6ba2a2)
![ade2](https://github.com/user-attachments/assets/17d8e95c-71af-43af-be7f-53128dc3f33b)
![ade3](https://github.com/user-attachments/assets/9157d9c0-3b69-4dcc-8199-34813d47d959)
![ade4](https://github.com/user-attachments/assets/11c93a93-3765-4286-a42a-c7d684c2d6bf)
![ade5](https://github.com/user-attachments/assets/cac4d3f4-bbc5-4ac7-ad70-cea5274512bb)
![ad6](https://github.com/user-attachments/assets/a490e07b-a539-43af-92e5-3f612be34abd)
![ad7](https://github.com/user-attachments/assets/ef95c0af-4e78-4482-9e05-0dc988486edf)
![ad8](https://github.com/user-attachments/assets/644703bd-52b1-4841-aaf6-12ea4967f6e2)
![ad9](https://github.com/user-attachments/assets/d2e38282-44e8-4f62-92fe-3ea2fc4a22ab)

---

<h2> Creating a Domain Admin and adding Client-1 as a user </h2>

Now that Active Directory is installed, we are going to set up a Domain Admin and add Client-1 as a user of the domain.

Go to DC-1, open Users and Computers, and navigate to myadlab.com. Right-click > New > Organizational Unit, and name it _EMPLOYEES. Repeat the process to create another Organizational Unit named _ADMINS.

Now that these folders are set up, go to the _ADMINS folder, right-click > New > User. You can enter any name and logon name you’d like—just make sure to remember them. I used Peter Parker as the name and Not_Spiderman as the logon name, change the password setting to never expires for lab purposes and leave the password as Cyberlab123!.

Next, we need to make Peter an admin. Click on Peter’s name, go to Properties > Member Of > Add, then type Domain Admins and click Check Name. It should refresh—make sure to click Apply, and now Peter is a Domain Admin.

Since Peter is now a Domain Admin, we can sign out and use Peter’s account for everything else.

Now, sign into Client-1 , open Settings, and click Rename PC (Advanced). Then, click Change, select Member of Domain, enter your domain name, and log in with the admin account (Peter Parker). The vm should welcome you into the domain, and you will need to restart it.

Go back to DC-1, open Active Directory Users and Computers, and check under Computers to ensure that Client-1 is listed.

This setup was necessary to configure Active Directory for future labs that will require it.

---

![a10](https://github.com/user-attachments/assets/08d16c65-86b0-4903-9b11-e2ee5271f233)
![ade11](https://github.com/user-attachments/assets/044cb3c4-5527-4eef-af72-98cb5e550f27)
![a12](https://github.com/user-attachments/assets/8aeae419-fa72-47f0-aa35-6b442498c3fd)
![ade13](https://github.com/user-attachments/assets/b2484316-cceb-40e3-b8eb-e3ddada7f591)
![ade14](https://github.com/user-attachments/assets/ecca5262-dc6f-49d5-8881-016ec1e61a36)
![ade15](https://github.com/user-attachments/assets/d505b858-31a6-4f3b-9e2b-30c6b57a67fc)
![adelab last](https://github.com/user-attachments/assets/78856636-1177-46c1-9bd5-7fa6b238a3f2)
![adelab3](https://github.com/user-attachments/assets/ce37581c-a04d-4cb0-883d-621e8d2e6a05)
![ad16](https://github.com/user-attachments/assets/f0406eec-7fc5-49e7-a030-2273416ea796)

---



 


