This document outlines the key folders and files in the Calculation Tools project, detailing their purposes and suggesting areas for improvement.

---

## 1. **Key Folders in the `App` Directory**

The main project files are located in the `App` folder, which is organized into various subfolders based on functionality.


![1726563317857](image/overview/1726563317857.png)

### 1.1 **About Folder**

* **Purpose** : Contains all the pages related to the “About” section of the project, such as the “About Us” information.
* **Modification Point** : This is where any informational changes or updates to the "About Us" page can be made.

### 1.2 **Account Folder**

* **Purpose** : Contains files for handling account-related functionalities, including:
* **Signup**
* **Login**
* **Modification Point** : You can modify or update the user authentication logic here.

### 1.3 **Admin Folder**

* **Purpose** : Contains files related to admin functionalities.
* **Current Limitation** : These files are not currently accessible via browser links.
* **Modification Point** : If admin pages need to be made accessible or enabled, you can update the routing or security access controls here.

### 1.4 **Blueprint Wizard Folder**

* **Purpose** : Contains the multistep wizards for different projects. Here, you can modify steps or adjust formulas for each project.
* **Global Wizard** : Used for handling global blueprint steps.
* **School Wizard** : Specifically used for multistep wizards related to school projects.
* **Country Wizard** : Used for blueprint steps related to country-based projects.
* **Modification Point** : Customize the steps and logic used within the wizard based on new requirements or data.

### 1.5 **Multischool Wizard Folder**

* **Purpose** : Specifically contains the multistep wizard functionality for school-related projects.
* **Modification Point** : This is where you can modify the school's wizard steps if new steps or conditions need to be added.

### 1.6 **Feedback Folder**

* **Purpose** : Designed to collect client/user feedback.
* **Current Limitation** : Not functional.
* **Modification Point** : This section can be activated to collect user feedback, potentially improving the user experience.

---

## 2. **Backend Files (Server Directory)**

The backend of the project is powered by **PHP** and located in the `server` directory. These files manage the application's core functionalities, including API routing, database interactions, and server-side logic.


**Connection file logic**

![1726563343322](image/overview/1726563343322.png)


**Calculations logic folder**

![1726563397464](image/overview/1726563397464.png)

* **Key Points** :
* **Slim Framework** is used for routing and handling API requests.
* **PHP scripts** manage various backend operations like handling form submissions, database queries, and more.

## 3. **Frontend Structure**

The frontend is Angular-based, and the core functionalities are distributed across multiple folders.

### 3.1 **About Folder**

* **Purpose** : Contains pages related to the "About Us" section of the application.

### 3.2 **Admin Folder**

* **Purpose** : Contains pages related to administrative functions that the admin can manage.

### 3.3 **Blueprint Wizard Folder**

* **Purpose** : Contains forms for handling wizards such as:
* **Global Wizard**
* **School Wizard**
* **Country Wizard**
* **Modification Point** : Changes to the form fields or logic can be applied here to adapt to new blueprint formats or client needs.

### 3.4 **Dashboard Folder**

* **Purpose** : Contains pages for normal users after they log in, including their personalized dashboard.

### 3.5 **Main Folder**

* **Purpose** : Controls the main home page and navigation logic.
* **Key Functionality** : This folder dictates which views users will see based on their access level. By default, the global blueprint is loaded.
* **Modification Point** : The main folder could be restructured to allow for more flexible switching between wizards (school, country, global) without redirecting to different subdomains.

---

## 4. **Improvement Suggestions**

### 4.1 **Frontend Folder Structure**

Currently, the frontend has separate wizards for schools, countries, and global blueprints. To enhance usability, this structure should be improved so that users can switch between school and country wizards without navigating to separate subdomains.

 **Suggestion** :

* **Unify Wizards** : Combine the school and country wizards into a single wizard interface that allows users to switch between them within the same platform. This will streamline the user experience and make it easier to navigate between different blueprint types.

### 4.2 **Backend Improvement**

The current backend uses the  **PHP Slim Framework** , which is lightweight but lacks some features for larger, more complex applications.

 **Suggestion** :

* **Migrate to Laravel** : Laravel provides more advanced features, such as built-in authentication, routing, and database management. Migrating to Laravel will improve scalability, security, and ease of development.
