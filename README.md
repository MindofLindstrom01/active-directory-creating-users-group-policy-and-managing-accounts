<p align="center">
  
![1-1](https://github.com/user-attachments/assets/899a9de9-9453-47f4-bc7c-5f0f4a96e312)

</p>

<h1>Creating Users, Group Policy, and Managing Accounts with Active Directory in Azure</h1>
<h2>Description</h2>
This project will demonstrate how to configure Remote Desktop for non-administrative users, automate user creation with PowerShell, and manage group policies. Additionally, I’ll cover account lockouts and log monitoring to simulate a real-life IT environment. Join me as I dive deeper into deploying Active Directory and enhancing system management skills!<br/>
<br/>
This project is a continuation of <a href="https://github.com/MindofLindstrom01/Preparing-Active-Directory-Infrastructure-in-Azure">Active Directory: Deploying Active Directory in Azure<a/><br/>

<br/>

You can find the Powershell script I run in this project here

<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Virtual Machines
- Remote Desktop Connection
- Active Directory

<h2>Operating Systems Used </h2>

- Windows 10 Pro</b> (22H2)
- Windows Server</b>

<h2>Project Walk-Through:</h2>

<h3>Step 1.</h3>

![1  server manager add features](https://github.com/user-attachments/assets/af068e14-5eea-495f-a86a-7ad393c160ca)

<p>Using the domain controller vm, search for Server Manager in the Windows Search bar and open it, then click "Add roles and features"</p>

<h3>Step 2.</h3>

![2  select AD domain services](https://github.com/user-attachments/assets/4d8de704-6c1c-43cf-a3d8-28b16c81e00a)

<p>Click next until Server Roles, then check Active Directory Domain Services</p>

<h3>Step 3.</h3>

![3  click add features](https://github.com/user-attachments/assets/5729cfdd-8cd3-40b8-ac00-6da435d0e024)

<p>Click Add Features</p>

<h3>Step 4.</h3>

![4  click install](https://github.com/user-attachments/assets/e7fce37d-da8f-42fa-a8d7-8ab6a2c5bf90)

<p>Check the box, then click install</p>

<h3>Step 5.</h3>

![5  install success](https://github.com/user-attachments/assets/996c1b39-73be-4b5c-884b-9a173eeec1a6)

<p>The installation should have succeeded, click close, now a restart will take place</p>

<h3>Step 6.</h3>

![6  promote to domain controller](https://github.com/user-attachments/assets/da0e2acb-4689-4ed3-9d62-640561674a51)

<p>After logging back in to the vm, go to the Server Manager, click the flag in the top right corner, then click "Promote this server to a domain controller".</p>

<h3>Step 7.</h3>

![7  new forest](https://github.com/user-attachments/assets/b1f0c3a2-1bb4-4b54-bdfe-284e8bb0d3fb)

<p>Select Add a new forest, name the domain, then click next</p>

<h3>Step 8.</h3>

![8  set pass](https://github.com/user-attachments/assets/66df412d-80cd-40c4-bdf9-4f3d05b64ec0)

<p>Create a password for DSRM, then click Next</p>

<h3>Step 9.</h3>

![9  click install](https://github.com/user-attachments/assets/278ae451-2d62-45d7-9de8-e0a18468ffb7)

<p>Click Install</p>

<h3>Step 10.</h3>

![10  configuration successful](https://github.com/user-attachments/assets/451d00c0-5ed4-4cfe-b80b-eea27a80b466)

<p>Now this server should successfully be configured as a domain controller</p>

<h3>Step 11.</h3>

![11  login as domain user](https://github.com/user-attachments/assets/a64b3fa3-38bc-4e5f-a8b2-fe560bbe0f86)

<p>Now attempt to log back in as a domain user using the domain name followed by the vm username</p>

<h3>Step 12.</h3>

![12  open ADUC](https://github.com/user-attachments/assets/17de8292-ce5c-4942-a0b1-74b45e02b812)

<p>Once inside, search "Active Directory Users and Computers" inside the Windows search bar and click it</p>

<h3>Step 13.</h3>

![13  create new org unit](https://github.com/user-attachments/assets/a56d16ea-8245-4027-a82d-98a7089b9e83)

<p>Right click the domain name, go to New, and click Organizational Unit</p>

<h3>Step 14.</h3>

![14  org units created](https://github.com/user-attachments/assets/65772f3a-a4a7-4be2-af84-1a6989cfcd18)

<p>Create two of these, one named _EMPLOYEES, and one named _ADMINS. These names must match exactly for the script to find them that we will use later</p>

<h3>Step 15.</h3>

![15  create new admin](https://github.com/user-attachments/assets/f1025acf-3224-425e-a30b-0757a04bdbc4)

<p>Right click the newly created _ADMINS organizational unit, go to new, then click User</p>

<h3>Step 16.</h3>

![16  create username](https://github.com/user-attachments/assets/075c16e1-31d2-4509-af98-60292213e110)

<p>Fill out the first, last, user logon name, then click Next. This will be our admin for the domain controller</p>

<h3>Step 17.</h3>

![17  set password](https://github.com/user-attachments/assets/d38d99c3-db18-4560-9f5d-eb44029a90ed)

<p>Set the password for the new User, check the boxes according to the image above, then click next. For the sake of the lab we don't want to expire or change the password.</p>

<h3>Step 18.</h3>

![18  click finish](https://github.com/user-attachments/assets/ddcde4f2-1981-4ae1-99d5-ab23798bb5b4)

<p>Click Finish</p>

<h3>Step 19.</h3>

![19  go to properties](https://github.com/user-attachments/assets/af0cfbac-12d5-4bba-b0fa-309cdfaaf9dc)

<p>Right click the newly created user and go to Properties</p>

<h3>Step 20.</h3>

![20  add jane to domain admins security group](https://github.com/user-attachments/assets/8ee03053-255b-416b-8bba-096e25c651cc)

<p>Click Member Of, click Add, type Domain Admins, click Check Names, click OK, then click Apply and OK. This will officially make this user an Admin of the domain.</p>

<h3>Step 21.</h3>

![21  login as jane admin](https://github.com/user-attachments/assets/055e9cbf-8902-4fe1-99e8-6ffe3ca965f2)

<p>Now login to the client VM</p>

<h3>Step 22.</h3>

![22  search system](https://github.com/user-attachments/assets/70f0a0fc-7130-4b69-a73a-eed96a24ae44)

<p>Once inside the client VM, search and click System in the Windows search bar</p>

<h3>Step 23.</h3>

![23  add client-1 to domain](https://github.com/user-attachments/assets/f3e9cfff-82a0-4d04-9a11-3f941973279a)

<p>Click "Rename this PC(advanced)", click Change, select Domain:, enter the name of the forest that was created, then click OK.</p>

<h3>Step 24.</h3>

![24  enter admin credentials](https://github.com/user-attachments/assets/12b25057-6137-4f4c-b586-60578dd201d6)

<p>Enter the admin credentials to officially join the client vm to the domain vm, then click OK</p>

<h3>Step 25.</h3>

![25  domain added success](https://github.com/user-attachments/assets/88c01a5b-00d5-4679-b65d-3950f38f5257)

<p>The client is now successfully apart of the domain</p>

<h3>Step 26.</h3>

![26  client-1 showing up in AD users   computers](https://github.com/user-attachments/assets/88331d3c-50c4-4637-8e87-7edd19ae06d2)

<p>Go back to the domain controller vm, go to Active Directory Users and Computers, under the domain name click Computers. The client vm should now show up as part of the domain.</p>

<h3>Step 27.</h3>

![27  create new org unit](https://github.com/user-attachments/assets/5377c858-9b14-472d-9405-8ef30cf10859)

<p>Right click the domain name and create a new Organizational Unit</p>

<h3>Step 28.</h3>

![28  name clients](https://github.com/user-attachments/assets/eb9a3745-8082-47bf-8c0b-32703cf3a9e0)

<p>Name this organizational unit _CLIENTS, then click OK</p>

<h3>Step 29.</h3>

![29  drag client-1 into clients OU](https://github.com/user-attachments/assets/d7609e02-488c-4c2f-bb79-ed4237a94f37)

<p>Drag the client vm into the _CLIENTS organizational unit</p>

<h2>Active Directory is Deployed!</h2>

<p>In this part, we have successfully installed Active Directory on the domain controller, created a domain admin, and joined the client VM to the domain. Next, we will create users in Powershell by running a script, and then manage the accounts and group policy!</p>





























