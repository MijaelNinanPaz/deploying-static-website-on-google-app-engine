# Steps to deploy a static website on Google App Engine
## Steps:

### 1. Create a new Google Cloud console project or retrieve the existing project ID to use.
   
   We need the project ID which is probably similar to the project name, we find this ID in the Google Cloud dashboard.
  
### 2. Install and initialize Google Cloud CLI
   
   (The Google Cloud CLI works on Windows 8.1 and later and Windows Server 2012 and later.)

   **2.1. Download the Google Cloud CLI installer.**
         Or alternatively, open a PawerShell terminal and run the following commands:
       
         (New-Object Net.WebClient).DownloadFile("https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe", "$env:Temp\GoogleCloudSDKInstaller.exe")
         & $env:Temp\GoogleCloudSDKInstaller.exe

   **2.2. Launch the installer and follow the prompts.**
   
   **2.3. Google Cloud CLI requires Python.**
   
After installation is complete, the installer gives you the option to create Start Menu and Desktop shortcuts, start the Google Cloud CLI shell, and configure the gcloud CLI. Make sure that you leave the options to start the shell and configure your installation selected. The installer starts a terminal window and runs the ```gcloud init``` command.
   
   **2.5. It will ask us to log in to continue, we accept with "y", a window will open in the browser to continue with the login and we click on allow.**
   
### 3. Preparing files
   **3.1. Create a directory that has the same name as your project ID.**
   
   The created directory must contain the project files
   
   **This guide uses the following structure for the project:**
  
    - app.yaml: Configure the settings of your App Engine application.
    - www/: Directory to store all of your static files, such as HTML, CSS, images, and JavaScript.
        - css/: Directory to store stylesheets.
          - style.css: Basic stylesheet that formats the look and feel of your site.
        - images/: Optional directory to store images.
        - index.html: An HTML file that displays content for your website.
        - js/: Optional directory to store JavaScript files.
        - Other asset directories.

### 4. Creating the app.yaml file
  The app.yaml file is a configuration file that tells App Engine how to map URLs to your static files. In the following steps, you will add handlers that will load www/index.html when someone visits your website, and all static files will be stored in and called from the www directory.

  **Create the app.yaml file in your application's root directory:**
  
  Edit the app.yaml file and add the following code to the file:

``` 
runtime: python27
api_version: 1
threadsafe: true

handlers:
- url: /
  static_files: www/index.html
  upload: www/index.html

- url: /(.*)
  static_files: www/\1
  upload: www/(.*)
```
### 5. Deploying your application to App Engine

**5.1. To deploy your app, run the following command from within the root directory of your application where the app.yaml file is located:**

```
gcloud app deploy
```

**5.2. choose the region**

The services to be deployed are shown and if we continue the configuration and deployment will end.

