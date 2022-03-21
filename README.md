# Docker-sonarqube

## Introduction
This module implement sonarqube with docker using docker-compose

## What you’ll need
+ [Docker Desktop](https://www.docker.com/products/docker-desktop/)

### Build your project with docker compose
```
------------------------------------------------------------
Run command
------------------------------------------------------------
docker-compose -p {optional-name} up -d --force-recreate
```
### Unable to start  SonarQube in a Docker container and showed an error below
```
ERROR: [1] bootstrap checks failed. You must address the points described in the following [1] lines before starting Elasticsearch.
bootstrap check failure [1] of [1]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
```
Have to set the vm.max_map_count value to 262144 at least in your instance or virtual machine, we have two options here,

you can insert the new entry into the sysctl configuration file **/etc/sysctl .conf** with the required parameter,  
  

1 | `$ sudo vim /etc/sysctl .conf`
```
vm.max_map_count = 262144
```
and also execute the command below to reflect directly and change the current state of Kernel.    

1 | `$ sudo sysctl -w vm.max_map_count=262144`

You can verify the configured in the setting by running the command,  

1 | `$ sudo sysctl vm.max_map_count`
    
Finally, don't forget to restart the instance or use the command below,  

1 | `sudo sysctl --system`

**On Windows:**

If you're using the Windows system just follow the steps below,
  
Open a **PowerShell command prompt** and execute the command,  
```
wsl -d docker-desktop  
```
After that,  

1 | `sysctl -w vm.max_map_count=262144`

## How do I use it?
  
Once sonarqube is active, to access the administration console, you need to go to the following URL:

`http://localhost:9000`

The default user is **admin** and the default password is **admin**.

***Note***: *When you are logged in, sonarqube will ask you to update your password*.

### On Java
Add the following sonarqube configuration properties in your project:
```
sonar.projectName=<your-project>
sonar.projectKey=<your-project>
sonar.language=java
sonar.host.url=http://localhost:9000
sonar.login=admin
sonar.password=<your-password>
```
For more information on sonarqube configuration properties, you can click [here](https://docs.sonarqube.org/latest/analysis/analysis-parameters/)