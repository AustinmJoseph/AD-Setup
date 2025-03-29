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
<h2>VM SEtup </h2>
First lets set up the domain controller. I went to azure, created my resource group and name it AD-LAb. I also created a seperate virtual network called ABV-Lab. Then create a virtual machine named DC-1 and have it image Windows Werver 2022, put it in the virtual network we just made. Then go into DC-1's network settins and set its ip address to static. Create another virtual machine and make sure the subnet is the one we just created. Get DC-1's Public ip address and sign into it, to disable the fire wall. I disabled the domain, private, and public profile firewalls. then logged into Client-1. AFter i logged into client one i tested to make sure client one could ping the domain controller, and checked the ipconfig by using "ipconfig/all" to see the output DNS was the domain controller.

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



