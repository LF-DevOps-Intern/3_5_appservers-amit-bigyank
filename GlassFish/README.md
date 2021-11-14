First we can simply install java 11 with the following command

```bash
sudo apt-get install openjdk-11-jdk
```

![enter image description here](https://i.imgur.com/Wb4nXNx.png)
To install glassfish6 we first have to download the zip file with the help of wget and extrat it

```bash
wget https://github.com/eclipse-ee4j/glassfish/releases/download/6.2.2/glassfish-6.2.2.zip

unzip glassfish-6.2.2.zip
```

Move the Glassfish server to the /**opt**/ directory by using the following command. Although we can move it to any place and run.

```bash
mv glassfish6 /opt
```

First, change current working directory by using the following command.

```bash
 cd glassfish6/opt/bin
```

Now, Start the server.

```bash
 ./asadmin start-domain
```

Since the port [8080] is already in use by the ssh service, glassfish will throw and error

![enter image description here](https://i.imgur.com/05gXOi4.png)

To change the port number go to `glassfish4\glassfish\domains\domain1\config` folder and here open `domain.xml` file and find tag

```java
<network-listeners>
    <network-listener port="8080" protocol="http-listener-1" transport="tcp" name="http-listener-1" thread-pool="http-thread-pool"></network-listener>
</network-listeners>

```

in `port` attribute of `<network-listeners>` you can specify your port address to 8088

![enter image description here](https://i.imgur.com/Oxvw3xn.png)
Now we can sucessfully start the glassfish server

![enter image description here](https://i.imgur.com/p7dvCbv.png)

We also need the allow the port in our firewall to access the server from outside of our network

![enter image description here](https://i.imgur.com/5a1BW7k.png)
Now we can visit the ip address of our server along with the port in the browser and verify that the server is running

![enter image description here](https://i.imgur.com/tsPX17w.png)
To create a demo Java (11) servlet application with maven, first we need to install maven with following command

```bash
apt install maven
```

To create a project open the console and enter the command

```java
mvn archetype:generate -DgroupId=bigyank.com.np -DartifactId=MavenTestWebProject -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
```

- DgroupId – This parameter specifying the package path
- DartifactId – This parameter specifies actual project name
- DarchetypeArtifactId – This parameter specifies the type of project. **maven-archetype-webapp** is a standard command for creating the web projects.

![enter image description here](https://i.imgur.com/c0au4uF.png)
Remove all the children of `<properties>` tag in `pom.xml` file and replace them with the following to compile the project with Java 11

```xml
<properties>
 <maven.compiler.release>11</maven.compiler.release>
</properties>
```

To generate the war package simply navigate to the project folder and put the following command

```
mvn package
```

![enter image description here](https://i.imgur.com/rBK4vC7.png)

Now we can finally deploy this war package. To deploy we have to enter the following command

```bash
./asadmin deploy <path/to/war/file>
```

![enter image description here](https://i.imgur.com/KFQO5Tq.png)
We can verify the deployed app from our admin portal of glasswire which runs on port 4848 so first we need to allow this port on our firewall

![enter image description here](https://i.imgur.com/2igSRkt.png)
