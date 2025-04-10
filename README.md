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

# osTicket Prerequisites Installation Guide (Windows 10 + Azure VM)

This repo outlines the steps to prepare a Windows 10 (or Server) environment for hosting **osTicket** using **Microsoft Azure**, **MySQL**, **PHP**, and **IIS**.

---

## 💻 System Requirements

- Windows 10 Pro / Windows Server 2016+ (Azure VM supported)
- Administrative privileges
- Stable internet connection

---

## 📦 Software Stack Overview

- **IIS (Internet Information Services)** - Web server
- **PHP 8.x** - Server-side scripting language
- **MySQL 5.7+** - Database server
- **osTicket v1.17+** - Support ticket system

---

## 🛠️ Step 1: Install IIS

1. Open **Control Panel → Programs → Turn Windows features on or off**
2. Enable the following:
   - Internet Information Services
   - Web Management Tools
   - World Wide Web Services
   - CGI (under Application Development)
3. Click **OK** to install
4. Confirm IIS is running: open a browser and go to `http://localhost`

---

## 🐘 Step 2: Install PHP

1. Download PHP for Windows from [windows.php.net](https://windows.php.net/download/)
2. Extract it to `C:\PHP`
3. Configure PHP in IIS:
   - Open **IIS Manager**
   - Click your server name → **Handler Mappings** → Add Module Mapping:
     - Request path: `*.php`
     - Module: `FastCgiModule`
     - Executable: `C:\PHP\php-cgi.exe`
     - Name: PHP
   - Click **Request Restrictions** and check “Invoke handler only if request is mapped to:” → select “File”
   - Click OK
4. Add PHP to the system environment variable PATH

---

## 🐬 Step 3: Install MySQL

1. Download MySQL Community Server from [mysql.com](https://dev.mysql.com/downloads/installer/)
2. Run the installer and choose:
   - MySQL Server
   - MySQL Workbench (optional)
3. Set root password and configure port (default is 3306)

---

## ⚙️ Step 4: Configure MySQL Database for osTicket

1. Open MySQL Command Line or Workbench
2. Run the following commands:
   ```sql
   CREATE DATABASE osticket;
   CREATE USER 'osticket_user'@'localhost' IDENTIFIED BY 'YourPassword123';
   GRANT ALL PRIVILEGES ON osticket.* TO 'osticket_user'@'localhost';
   FLUSH PRIVILEGES;
   ```

---

## ⬇️ Step 5: Download and Prepare osTicket

1. Download osTicket from [osTicket.com](https://osticket.com/download/)
2. Extract to `C:\inetpub\wwwroot\upload`
3. Rename `ost-sampleconfig.php` to `ost-config.php`
4. Ensure the following have write permissions:
   - `include/ost-config.php`
   - `attachments/`
   - `logs/`

---

## 🔁 Step 6: Restart IIS

1. Open Command Prompt as Admin:
   ```bash
   iisreset
   ```
2. Navigate to `http://localhost/upload` to begin osTicket web installer

---

## ✅ Summary

By the end of this process, your environment should be ready to install and configure osTicket:

- IIS + PHP configured
- MySQL database and user set up
- osTicket files in the correct directory
- Permissions granted
