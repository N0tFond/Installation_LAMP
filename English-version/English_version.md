# LAMP Server Installation 🚀

[![fr](https://img.shields.io/badge/Lang-Français-blue.svg)](../README.md)

## Prerequisites

> ⚠️ **Important**: This documentation is intended for Linux or WSL Linux systems only.

## Table of Contents

- [System Update](#system-update)
- [Apache 2 Installation](#apache-2-installation)
- [Database Installation](#database-installation)
- [PHP Installation](#php-installation)
- [Notes](#notes)

## System Update

Before starting, update your system:

```bash
sudo apt update && sudo apt upgrade -y
```

## Apache 2 Installation

1. Install packages:

```bash
sudo apt install -y apache2 apache2-utils
```

2. Check status:

```bash
sudo systemctl status apache2.service
```

Expected result:
![Apache2 Status](./imgs/command_output_apache2.png)

> 💡 If you have a graphical interface, open `localhost` in your browser:
>
> ![Localhost page](./imgs/localhost_output.png)

## Database Installation

### Option 1: MariaDB

```bash
sudo apt install -y mariadb-server mariadb-client
```

#### Securing MariaDB

1. Launch the security script:

```bash
sudo mysql_secure_installation
```

2. Follow these steps:
   - Press Enter for root password (empty by default)
   - Type 'Y' to set a root password
   - Enter and confirm your new password
   - Answer 'Y' to the following questions:
     - Remove anonymous users? (Y)
     - Disallow root login remotely? (Y)
     - Remove test database? (Y)
     - Reload privilege tables? (Y)

Expected output:

```bash
Securing the MySQL server deployment.

Enter password for user root:
New password:
Re-enter new password:

Remove anonymous users? [Y/n] Y
Disallow root login remotely? [Y/n] Y
Remove test database and access to it? [Y/n] Y
Reload privilege tables now? [Y/n] Y

All done!
```

> 📝 For detailed MariaDB configuration, see [MariaDB_Config.md](./MariaDB_Config.md)

### Option 2: MySQL

```bash
sudo apt install -y mysql-server
```

#### Securing MySQL

1. Launch the security script:

```bash
sudo mysql_secure_installation
```

2. Follow the configuration steps:
   - Configure the password validation plugin
     - Choose complexity level (0 = LOW, 2 = STRONG)
   - Set a root password
   - Answer 'Y' to the following questions:
     - Remove anonymous users? (Y)
     - Disallow root login remotely? (Y)
     - Remove test database? (Y)
     - Reload privilege tables? (Y)

Expected output:

```bash
Securing the MySQL installation.

Validating password strength for root user.
Press y|Y for Yes, any other key for No: Y

Choose the level of password validation policy:
0 = LOW    Length >= 8
1 = MEDIUM Length >= 8, numeric, mixed case, and special characters
2 = STRONG Length >= 8, numeric, mixed case, special characters and dictionary
Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1

Remove anonymous users? [Y/n] Y
Disallow root login remotely? [Y/n] Y
Remove test database and access to it? [Y/n] Y
Reload privilege tables now? [Y/n] Y

All done!
```

> 📝 For detailed MySQL configuration, check the [MySQL Documentation](https://dev.mysql.com/doc/)

## PHP Installation

1. Install PHP packages:

```bash
sudo apt install php libapache2-mod-php php-mysql
```

2. Configure permissions:

```bash
sudo chown $USER /var/www/html/*
```

### Installation Verification

#### Via Terminal

```bash
php -v  # Should display PHP 8.2.26
```

![PHP Version](./imgs/php_cmd_output.png)

#### Via Apache

1. Access the web directory:

```bash
cd /var/www/html
```

2. Remove default index:

```bash
sudo rm index.html
```

3. Create an `index.php` file with the following content:

```php
<?php phpinfo(); ?>
```

Expected result:
![PHPInfo](./imgs/phpinfo_output.png)

## Notes

> ⚠️ **Warning**: This configuration is intended for local development or closed network environments.
> Do not use in production without additional security configuration.

---

💡 **Tip**: For more detailed configuration, check the official documentation of each component:

- [Apache Documentation](https://httpd.apache.org/docs/)
- [PHP Documentation](https://www.php.net/docs.php)
- [MariaDB Documentation](https://mariadb.org/documentation/)

---

_If you find this guide useful, feel free to share it!_ ⭐
