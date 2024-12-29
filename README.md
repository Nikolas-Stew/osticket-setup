<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket through a fresh environment.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure VM
- IIS
- PHP Manager
- Rewrite Module
- VC Redist
- MySQL
- Heidi SQL
- osTicket


<h2>Installation Steps</h2>


1.) The first thing you are going to want to do is create a virtual machine by going to the Azure webpage. Setup your virtual machine with `Windows 10 Pro, Version 22H2`. Ensure you set up a username and password you will remember for the lab and check the option to show you have an eligible Windows key. 
>Note, you will want to create a virtual machine with atleast 2 or 4 vcpus and 16 GB's of memory to not cause any lag / buffering during the lab.

2.) Once the machine is created wait for it to be fully up and running. Once it shows running you can open it and grab the public IP, copy that and open `Remote Desktop Connection` app and paste that IP into there. 
</p>
<br />

<p>
<img src="https://i.imgur.com/B6RSGQE.png" height="80%" width="80%" alt="VM Setup"/>
</p>
<p>
<p>
<img src="https://i.imgur.com/mBTKfxo.png" height="60%" width="60%" alt="VM Connection"/>
</p>
<p>
  
>When the login page comes up make sure you hit more choices and change the username, sometimes it can use your windows username to try and sign into the VM but it won't work.

3.) Once you have connected to your virtual machine you will want to go to your control panel. From the control panel open up programs. Select, Turn Windows features on and off. From here navigate to `Internet Information Services` then `World Wide Web Services`. First you will want to check `Common HTTP Features` then navigate to `Application Development Features` and check the box for `CGI` then hit ok.

<p>
<img src="https://i.imgur.com/8hTk6Ts.png" height="100%" width="100%" alt="IIS Installation"/>
</p>
<p>
  
>Make sure all Common HTTP Features are checked. To ensure IIS was installed properly navigate to your browser and enter 127.0.0.1 and you should get a result as below.
 
 To make sure IIS is installed / enabled go to a browser of your choice and search for 127.0.0.1 
  It should look something like this. 
  
<p>
<img src="https://i.imgur.com/XOmVwwL.png" height="80%" width="80%" alt="127.0.0.1 Check"/>
</p>
<p>
  
>Downloads sourced from https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD

4.) Now that the IIS is on, you will be able to start your next downloads. First with PHP you can install `PHPManagerForIIS_V1.5.0`. 
  
5.) Next from the Installation Files, download and install the Rewrite Module `rewrite_amd64_en-US.msi`. Afterwards creating a folder in the C drive called PHP.
  
6.) From the Installation Files, open `php-7.3.88-nts-Win32-VC15-x866.zip` and unzip the contents into `C:\PHP`.

7.) Once you have downloaded and extracted the zip file into the PHP folder on the C drive, download and install the `VC_redist.x86.exe` from the installation files and follow the steps given by the install wizard.  
  
8.) Download and install MySQL file `mysql-5.5.62-win32.msi`. Select the following options: `Typical`, Check the option `Launch instance configuration` and finally check `Standard Configuration`. Typically here you would set what you want as your root password, for this instance we will use "Password1".

9.) Once entered hit `Next` then hit `Execute` to create the config files and SQL installation.
 
10.) Now that we have the files downloaded and installed we will want to search for IIS in the windows search bar. Open IIS as an administrator. and select into `PHP Manager` then click `Register new PHP version`.
  
<p>
<img src="https://i.imgur.com/Fw9KUfA.png" height="80%" width="80%" alt="ISS PHP Manager"/>
</p>
<p>
  
>You need to provide a path to `php-cgi`, hit the 3 dots, then naviage C: > PHP > php-cgi and hit open. Hit ok, navigate back to the osticket-Setup and hit restart on the right side
  
11.) Direct back to the osTicket-Installation file and extract `osTicket-v1.15.8` into C:\inetpub\wwwroot . Afterwards going and renaming the `upload` file to `osTicket`. Once done restart inside of IIS again.
  
12.) inside IIS go to sites > Default > osTicket then on the right side click `Browse *:80 (http)`.
  
<p>
<img src="https://i.imgur.com/FczmovD.png" height="100%" width="100%" alt="osTicket Setup"/>
</p>
<p>
  
  You will notice some extensions are disabled. To remedy this go back to ISS > Sites > Default > osTicket, open `PHP Manager` and click `Enable or disable an extension`. From here we want to eanble 3 extension being `php_imap.dll`, `php_intl.dll` and `php_opcache.dll` by finding, clicking them and hitting enable on the top right
  
13.) Once we have those extensions enabled in IIS, we are going to want to rename one of the files in our osTicket folder. Go into the file explorer and search for C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php, we are going to rename this file to `ost-config.php`. We will then right click on this and hit properties, navigate to security and click on advanced and disable the inheritance.
  
<p>
<img src="https://i.imgur.com/uGvi4Mm.png" height="100%" width="100%" alt="Perm Setup"/>
</p>
<p>
  
  Afterwards we are going to add new permissions, so hit `Add` then at the top `Select a principal`, in the box type `Everyone` and hit ok. Make sure to set `Full Control` perms to everyone. Click `Apply` and `OK`

  Next open back up osTicket in your browser and hit continue, fill out all the information until you reach `Database settings` and proceed to install HeidiSQL from installation files by opening `HeidiSQL_12.3.0.6589_Setup`.

  Once it Opens hit New and fill in the username and password and hit `Open`.
  
<p>
<img src="https://i.imgur.com/A8XJe8E.png" height="90%" width="90%" alt="HeidiSQL"/>
</p>
<p>
  
>Make sure username is root and password is Password1.

  Iside of Heidi we will want to right click `Unnamed` then select `Create new` then `Database`, naming that database `osTicket`. Afterwards navigate into your browser and fill out Username as `root`, Password as `Password1` and MySQL Database as `osTicket`. Afterwards click `Install Now`.
  
<p>
<img src="https://i.imgur.com/770zQCu.png" height="100%" width="100%" alt="Database Creation"/>
</p>
<p>
  
  Since were through the process we want to do a little cleanup, First we will delete the folder C:\inetpub\wwwroot\osTicket\setup, then we will want to set permisisons back to `Read` only in the `ost-config.php` file inside of C:\inetpub\wwwroot\osTicket\include. Final step we will complete will be to login to osTicket inside your browser.
  
<p>
<img src="https://i.imgur.com/QyuZlQL.png" height="80%" width="80%" alt="osTicket Login"/>
</p>
<p>
  
  You have completed the setup and should be able to log in to osTicket now!
