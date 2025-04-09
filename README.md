<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

Windows VM (Azure or local)
- Administrator access
- IIS installed and configured
- PHP (v8.0+)
- MySQL / MariaDB
- osTicket installer files

<h2>Installation Steps</h2>

1. **Create a Windows Virtual Machine** in Azure or locally.
2. **Install IIS** via Server Manager or Windows Features.
3. **Install PHP** from the [PHP website](https://windows.php.net/download/).
4. **Set up MySQL/MariaDB** and create a database for osTicket.
5. **Download osTicket** from the [official site](https://osticket.com/download/).
6. **Place osTicket files** in the IIS root directory (e.g., `C:\inetpub\wwwroot\osTicket`).
7. **Configure permissions** for the `include` and `upload` folders.
8. **Run the web installer** by navigating to `http://your-ip/osTicket` in your browser.
9. **Complete the installation** by entering your database info and creating the admin account.
10. **Delete the `setup` folder** after installation for security.
<p>
  


## 💾 Installation Prerequisites

Before installing osTicket, ensure the following are set up:

- ✅ Windows 10 VM in Azure  
- ✅ RDP access enabled  
- ✅ IIS installed with the following features:
  - CGI
  - ISAPI Extensions
  - ISAPI Filters
  - Common HTTP Features (Static Content, Default Document, etc.)
- ✅ PHP installed and added to system PATH  
- ✅ MySQL Server installed and running  
- ✅ osTicket zip file downloaded from [https://osticket.com/download](https://osticket.com/download)

---

## 🛠️ Installation Steps

### 1. Create and Connect to the VM

- Deploy a Windows 10 VM using the Azure portal
- Allow **RDP (port 3389)** and **HTTP (port 80)** through the Network Security Group
- Use **Remote Desktop Connection** to log in to the VM

### 2. Install IIS

Open **Control Panel → Programs and Features → Turn Windows features on or off**  
Check these features:
Internet Information Services └── Web Management Tools └── World Wide Web Services ├── Application Development Features → [✓] CGI ├── Common HTTP Features → [✓] Static Content, Default Document └── Security → [✓] Request Filtering




![windows features IIS](https://github.com/user-attachments/assets/7ba2564a-ddef-47a4-90c7-4b199cbd78f3)

### 3. Install PHP

- Download PHP 8.0+ for Windows from [https://windows.php.net/download/](https://windows.php.net/download/)
- Unzip to `C:\PHP`
- Add `C:\PHP` to the **System Environment Variable → PATH**
- Add PHP handler to IIS:
- Open IIS Manager → Handler Mappings → Add Module Mapping:
    ```
    Request Path: *.php
    Module: FastCgiModule
    Executable: C:\PHP\php-cgi.exe
    Name: PHP_via_FastCGI
    ```


![IIS php](https://github.com/user-attachments/assets/6c60bc1e-ecdb-4e0c-bd78-87cf85092d52)
---

### 4. Install MySQL

- Download and install MySQL Community Server
- During setup, create a new root password
- Log in using command line:
mysql -u root -p CREATE DATABASE osticket; CREATE USER 'ostuser'@'localhost' IDENTIFIED BY 'yourpassword'; GRANT ALL PRIVILEGES ON osticket.* TO 'ostuser'@'localhost'; FLUSH PRIVILEGES;






![qa1](https://github.com/user-attachments/assets/48a9e3e7-1085-4773-a5e2-ab446bfd6572)


![qa2](https://github.com/user-attachments/assets/d8e06eb1-501f-4bb5-afe4-c32d5a86d916)

---

### 5. Download and Extract osTicket

- Go to [https://osticket.com/download](https://osticket.com/download)
- Extract the contents to:
C:\inetpub\wwwroot\osTicket



- Rename the file:
C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php → ost-config.php



- Right-click the `include` and `ost-config.php` files → Properties → Uncheck "Read-only"
- Grant "IIS_IUSRS" Full Control permissions to the `osTicket` folder



![image](https://github.com/user-attachments/assets/e607b31a-11de-47bd-a7ac-8d2a01487803)
---

### 6. Run the Installer in Browser

- Open browser inside the VM and go to:
http://localhost/osTicket



- Complete the on-screen steps:
- Admin name and email
- Database name, username, and password (`osticket`, `ostuser`, etc.)



![image](https://github.com/user-attachments/assets/566d32ae-bbde-4922-9675-85b0909de739)
---

### 7. Post-Installation Cleanup

- Delete the `setup/` directory from `C:\inetpub\wwwroot\osTicket`
- Back up your `ost-config.php` file

---

## ✅ Final Notes

- To access osTicket externally, use the **public IP of your Azure VM**
http://<your-azure-vm-ip>/osTicket


- Secure MySQL with a strong root password and firewall rules.
- Keep PHP, MySQL, and osTicket updated regularly.



