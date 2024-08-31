# TWN_Demos_Module5
Demo Projects from Module 5 - Cloud &amp; Infrastructure as Service Basics with DigitalOcean

## Setup and Configure a Server on DigitalOcean
- Create a DigitalOcean account (https://cloud.digitalocean.com)
- Create a Droplet (MANAGE > Droplets > Create)
  - Choose a region that is geographically the closest to you
  - Choose an image -> Ubuntu
  - CPU options -> Regular + 512 MB CPU
  - Choose Authentication Method (to access the droplet) -> SSH Key
- Configure a Firewall (Networking > Firewalls > Create Firewall)
  - Inbound Rules: Type SSH, Protocol TCP, Port Range 22, Sources <myPublicIPAddress> -> needed to access the Droplet
  - Assign this Firewall to the Droplet
- ``ssh root@<ipOfDroplet>`` -> to connect to the Droplet
- Install Java on Droplet
  - Once connected to the Droplet, run ``apt install openjdk-8-jre-headless``

## Create and configure a new Linux user on the Droplet (Security best practice)
- You should not execute services or start applications with root users because you are giving the application root privileges
- Create a user for every application with only the permission it needs to run the app
- On the remote server, run ``adduser nameOfNewUser``
- In order to allow this user to run some commands as a root user, add the user to the "Sudo" group -> ``usermod -aG sudo nameOfNewUser``
- ``su - nameOfNewUser`` -> to log in as the new user
- We also need to add the ssh key for the new user, so that we can login with their credentials:
  - ``mkdir .shh`` -> to create .ssh folder into the root directory of the new user
  - ``sudo vim .ssh/authorized_keys`` -> to create a new file containing the SSH key (we need sudo privileges to enter the .ssh folder)
  - Copy and paste the public SSH key into that file

## Deploy and run a Java Gradle application on Droplet
- Build Jar File
  - clone java-react-example locally
  - ``cd java-react-example``
  - ``gradle build``
- Copy to remote Server
  - ``scp build/libs/java-react-example.jar root@IpOfDroplet:/root`` -> copy the jar file into the root folder of the remote server
- Run App on the remote Server
  - log into the remote server (``ssh root@<ipOfDroplet>``)
  - ``java -jar java-react-example.jar``
  - To access the application from the browser, we need to open the port the application is running on -> configure that on the firewall:
    - Inbound Rules -> Type custom, Protocol TCP, Port Range 7071, Sources IPv4 IPv6
    - http://ipOfDroplet:7071
