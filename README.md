<p align="center">
  
![1-1](https://github.com/user-attachments/assets/899a9de9-9453-47f4-bc7c-5f0f4a96e312)

</p>

<h1>Creating Users, Group Policy, and Managing Accounts with Active Directory in Azure</h1>
<h2>Description</h2>
This project will demonstrate how to configure Remote Desktop access for non-administrative users, automate user creation with PowerShell, and manage group policies. Additionally, we'll cover account lockouts to simulate a real-life IT environment.<br/>
<br/>
This project is a continuation of <a href="https://github.com/MindofLindstrom01/deploying-active-directory-in-azure">Active Directory: Deploying Active Directory in Azure<a/><br/>

<br/>

You can find the Powershell script used in this project <a href="https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1">here

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

![1  login to client-1 as admin](https://github.com/user-attachments/assets/dce43e84-01a0-453b-ac97-9c29b6cc490a)

<p>Login to the client vm using the admin credentials</p>

<h3>Step 2.</h3>

![2  go to system settings](https://github.com/user-attachments/assets/69800ab1-e7fc-4099-a631-61b27a04964f)

<p>Once inside the client vm, search for System and click it</p>

<h3>Step 3.</h3>

![3  click remote desktop](https://github.com/user-attachments/assets/0aef4a2b-33ee-404d-b6ab-ef076fc48c05)

<p>Click Remote Dekstop</p>

<h3>Step 4.</h3>

![4  click select users to access](https://github.com/user-attachments/assets/42894204-a726-42ae-9d41-ae4e779d8159)

<p>Click "Select users that can remotely access this PC", then click Add</p>

<h3>Step 5.</h3>

![5  allow all domain users to login to client-1](https://github.com/user-attachments/assets/e38de5dd-f518-48fc-bbbf-abea69418982)

<p>Type in "Domain Users", click Check Names, then click OK. This will allow all domain users to be able to access the client via Remote Desktop.</p>

<h3>Step 6.</h3>

![6  open powershell ise](https://github.com/user-attachments/assets/f9560793-667e-479d-bdf1-f9d58590f617)

<p>Now login to the domain controller as an admin, search for Windows Powershell ISE in the Windows search bar, then click run as administrator</p>

<h3>Step 7.</h3>

![7  create a new script file](https://github.com/user-attachments/assets/aa83fe66-4518-4f34-877e-f33403de690c)

<p>Click the file icon in the top left to start the creation of a new .ps1(Powershell) script file</p>

<h3>Step 8.</h3>

![8  save the script](https://github.com/user-attachments/assets/7c2f5c15-a648-4824-8f49-e6182062dbf1)

<p>Press CTRL+S to save the script in your desktop</p>

<h3>Step 9.</h3>

![9  paste the powershell script](https://github.com/user-attachments/assets/814f8a80-d1ff-4ddd-bd80-1be98dbd3688)

<p>Paste the Powershell script inside the file</p>

<h3>Step 10.</h3>

![10  run the script](https://github.com/user-attachments/assets/e22e9e10-68c9-47ed-906b-d829290c59df)

<p>Now run the script by clicking the green play button. This will generate 10000 randomly generated users each with the same password of "Password1" and add them to the _EMPLOYEES organizational unit created previously.</p>

<h3>Step 11.</h3>

![11  pick one randomly created user](https://github.com/user-attachments/assets/22d9ad64-19b1-4334-b429-979c242bf4df)

<p>Go back to the domain controller vm and pick one randomly created user within the _EMPLOYEES organizational unit inside ADUC</p>

<h3>Step 12.</h3>

![12  login to client-1 as your chosen user](https://github.com/user-attachments/assets/46a967ba-4659-49a3-b0c9-42dcc7e4b97d)

<p>Now attempt to login to the client vm as the randomly created user with the domain name followed by the appropriate username and a password of "Password1"</p>

<h3>Step 13.</h3>

![13  domain user login success](https://github.com/user-attachments/assets/c2dc8e52-74c5-4295-96b4-e71884ebcf43)

<p>Once inside, we can open command prompt to verify that we are successfully logged in as the chosen user</p>

<h3>Step 14.</h3>

![1  right click select run](https://github.com/user-attachments/assets/305bca9f-328b-4f38-9086-3e793e508198)

<p>Go back to the domain controller vm, right click the Windows icon, and click Run</p>

<h3>Step 15.</h3>

![2  type gpmc msc](https://github.com/user-attachments/assets/02b1423f-e961-41cc-8e5c-fb50acd16079)

<p>Type "gpmc.msc", then click OK. This will open Group Policy Management</p>

<h3>Step 16.</h3>

![3  edit default domain policy](https://github.com/user-attachments/assets/64e7bc4e-7b57-41aa-9dc6-9c5b004ec6c3)

<p>Go to Forest:, Domains, the domain name, right click Default Domain Policy, then click Edit</p>

<h3>Step 17.</h3>

![4  go to account lockout policy](https://github.com/user-attachments/assets/5b712d8d-3adc-4b09-887b-881ca8975915)

<p>Go to Computer Configuration, Policies, Windows Settings, Security Settings, Account Policies, click Account Lockout Policy, then click Account lockout duration</p>

<h3>Step 18.</h3>

![5  set the lockout duration for 30 minutes](https://github.com/user-attachments/assets/73097983-46b3-45ed-a85a-38406e6f70c9)

<p>Check the box, set the account lockout duration to 30 minutes, then click Apply and OK</p>

<h3>Step 19.</h3>

![6  other policies automatically changed](https://github.com/user-attachments/assets/3e2d8433-d316-4637-a293-b6fb0fddb281)

<p>This will automatically configure the other lockout policy settings. We are doing this so we can purposefully lock out a domain user account later</p>

<h3>Step 20.</h3>

![7  gpupdate force command as jane admin](https://github.com/user-attachments/assets/fe3c35f7-a92c-4d10-9cdc-3caf701f45e0)

<p>This policy change will take some time to apply. Instead of waiting, log back into the client vm as an admin, open command prompt, and run the "gpupdate /force" command to instantly update the group policy</p>

<h3>Step 21.</h3>

![8  policy successfully updated](https://github.com/user-attachments/assets/e13a1b5d-bd8e-4997-964d-887329b4679d)

<p>The policy has now been updated.</p>

<h3>Step 22.</h3>

![9  grab a random domain user](https://github.com/user-attachments/assets/fed0f48d-8840-4b26-874b-20d2655aca68)

<p>Once again, grab a random domain user within the _EMPLOYEES organizational unit within ADUC from the domain controller vm</p>

<h3>Step 23.</h3>

![10  enter a bad password 6 times for client-1](https://github.com/user-attachments/assets/68c27b51-e6a2-4015-b1e4-1227948cdc1d)

<p>Now attempt to login 6 times into the client vm with that user and the wrong password</p>

<h3>Step 24.</h3>

![11  locked out](https://github.com/user-attachments/assets/9e3fe228-1cb5-4c99-9afa-ac6f5ac4bbee)

<p>This will result in a security message indicating that the domain users account has been locked out</p>

<h3>Step 25.</h3>

![12  unlock the account](https://github.com/user-attachments/assets/b96b4676-2dcf-4d53-9ac6-eaa2be124426)

<p>Now go back to the domain controller vm inside ADUC and click on the user's account that has been locked out. Click Account, check the unlock account box, then click Apply and OK. This will unlock the domain user's account</p>

<h3>Step 26.</h3>

![13  attempt to login again](https://github.com/user-attachments/assets/de45d5cf-2c2a-402f-b433-a6e9f5ad6bc2)

<p>Now attempt to login to the client vm with the domain user's account using the correct password</p>

<h3>Step 27.</h3>

![14  login success](https://github.com/user-attachments/assets/2edb1ccf-ca30-48ea-afd4-5c6fc543cf06)

<p>You should now be able to successfully login as the account has been unlocked</p>

<h3>Step 28.</h3>

![15  right click   disable account](https://github.com/user-attachments/assets/75ca692e-3432-4df3-8e57-19e76be74771)

<p>Go back to the domain controller vm inside ADUC, right click the domain user, and click disable account. This will disable the domain user's account.</p>

<h3>Step 29.</h3>

![16  disabled](https://github.com/user-attachments/assets/5a394f1f-5120-4aeb-a185-24d73316b5a5)

<p>The domain user's account is now disabled</p>

<h3>Step 30.</h3>

![17  attempt to login to bah dew](https://github.com/user-attachments/assets/e4cb0198-826e-4fa1-b5d8-d152f8b636d7)

<p>Now attempt to login to the client vm as the domain user again</p>

<h3>Step 31.</h3>

![18  login fail account is disabled](https://github.com/user-attachments/assets/33882ea3-f584-4dbb-ac4c-512b878da3de)

<p>This should result in a message saying the user account is currently disabled.</p>

<h3>Step 32.</h3>

![19  enable the account](https://github.com/user-attachments/assets/3bf041e4-c9a4-4dd0-8fac-48151e456706)

<p>Go back to the domain controller vm insude ADUC, find and right click the user with the disabled account, then click Enable Account.</p>

<h3>Step 33.</h3>

![20  enabled](https://github.com/user-attachments/assets/f10e9edf-e7a1-4109-afc8-aa5415c3a675)

<p>The domain user's account is now enabled</p>

<h3>Step 34.</h3>

![21  attempt to login](https://github.com/user-attachments/assets/768e9c24-69f7-47c8-b415-fc9ad8ade999)

<p>Now attempt to login to the client vm with the domain user's credentials</p>

<h3>Step 35.</h3>

![22  login success](https://github.com/user-attachments/assets/c031b240-62a7-46a0-85b2-99f108b781fe)

<p>You should now successfully login as the user as the account has been re-enabled</p>

<h2>Active Directory: Creating Users, Group Policy, and Managing Accounts in Azure is Now Complete</h2>

<p>In this part, we've successfully configured Remote Desktop for non-administrative users, automated user creation with PowerShell, and managed group policies. Additionally, we covered account lockouts to simulate a real-life IT environment!</p>





























