<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This demonstration outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: Initial osTicket Installation](https://youtu.be/078a7mSwRk4)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Overview of Process</h2>

- Create a VM in Azure and Connect Through Remote Desktop
- Enable IIS
- Install Visual C++ Redistributable
- Install IIS URL Rewrite Module
- Install PHP Manager
- Install SQL server (MySQL) + SQL UI (HeidiSQL)
- Install osTicket Files
- Add osTicket Extensions
- Setup osTicket Helpdesk and Connect it to MySQL

<h2>Installation Steps</h2>

<p>
<img src="https://github.com/user-attachments/assets/e2464cf9-1e3a-415f-8aba-ea8d9d6acadf" height="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
We will start by creating a Windows 10 OS virtual machine in Microsoft Azure, creating a Resource Group along with it to store the VM. For the size, I chose to use 4vcpu, 16GiB memory system, but any of the "Recommended by image publisher" options should work. Make an admin username and password, check the licensing box, then Review + Create. After the VM is created, copy its public IP address and paste it into your Remote Desktop application, logging in with the previously created admin username and password,
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/e21d1193-6e8a-498a-a270-d83e4dca4da8" height="25%" alt="Disk Sanitization Steps"/>
</p>
<p>
The first thing to do within the VM is to enable IIS (Internet Information Services), as well as CGI on the device. IIS will allow us to host osTicket locally to the device, and CGI allows us to run PHP scripts that are necessary for osTicket. This can be done by searching the Windows menu for "Turn Windows Features On or Off," then navigating to Internet Information Services, checking the box, then expanding it, then locating and checking CGI under World Wide Web Services.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/11dea6bf-2de4-404c-9243-6428d65a7b6f" height="30%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/user-attachments/assets/d8d6395e-c711-4abd-9f50-400c39efa295" height="30%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we need to install Visual C++ Redistributable and IIS URL Rewrite Module. These are 2 things we need on the device to make everything work together.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/7799c676-cfe9-4317-9280-fcf7fb581f39" height="25%" alt="Disk Sanitization Steps"/>
</p>
<p>
We will need to install PHP for Windows in order to be able to configure PHP Extensions for osTicket later. To do this, create a new directory in Windows(C:) named "PHP" and extract the zipped folder with the PHP installation files to it. This can be found at https://www.php.net/downloads. After that, we register the PHP version within the PHP Manager in IIS Manager by navigating to php-cgi.exe.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/90f4c732-b754-41a4-b13b-24bd9117ff57" width="49%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/user-attachments/assets/70ba7f90-c76b-4294-b24b-35e0c9192be5" width="49%" alt="Disk Sanitization Steps"/>
</p>
<p>
Before installing osTicket, it is best to already have an SQL server and UI installed. We'll be using MySQL as the server and HeidiSQL as the UI. When installing MySQL, I am using username and password "root". Inside of HeidiSQL, create a new database and name it osTicket.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/0e3dca5a-23d9-470e-ad96-824b14ff2ea0" height="25%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/user-attachments/assets/9819572f-ff3d-4d67-a8da-b90923512a05" height="25%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we are installing osTicket. To do this, open C: > inetput > wwwroot, then in your osTicket installation file zip folder, drag the "upload" folder into wwwroot. Rename "upload" to "osTicket". From this osTicket folder navigate to the "include" folder and rename "ost-sampleconfig.php" to "ost-config.php." At this point we can go into IIS Manager, stop and start the server to refresh it, then navigate to Sites > Default Web Site > osTicket, click Browse on the right hand side and it will open up osTicket in the browser.
</p>
<br />

![image](https://github.com/user-attachments/assets/481bddc2-6592-494c-8aa7-4ab0a44ee587)
<p>
To set up some recommended extensions for osTicket, open up PHP Manager within IIS Manager, select Enable or disable an extension under PHP Extensions, and enable, php_imap.dll, php_intl.dll, and php_opcache.dll, then refresh the browser and click continue on osTicket.
</p>
<br />

<img src="https://github.com/user-attachments/assets/fd4d5915-1437-419d-9a8e-c3cc5d113658" width="50%"/>
<p>
  Finally, fill in the info for your Helpdesk, as well as the Admin user. Make sure your Helpdesk email and Admin User email are different, then under Database Settings enter the information for the Database you created (it should be named osTicket).
</p>
<br />
