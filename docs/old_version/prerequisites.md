# Setup and Run the Old Version of the Calculation Tools

To set up and run the old version of the Calculation Tools, ensure that your environment is properly configured with the following software and tools:

Works for Linux, Windows, Mac

## 1. Node.js and Gulp

### Install NVM (Node Version Manager)

Node Version Manager (NVM) allows you to install and manage multiple versions of Node.js on your system. This is particularly useful for this project as it requires Node.js version 10.24.0.

1. **Install NVM**:

   * Follow the installation instructions for NVM specific to your operating system:

     * **Windows**: Download and install from the [NVM for Windows GitHub repository](https://github.com/coreybutler/nvm-windows).
     * **macOS/Linux**: Install using the following command in your terminal:

     ```
     curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh |  
     ```
2. **Install Node.js version 10 using NVM**:

   * Once NVM is installed, use it to install Node.js version 10.24.0:

     ```
     nvm install 10.24.0
     ```
3. **Verify available Node.js versions**:

   * List all installed versions of Node.js using:

     ```
     nvm list
     ```
4. **Switch to Node.js version 10**:

   * Set Node.js version 10.24.0 as the active version:

     ```
     nvm use 10
     ```
5. **Confirm the active Node.js version**:

   * Verify that Node.js version 10.24.0 is active:

     ```
     node -v
     ```
   * Ensure the output shows `v10.24.0`.
6. **Install Gulp**:

   * Gulp is required for automating tasks and managing workflows. Install it:

     ```
     npm install --global gulp-cli@2.3.0
     npm install gulp@4.0.2 --save-dev
     ```

## 2. Python

### Python Version: 2.7

For this project, Python 2.7 is required. Ensure that it is installed and configured on your system.

1. **Install Python 2.7**:

   * Download and install Python 2.7 from the [Python Releases for Windows](https://www.python.org/downloads/release/python-2718/) page.
   * On macOS/Linux, use your package manager:

     ```
     sudo apt-get install python2.7
     ```
   * Verify the installation:

     ```
     python --version
     ```
   * Ensure the output shows `Python 2.7.x`.

## 3. PHP

### PHP Version: 7.3 and Above

PHP is required for various backend functionalities in the old version of the tools. Ensure you have PHP version 7.3 or higher installed.

1. **Install PHP**:

   * Download and install PHP from the [official PHP website](https://www.php.net/downloads).
   * Alternatively, use a package manager:**( Reccomended Approach )**

     * **Windows**: Use a WAMP or XAMPP stack that includes PHP 7.3 or above.
     * **macOS/Linux**: Use Homebrew (macOS) or apt-get (Linux):

     ```
     brew install php@7.3
     ```
     ```
     sudo apt-get install php7.3
     ```
2. **Verify PHP Installation**:

   * Confirm the PHP version:

     ```
     php -v
     ```
   * Ensure the output shows `PHP 7.3.x` or higher.
