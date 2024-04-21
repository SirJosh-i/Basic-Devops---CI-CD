# Installing and Configuring Maven

## Power On: JMaster

### 1. Install Java first

- To install Java
```bash
yum -y install java
java -version
```
- Remove old version JDK(optional)
```bash
yum -y remove (version)
```
- Or, choose alternative:
```bash
alternatives --config java
```
- Check version
```bash
java -version
```


### 2. Set JAVA_HOME Variable Path

```bash
cd /usr/lib/jvm/java-11<tab>
```
```bash
pwd 
```
copy displayed path

```bash 
vi /root/.bash_profile
```
Add the following lines to .bash_profile:
```bash
JAVA_HOME=(paste the copied path)
PATH=$PATH:$HOME/bin:$JAVA_HOME
```
Then refresh the profile:
```bash
. /root/.bash_profile

# OR

source /root/.bash_profile 
```
### 3. Installing Maven on JMaster (and Slave Machines if any, Developers if needed)

- make a new dir opt
```bash
mkdir /opt
cd /opt
```
- Download and extract Maven

goto the Maven official site and copy .tar.gz binary file link

```bash
wget <paste the copied link>
```
```bash
tar -zxvf apache-maven<tab>.tar.gz
```
### 4. Set M2 and M2_HOME Variable Path

```bash
cd /opt/apache-maven<tab>

pwd   # Copy the path

vi /root/.bash_profile
```
Add the following lines to .bash_profile:
```bash
M2_HOME=/opt/apache-maven-3.9.6
M2=$M2_HOME/bin
PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$M2
```
Then refresh the profile:
```bash
source /root/.bash_profile
```
Verify the configuration:
```bash
echo $M2_HOME
echo $M2
echo $PATH
mvn -version
```

### 5. Installing Plugin "Maven Invoker"
- Jenkins dashboard on JMaster
- Manage Jenkins
- Manage Plugins
- Available
    - Search: Maven Invoker
- Install without restart

  ![mavin-invoker plugin](https://github.com/SirJosh-i/Maven-Config/assets/69949528/f13cceea-cf0d-40bd-b166-6071116360a1)


### 6. Specifying JAVA_HOME and M2_HOME Path in Jenkins
- Jenkins dashboard
- Manage Jenkins
    - Global Tool Configuration
        - Add JDK
            - Name: Java
            - JAVA_HOME: /usr/lib/jvm/java-11.........
            - Uncheck "Install automatically"

        - Add Maven
          
          ![mavin install on jenkins](https://github.com/SirJosh-i/Maven-Config/assets/69949528/d8e892d4-6c7e-4bc9-adc9-c1700be7810e)

          
            - Name: Maven
            - MAVEN_HOME: /opt/apache-maven-<version>
            - Uncheck "Install automatically"

Apply and Save

### 7. Creating Java-Based Web Application Using Maven
```bash
mkdir -p /opt/mymaven
cd /opt/mymaven
```
Search a web app Maven project in Google (copy)

Example : 

```bash
mvn archetype:generate -DgroupId=com.javaweb -DartifactId=javaweb -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
```

```bash
cd javaweb
```
you can also Push the project to GitHub so that it can be pulled on developer machines later on.

```bash
ls
```
To compile the code using Maven, it must be compiled from the path having POM.xml
```bash
mvn compile
```
Packaging the web app into a WAR file (which will be deployed in the application server)
```bash
mvn package
```
After compile and package, a .war file will be created, which is the Java-based web app artifact.
```bash
cd target

ls
```
Now you are done with installing and Configuring maven on JMaster.
