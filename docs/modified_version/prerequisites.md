# Modified Calculation Tools Prerequisites

The modified version of the Calculation Tools introduces updated frameworks and tools to ensure better performance, security, and compatibility. Please make sure your environment is configured with the following software and tools:

Works for Windows, mac, and Linux


# Node.js Setup

## Node.js Version: 20.x or Higher

For this project, **Node.js version 20 or higher** is required. The latest **LTS version** is recommended.

## Steps:

1. **Install NVM (Node Version Manager)**
   - Download and follow the guide from the [NVM GitHub page](https://github.com/coreybutler/nvm-windows).

2. **Install Node.js version 20 using NVM**
   - Use NVM to install Node.js version 20.x:
     ```
     nvm install 20
     ```

3. **Verify Installed Node.js Versions**
   - List all installed Node.js versions:
     ```
     nvm list
     ```

4. **Switch to Node.js Version 20**
   - Set Node.js version 20.x as the active version:
     ```
     nvm use 20
     ```

5. **Confirm Active Node.js Version**
   - Verify that Node.js version 20.x is active:
     ```
     node -v
     ```
   - Ensure the output shows `v20.x.x`.

6. **Install Gulp**
   - Gulp is required for task automation. Install it using:
     ```
     npm install --global gulp-cli@2.3.0
     npm install gulp@4.0.2 --save-dev

## 2. Python

### Python Version: 3.x or Higher

The modified version requires Python 3.x for better performance and support of modern libraries.

1. **Install Python 3.x** :

   * Download and install the latest version of Python 3.x from the [Python official website](https://www.python.org/downloads/).
   * On macOS/Linux, use your package manager:

   ```
   sudo apt-get install python3
   ```
2. **Verify the installation**:

   * Confirm the installation:

   ```
   python3 --version
   ```

   * Ensure the output shows `Python 3.x.x`.

## 3. PHP

### PHP Version: (Supports 7.4 +)

For optimal performance and compatibility, PHP version 7.4+ is recommended.

1. **Install PHP 7.4** :

   * Download and install PHP 7.4 from the [official PHP website](https://www.php.net/downloads).
   * Alternatively, use a package manager: **(RECOMMENDED APPROACH)**
     * XAMPP (Windows, macOS, Linux) or stack that includes PHP 7.4 or above.
     * [XAMPP FOR WINDOWS DOWNLOAD LINK](https://sourceforge.net/projects/xampp/files/XAMPP%20Windows/7.4.33/)
     * [XAMPP FOR LINUX DOWNLOAD LINK](https://sourceforge.net/projects/xampp/files/XAMPP%20Linux/7.4.30/)
     * [XAMPP FOR MacOS DOWNLOAD LINK](https://sourceforge.net/projects/xampp/files/XAMPP%20Mac%20OS%20X/7.4.33/)

   ##### **THATS IT :)** 

If you download xampp from the links shared above and install it , you get the following setup

> **php 7.4 , Apache, mysql** 

This setup allows you to run php and also upload the database. 


---

---



### Additional Tools ( If you had php already installed n your platform )

4. **Using PHP Version Switcher (Windows only)**:  

   * Open PowerShell and install Scoop:

   ```
   irm get.scoop.sh | iex
   # You can use proxies if you have network trouble accessing GitHub, e.g.
   irm get.scoop.sh -Proxy 'http://<ip:port>' | iex
   ```
   * Confirm if Scoop is installed:

   ```
   scoop --version
   ```
   * Install PHP 7.4 using Scoop:

   ```
   scoop bucket add versions
   scoop install versions/php74
   ```
   * To switch between PHP versions:

   ```
   scoop list
   scoop switch php74
   ```
5. **Verify PHP Installation** :

   * Confirm the PHP version:

   ```
   php -v
   ```
   * Ensure the output shows PHP 7.4+.
