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

  Read this file; [Tomcat_config](https://github.com/SirJosh-i/Tomcat-Config.git). It contains the complete instructions for installing and configuring the Tomcat Server.

## 2. Installing and Configuring Maven

This section provides instructions for installing and configuring Maven as part of the CI/CD pipeline setup. It covers the necessary steps to set up Maven on the Jenkins server, enabling seamless integration for building and packaging Java web applications.

  ### Project File
  Read this file to complete instructions for installing and configuring Maven; [Maven_config](https://github.com/SirJosh-i/Maven-Config.git)

## 3. Jenkins Pipeline for Maven Java Web App

This section details the Jenkins pipeline for building and deploying Java web applications using Maven. It guides you through configuring Jenkins to automate the integration of Maven, GitHub, and Tomcat Server. The pipeline includes steps for pulling source code, building the Maven project, packaging the Java web application, and deploying the artifact.

  ### Creating a New Repo in GitHub for Our Java-based Web Website

  To start, follow these steps to create a new repository on GitHub for your Java-based web application.

  - Login to GitHub.
  - Create a new repository named `mymaven`.
  ![image](https://github.com/SirJosh-i/Basic-Devops---CI-CD/assets/69949528/21fe0211-e5e6-441e-af16-ba19ee6e9907)

  - Copy the repository URL.

  On the developer's machine:

  ```bash
  # Create a folder for your project
  mkdir -p /root/project/mymaven
  cd /root/project/mymaven/

  # Clone an existing Maven project or initialize a new one
  git pull <any existing Maven project>
  # Remove unnecessary files if any

  # Initialize and push to the new GitHub repository
  git init
  git remote add origin <your repo URL>
  git pull origin master
  git add -A
  git commit -m "maven java web app first commit"
  git push origin master
  ```
  ### Install the "Deploy to Container" Plugin in Jenkins Master
  Ensure the Jenkins master is set up with the necessary plugins.
  ![deploy-plugin](![Deploy to container plugin download](https://github.com/SirJosh-i/Basic-Devops---CI-CD/assets/69949528/49ec78ee-4a52-4d51-a8fd-99f28670bc3c))
  ```markdown
  - Open Jenkins dashboard.
  - Navigate to "Manage Jenkins" 
    -> "Manage Plugins."
  - In the "Available/Installed"
    -> Search for "Deploy to Container."
  - Install the plugin without restarting Jenkins.
  ```
  Start and enable the NTP server:
  ![start-enable](![chronyd setup](https://github.com/SirJosh-i/Basic-Devops---CI-CD/assets/69949528/4d9c5e2b-3eb2-4302-b5c7-77f30ba893d5))
  ```bash
  systemctl start chronyd
  systemctl enable chronyd
  ```
  ### Creating a Jenkins Job for Maven Java Web App Deployment
  Follow these steps to create a Jenkins job for building and deploying your Java web application.

  - Open Jenkins dashboard.

  - Create a new freestyle project.

  ![freestyle-job](![create jenkins job](https://github.com/SirJosh-i/Basic-Devops---CI-CD/assets/69949528/f0f7c94e-c818-4182-bea3-c09a39d25b1a))
  
  - Set Git repository URL and credentials.
  ![git-code](https://github.com/anilrajrimal1/mymaven/blob/master/screenshots/add%20repo%20to%20job.png)

  - Use "Poll SCM" for build triggers.
  ![buld-trrigres](![poll scm](https://github.com/SirJosh-i/Basic-Devops---CI-CD/assets/69949528/233d8f0c-944e-48c3-9650-9c52c6104a75))

  - Configure build steps for Maven and Invoke top-level Maven target.
  ![top-level](![mavin-invoker plugin](![top level maven](https://github.com/SirJosh-i/Basic-Devops---CI-CD/assets/69949528/f1f34954-a988-4b39-936d-3169b6432c27)))
