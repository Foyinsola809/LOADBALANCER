# LOADBALANCER

## SETTING UP A BASIC LOADBALANCE

#### Two instances that will be created, each with Apache web server installed. The necessary ports will be opened in each instance to allow traffic from anywhere. These instances will be updated to display their IP addresses. Additionally, an extra instance will be created with NGINX installed and configured to act as a load balancer, distributing traffic across the web servers. The steps below outline how this is achieved:


#### Step - 1 Create two instances.

The image below shows Instance 1 created and named `APACHECLB1`

![alt text](<img/01.int 1.png>)



The seconcd instance is created and shown below; `APACHELB2`

 ![alt text](<img/02.int 2.png>)

#### Step - 2 Add Port 8000

For the 2 intances, open port 8000 by editing the inbound rules for both, as shown in the images below

 ![alt text](<img/03.port 1.png>)


 ![alt text](<img/04.port 2.png>)



#### Step - 3 Connect the instances

Now that all the instances are set up, they will be connected from the local terminal through `SSH` as shown in the images below. it should be noted that the key should be made viewable before connection is attempted.
Here, the key pair is '`loadruner.pem' and the DNS will be used in the command instead of the IP address

The images below show how the connection for both instances are made.


 ![alt text](<img/05.SSHclient -1.png>) 


 ![alt text](<img/06.SSHclient -2.png>) 


 ![alt text](<img/07.Connect -1.png>) 


![alt text](<img/08.connect 2.png>) 

#### Step - 4 Install Apache

Once connected, apache is installed on both instances as below.

![alt text](<img/09.instap -1 .png>) 


![alt text](<img/10.verifyap -1.png>) 


![alt text](<img/11.instap 2.png>) 


![alt text](<img/12.verifyap 2.png>) 



#### Step - 5 configure Apache

Now that the apache is installed for each instance, the apache webserver will be configured to serve content on port 8000. This will involve creating a new index.html to display the IP address of the instance. The steps are shown below for both instances. 

Both need to be configured to listen from port 8000

![alt text](<img/13.editor 1.png>) 


![alt text](<img/14.conf 1.png>) 


![alt text](<img/15.editor 1.png>) 


![alt text](<img/16.conf 2.png>) 


As shown below, the default configuration must also be changed such that thier vitualhost port 80 is 8000

![alt text](<img/17.defaaultcode 1.png>) 


![alt text](<img/18.defaultchange 1.png>) 


![alt text](<img/19.defaultcode 2.png>) 


![alt text](<img/20.defaultchnage 2.png>) 

Once the above is completed, restart apache 

![alt text](<img/21.restartap 1.png>) 


![alt text](<img/22.restartap 2.png>) 

As mentioned ealier, index.html files are to be created. This will also be edited as shown below

![alt text](<img/23.index -1.png>) 

![alt text](<img/24.indexcode 1.png>) 


![alt text](img/25.index-2.png) 


![alt text](img/26.indexcode-2.png) 

The file ownership should also be changed for the index.html files

![alt text](<img/27.chmod 1.png>) 


![alt text](<img/28.chmod 2.png>) 

The default html file should be overidden as shown below.

once the overide is completed, restart apache2

![alt text](<img/29.overide 1.png>) 


![alt text](<img/30.overide 2.png>)

#### Step - 6 Update and dispplay IP address

By typing the IP address of both instances in the browser. the following is displayed in each case

![alt text](<img/31.welcome 1.png>) 


![alt text](<img/32.welcome 2.png>) 


#### Step - 7 Launch additional Intance

A new instance called `NGINXLB` is created. This will act as the loadbalancer. 

![alt text](img/33.inst-ng.png) 

Ensure port 80 is accepting traffic from anywhere

![alt text](img/33.port80.png) 

Connect into instance as shown below using SSH. 

![alt text](<img/34.connect 3.png>) 

#### Step - 8 Install NGNIX

Once connection is completed, update and install NGINX, and verify that it is active

![alt text](img/35.inst-ng.png) 


![alt text](<img/36 very-ng.png>) 

#### Step - 9 Configure NGINX

![alt text](img/37.confcode-ng.png) 

Edit the configuration file to ensure NGINX is acting as a load balancer by editing the backend servers to the IP addresses of the apache webservers and the IP address of the NGINX as the server

![alt text](img/38.editconf-ng.png) 

Test the configuration and restart NGINX
![alt text](img/40.ngtest.png) 

#### Step - 10 Display IP address

Paste the IP address of the NGINX and the should display the same pages being served by the webservers

![alt text](img/41.welcome-ng.png) 
