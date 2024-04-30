# Installing and Configuring Maven on Ubuntu 24.04 LTS

## Power On: Ubuntu

### 1. Install java

- Installing java-17-jdk
```bash
sudo apt-get install openjdk-17-jdk
```
- Check version
```bash
java -version
```

### 2.Installing packages for jenkins:

- wget is used to download contents directly from the terminal.
  #### Difference between yum and wget:
  - yum is used primarily in RedHat based Linux distributions, to manage software packages and     repositories.
  - While, wget is commandline utility used for downloading files from the Internet.

- To install packages, head to the official site of jenkins: [Jenkins](https://www.jenkins.io/doc/book/installing/linux/)
  ```bash
      sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \ https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
      echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]"https://pkg.jenkins.io/debian-stable binary/ | sudo tee \ /etc/apt/sources.list.d/jenkins.list > /dev/null
  ```
  
### 3. Update your system and proceed to install Jenkins
- Update:
  ```bash
  sudo apt-get update
  ```
- Install Jenkins:
  ```bash
  sudo apt-get install jenkins
  ```
- Start, enable and check status of jenkins:
  ```bash
  sudo systemctl start jenkins
  sudo systemctl enable jenkins
  sudo systemctl status jenkins
  ```

### 4. Logging into Jenkins
- Open firefox in Ubuntu and type in:
  ```bash
  localhost:8080
  ```
  #### To access jenkins via local machine:
  - Keep your Ubuntu on
  - Access a web browser in your local machine
  - Type in:
    ```bash
    your_Ubuntu-ip_address:8080
    ```
- Landed in Jenkins?
  Copy the path given
- In Ubuntu:
  ```bash
  sudo cat <copied path>
  ```
- The displayed is your password to Jenkins
- Head to the website:
  Paste your copied password
- Follow along the recommended/prompted instructions.

### 5. Installing Plugin "Maven Invoker"
- Jenkins dashboard on JMaster
- Manage Jenkins
- Manage Plugins
- Available
    - Search: Maven Invoker
- Install without restart
  ![mavin-invoker plugin](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Maven-screenshot/maven%20invoker.png)

### 6. Specifying JAVA_HOME and M2_HOME Path in Jenkins
- Jenkins dashboard
- Manage Jenkins
    - Global Tool Configuration
        - Add JDK
            - Name: Java
            - JAVA_HOME: /usr/lib/jvm/java-11.........
            - Uncheck "Install automatically"

        - Add Maven
          ![mavin install on jenkins](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Maven-screenshot/Maven-Configuration-Jenkins.png)
          
            - Name: Maven
            - MAVEN_HOME: /opt/apache-maven-<version>
            - Uncheck "Install automatically"

#### Apply and Save

### 7. Creating Java-Based Web Application Using Maven
```bash
mkdir -p /opt/mymaven
cd /opt/mymaven
```

- Search a web app Maven project in Google (copy)
```bash
mvn archetype:generate -DgroupId=com.javaweb -DartifactId=javaweb -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
```

- Go to javaweb directory
```bash
cd javaweb
ls
```

- To compile the code using Maven, it must be compiled from the path having POM.xml  
```bash
mvn compile
```

- Packaging the web app into a WAR file (which will be deployed in the application server)
```bash
mvn package
```
![image](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Maven-screenshot/mvn-package-success.png)

- After compile and package, a .war file will be created, which is the Java-based web app artifact.
```bash
cd target
ls
```
#### Now you are done with installing and Configuring maven on JMaster.

