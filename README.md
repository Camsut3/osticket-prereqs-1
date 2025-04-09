<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

## 🧰 Tools Used

- Microsoft Azure (for hosting VM)
- Windows 10 (on the VM)
- IIS (Internet Information Services)
- PHP (via FastCGI)
- MySQL (Community Edition)
- osTicket (latest version)

---

## ✅ Prerequisites Checklist

1. **Azure Virtual Machine**
    - Windows 10 Pro
    - Inbound ports allowed: RDP (3389), HTTP (80)

2. **Remote Access**
    - Use Remote Desktop to connect to your VM after deployment.

3. **Install IIS**
    - Go to Control Panel → Programs → Turn Windows Features On or Off
    - Enable:
        - Internet Information Services
            - Web Management Tools
            - World Wide Web Services
                - Common HTTP Features
                - Application Development → CGI
                - Security → Request Filtering

4. **Install PHP**
    - Download from https://windows.php.net/download
    - Extract to `C:\PHP`
    - Add `C:\PHP` to System PATH
    - Configure in IIS:
        - Open IIS Manager → Handler Mappings → Add Module Mapping
            - Request Path: `*.php`
            - Module: `FastCgiModule`
            - Executable: `C:\PHP\php-cgi.exe`
            - Name: `PHP_via_FastCGI`

5. **Install MySQL**
    - Download from https://dev.mysql.com
    - Setup root password
    - Create database and user:

    ```sql
    CREATE DATABASE osticket;
    CREATE USER 'ostuser'@'localhost' IDENTIFIED BY 'yourpassword';
    GRANT ALL PRIVILEGES ON osticket.* TO 'ostuser'@'localhost';
    FLUSH PRIVILEGES;
    ```

6. **Download osTicket**
    - https://osticket.com/download
    - Extract to: `C:\inetpub\wwwroot\osTicket`
    - Rename: `include\ost-sampleconfig.php` → `ost-config.php`

7. **Set File Permissions**
    - Give `IIS_IUSRS` full control of:
        - `ost-config.php`
        - `include/`
        - `attachments/`
        - Root osTicket folder

8. **Run Installer**
    - Open browser in VM: `http://localhost/osTicket`
    - Follow web-based installer instructions

---

## 📌 Final Notes

- Delete the `/setup` directory after installation.
- Make `ost-config.php` read-only for security.
- Access osTicket from external IP: `http://<azure-public-ip>/osTicket`
