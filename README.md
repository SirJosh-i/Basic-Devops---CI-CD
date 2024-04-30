# Project: CI/CD Setup with Github, Jenkins, Maven and Tomcat

![image](https://github.com/SirJosh-i/Basic-Devops---CI-CD/assets/69949528/e7db2155-41e7-4c0b-a865-efc29117003b)


## Overview

This project focuses on setting up a Continuous Integration/Continuous Deployment (CI/CD) pipeline using GitHub, Jenkins, Maven, and Tomcat. The primary objectives include setting up Jenkins, configuring Maven and Git, setting up a Tomcat Server, integrating GitHub, Maven, and Tomcat Server with Jenkins, creating CI and CD jobs, and testing the deployment of a Java web application.

# Table of Contents

1. Installing and Configuring Tomcat Server
2. Installing and Configuring Maven
3. Jenkins Pipeline for Maven Java Web App

## 1. Installing and Configuring Tomcat Server

This section provides instructions for installing and configuring Tomcat Server as part of the CI/CD pipeline setup. It outlines the essential steps to ensure a successful deployment environment for the Java web application

  ### Project File

  Read this file; [Tomcat_config](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Tomcat-Config.md). It contains the complete instructions for installing and configuring the Tomcat Server.

## 2. Installing and Configuring Maven

This section provides instructions for installing and configuring Maven as part of the CI/CD pipeline setup. It covers the necessary steps to set up Maven on the Jenkins server, enabling seamless integration for building and packaging Java web applications.

  ### Project File
  Read this file to complete instructions for installing and configuring Maven; [Jenkins_maven-config](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Jenkins-config.md)

## 3. Jenkins Pipeline for Maven Java Web App

This section details the Jenkins pipeline for building and deploying Java web applications using Maven. It guides you through configuring Jenkins to automate the integration of Maven, GitHub, and Tomcat Server. The pipeline includes steps for pulling source code, building the Maven project, packaging the Java web application, and deploying the artifact.

  ### Creating a New Repo in GitHub for Our Java-based Web Website

  To start, follow these steps to create a new repository on GitHub for your Java-based web application.

  - Login to GitHub.
  - Create a new repository named `mymaven`.
  ![image](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Maven-screenshot/mymaven-repo-created.png)
  - Copy the repository URL.

  ### On the developer's machine
  #### Clone an existing maven project: Check [Maven_config](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Jenkins-config.md) for more information.
    ```bash
      # Create a folder for your project
      mkdir -p /root/project/mymaven
      cd /root/project/mymaven/
      
      # Clone an existing Maven project
      git clone <any existing maven repo>
      git add .
      git commit -m "Maven-Web_project"
      git push origin master
    ```
    
  ### Install the "Deploy to Container" Plugin in Jenkins Master
  Ensure the Jenkins master is set up with the necessary plugins.
  ![Deploy to container plugin download](https://github.com/SirJosh-i/Basic-Devops---CI-CD/assets/69949528/49ec78ee-4a52-4d51-a8fd-99f28670bc3c)
  ```markdown
  - Open Jenkins dashboard.
  - Navigate to "Manage Jenkins" 
    -> "Manage Plugins."
  - In the "Available/Installed"
    -> Search for "Deploy to Container."
  - Install the plugin without restarting Jenkins.
  ```
### 5. Creating a Jenkins Job for Maven Java Web App Deployment
Follow these steps to create a Jenkins job for building and deploying your Java web application.

- Open Jenkins dashboard.
- Create a new freestyle project.
  ![freestyle-job](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Maven-screenshot/MyMaven-package.png)
  
- Set Git repository URL and credentials.
  ![git-code](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Maven-screenshot/Git-integration-jenkins.png)

- Use "Poll SCM" for build triggers.
  ![buld-trrigres](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Maven-screenshot/Poll%20SCM.png)

- Configure build steps for Maven and Invoke top-level Maven target.
  ![top-level](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Maven-screenshot/Invoke%20top%20level%20-%20Maven%20targets.png)

- Add a post-build action to deploy the WAR file to a Tomcat container.
  ![post-build](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Maven-screenshot/Post%20build%20actions.png)

- Configure container details, including the URL, credentials, and WAR file path.
  ![global-cred](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Maven-screenshot/ssh%20key%20-%20tomcat%20-%20jenkins%20global%20config.png)

- Apply and save the configuration.

Access your deployed web application at http://your-ip-address/javaweb.

  ![webserver-output](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Tomcat-pics/deployed%20-%20tomcat.png)

