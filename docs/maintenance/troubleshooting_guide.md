
# Calculation Tools Troubleshooting Guide

This guide provides steps for troubleshooting both the frontend and backend of the Calculation Tools project.

---

## **Frontend Troubleshooting (Client Folder)**

The frontend is based on **Angular v1**. Follow these steps to troubleshoot common issues:

### 1. **Check Node.js and NPM Versions**

* Ensure you are using the correct Node.js and npm versions required for Angular v1.
* You can check the versions by running:

``` 
node -v
npm -v
```

* Ensure you're using **Node.js v10.x.x** (on old version) or **v20.x.x** (on modified version), which are compatible with Angular v1.

### 2. **Reinstall Node Modules**

* Sometimes, dependency issues may arise. Try removing and reinstalling the `node_modules` folder:

``` 
rm -rf node_modules
npm install
```

### 3. **Check for Console Errors**

* Open your browser's Developer Tools (usually by pressing **F12**) and look for errors in the **Console** tab. These will give clues about missing dependencies or syntax errors.

### 4. **Run in Development Mode**

* Use `gulp serve` to run the project in development mode and identify any errors during the build process:

``` 
gulp serve
```

### 5. **Troubleshoot Gulp Issues**

* If there are issues with Gulp tasks, ensure you have the correct versions installed globally:

``` 
npm install --global gulp-cli
gulp --version
```

### 6. **Dependency Conflicts**

* If there are package conflicts, try resolving them by running:

``` 
npm audit fix
```

### 7. **Cross-Origin Resource Sharing (CORS)**

* If you're encountering CORS errors (especially during API calls), ensure that the backend server is configured to allow requests from the frontend domain.

## **Backend Troubleshooting (Server Directory)**

The backend is based on the **PHP Slim Framework**. Follow these steps to troubleshoot the backend:

### 1. **Check PHP Version**

* Ensure that the correct PHP version is installed. PHP Slim v3 is compatible with PHP 7.4.x. You can check the version by running:

``` 
php -v
```

### 2. **Verify Dependencies**

* Ensure all required PHP dependencies are installed using Composer:

``` 
composer install
```

### 3. **Check Apache/Nginx Configuration**

* Ensure that your Apache or Nginx server is correctly configured to route requests to the Slim framework. The `public` folder should be the root directory.
* Check your **virtual host** configuration for proper routing.

### 4. **Check Logs**

* PHP errors will often be logged in the **error_log** file on your server. Check this file for any issues with routing, database connections, or PHP errors.

### 5. **Test API Endpoints**

* Use tools like **Postman** or **cURL** to manually test the API endpoints. Make sure the expected responses are being returned, and check for any errors.
* Example using cURL:

``` 
curl -X GET http://localhost/api/endpoint
```

### 6. **Database Connection**

* Ensure the backend is correctly connecting to your database. Check the **(.env) or (server/app/settings.php)** file for the correct credentials (host, username, password, database).
* Use MySQL CLI or phpMyAdmin to verify database connectivity.

### 7. **Cache Issues**

* If the backend seems unresponsive or stale, try clearing the PHP and server-side cache.

### 8. **Check CORS Configuration**

* Make sure that CORS is properly configured on the backend to allow API requests from the frontend application.
