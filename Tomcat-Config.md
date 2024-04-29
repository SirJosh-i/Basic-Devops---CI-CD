# Installing and Configuring Tomcat Server

## Power On: Webserver

Apache Tomcat is an application server and a servlet container. Combining the concept of both http and servlet, we have a single tomcat server.

## 1. Install Java

  - To install Java:
    ```bash
    yum -y install java-11-openjdk
    ```
  - Set Alternative:
    ```bash
    alternatives --config java(Select your appropriate version)
    ```
    ![alt-java](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Tomcat-pics/alternatives-java.png)
  - Check version:
    ```bash
    java --version
    ```
    ![java-version](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Tomcat-pics/java-version.png)
    
## 2. Set JAVA_HOME Variable Path
  - Goto the path where your java lies:
    ```bash
    cd /usr/lib/jvm/java-11<tab>
    ```
  - To display the path you are in:
    ```bash
    pwd
    ```
    ![java-pwd](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Tomcat-pics/java-pwd.png)
  - Copy the displayed path:
    ```bash
     vi /root/.bash_profile
    ```

  - Add the following lines to .bash_profile:
      ```bash
      JAVA_HOME=(paste the copied path)
      PATH=$HOME/bin:$JAVA_HOME
      ```
  - Refresh the profile:
    ```bash
    . /root/.bash_profile
    # OR
    source /root/.bash_profile
    ```

## 3. Download Apache Tomcat in the form of .tar.gz and extract it

   - Make a new directory:
     ```bash
     mkdir /opt
     cd /opt
     ```

   - Download and extract Apache Tomcat:
     Go to Apache Tomcat's official server and copy the link (.tar.gz) of your preferred version
     ```bash
     wget <paste the copied link>
     tar -zxvf <download file>.tar.gz
     ```
     
     ```bash
     cd /opt/apache-<tab>/bin
     ```
     
     - Linking startup.sh and shutdown.sh to tomcatup and tomcatdown respectively
     ```bash
     ln -s /opt/apache-tomcat<tab>/bin/startup.sh /usr/local/bin/tomcatup
     ln -s /opt/apache-tomcat<tab>/bin/shutdown.sh /usr/local/bin/tomcatdown
     ```
     ```bash
     echo $?  #zero indicates success
     ```

## 4. Change the port of Tomcat Server(eg: 8090) or keep it default(8080)

  - Search for the connector port and modify it to 8090:
    ```bash
    cd /opt/apache-tomcat-<tab>/conf
    vi server.xml
    ```

## 5. Firewall

  - Install firewall(If not installed):
    ```bash
    yum -y install firewalld
    ```
  - Start and enable firewall:
    ```bash
    systemctl start firewalld
    systemctl enable firewalld
    systemctl status firewalld #Checking if the firewall is active.
    ```
  - Allow port: 8090 in Firewall:
    
    ```bash
    firewall-cmd --permanent --add-port=8090/tcp
    firewall-cmd --reload
    firewall-cmd --list-all
    ```
    
## 6. Allow access to the Tomcat Server from any remote hosts

  - Edit context.xml located inside host-manager:
    ```bash
      cd /opt/apache-tomcat<tab>/webapps/host-manager/META-INF
      vi context.xml
    ```
  - Search for Valve and comment it:
    ```bash
      <!--<Valve...>-->
    ```
  - Also edit .xml file inside manager:
    ```bash
      cd /opt/apache-tomcat<tab>/webapps/manager/META-INF
      vi context.xml
    ```
  - Search for Valve and comment it:
    ```bash
      <!--<Valve...>-->
    ```
Now, Open a browser locally or remotely to test the Apache Tomcat server, URL:http://your-ip_address:8090
![Apache Tomcat-Server](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Tomcat-pics/apache-tomcat.png)

### 7. Setup Credentials to Login into 'Manager App'
```bash
cd /opt/apache-tomcat<tab>/conf
vi tomcat-users.xml
```
Add the following lines to tomcat-users.xml:
```bash
<role rolename="Manager-gui"/>
<role rolename="Manager-script"/>
<role rolename="Manager-jmx"/>
<role rolename="Manager-status"/>

<user username="tomcat" password="tomcat123" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
<user username="deployer" password="deployer123" roles="manager-script"/>
```
Save and exit.

### 8. Refresh the Changes
```bash
tomcatdown
tomcatup
```

# Alternative to Tomcat-Installation:

## 1. Installing Tomcat directly from the Internet:
- Yum is an open-source commandline package installer
  ```bash
  yum -y install tomca
  ```

## 2. Modify JAVA options utilized by Tomcat during startup
  - Config tomcat.conf 
    ```bash
      nano /usr/share/tomcat/conf/tomcat.conf
    ```
    
  - Add the following line:
    ```bash
      JAVA_OPTS="-Djava.security.egd=file:/dev/./urandom -Djava.awt.headless=true -Xmx256m -         XX:MaxPermSize=128m -XX:+UseConcMarkSweepGC"
    ```

## 3. Installing Tomcat-webapps and Tomcat-admin-webapps
  - Allows you to manage deployed web applications.
    ```bash
      yum -y install tomcat-webapps tomcat-admin-webapps
    ```
    
## 4. To login to "Manager App"
  - To utilize previously installed manager webapps, we establish a login for tomcat users
  ```bash
    nano /usr/share/tomcat/conf/tomcat-users.xml
   ```
  - Insert the following in between <tomcat-users>...</tomcat-users>
    <user  username="admin" password="A-STRONG-PASSWORD" roles="manager-gui,admin-gui"/>
  ### Do not forget to edit username and password.

## 5. Refresh the changes
  - Refresh Daemon
    ```bash
    systemctl daemon-reload
    ```
  - Start tomcat
    ```bash
    systemctl start tomcat
    ```
Now, the tomcat server is installed and configured on your webserver. You can access the manager app with the provided credentials. 

## 10. Using the credentials to login into Apache Tomcat
![Manager-app-login](https://github.com/SirJosh-i/Basic-Devops---CI-CD/blob/master/Tomcat-pics/tomcat-credentials.png)

    
