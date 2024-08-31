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
  - 

## Create and configure a new Linux user on the Droplet (Security best practice)

## Deploy and run a Java Gradle application on Droplet
