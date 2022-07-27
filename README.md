# Basic webapp deployment on Azure
Hey guys this is my firt Azure project, I have created a basic HTML/CSS webpage and deployed on 4 servers
using Apache Server. I used Azure's load-balancers in this project to balance the load over each server.
This project basically seperates the users from India and users from all other countries to two different web pages.
for example if i am searching for my-project.in form india then i will be forwarded to the Indian servers,
here i have created two servers for each i.e. for indian users and other users so either i will be forwarded to indian server 1 or indian server 2 depending on the load over a server.

## Steps of project
### 1. Created Microsoft Azure account
* I sign up on Azure portal using my email id (portal.azure.com)
* I have used the free trial for this project.

### 2. Make Virtual Machines
* I created 4 Virtual Machines in azure (2 in East Japan region and 2 in West US 3 region)
#### Creating VMs (the procedure):
1. click on create in vm section
2. Create new resource group and name it
![image](https://user-images.githubusercontent.com/74852695/181093726-a1a9926f-6338-4bef-a6e7-92823465c4d7.png)

3. Name your VM (Indian Server 1 & 2 and US Server 1 & 2)
4. Select region (East Japan & West US)
5. Select the OS image you want (Ubuntu Server 20.04 in my case)
6. Choose authentication type (password in my case)
7. Select inbound port (SSH 22 because we are going to ssh into our servers for configuration)
8. Goto Disk and select any disk of your choice (leave everything default)
9. In Networking create new V-Net and new public IP and leave everything default
10. Goto monitoring and disable the Boot monitor it will save your cost.
11. Click on Review+Create and create. (done)
12. Goto your VM > Networking > indbound port rules > add rule and do the following.
![image](https://user-images.githubusercontent.com/74852695/181095185-1bcdfbe1-eaf9-4fcc-82b2-f9e1c04ba9cf.png)

This is required for allowing http port on vm.
> Make 2-2 VMs in same region, resource group and V-Net.

### 3. Configuring VMs
* Firstly SSH into server using terminal command (ssh username@publicIp )
* Installed Apache 2 in all servers (terminal: sudo apt-get install apache2)
* Changed the index.html file in /var/www/html with my index.html file and index.css file
* Opened my public ip on browser and check if it is running. (it works!!)
![image](https://www.server-world.info/en/note?os=Ubuntu_20.04&p=httpd&f=1)


### 4. Creating Application Gateways
* Search for application gateway and click click on create (Create 2).
![image](https://user-images.githubusercontent.com/74852695/181168515-b6efcde0-9203-4f3d-9337-fe507599ede8.png)

* Fill the details respected to different servers.
* Add frontend and Backend pool respectively.
* Review + Create
* After creating the application gateways try to search for gateway ip in browser to see if it is working i.e. it will land you on different server when you refresh it.
> Indian Server 1 ![image](https://user-images.githubusercontent.com/74852695/181169125-36693732-a0c6-4205-98a5-64a59318f8c0.png)
> Indian Server 2 ![image](https://user-images.githubusercontent.com/74852695/181169466-ccd65727-42df-4fa8-97e2-cd3dbbfaa5c9.png)


### Create Traffic Manager
* To manage the traffic over servers I have created traffic manager by searching and clicking on 'create'
* Named the Traffic manager and Routing method will be Geographic.
* Choose the same resource group used in US servers. 
* Review + Create
* After successfully creating traffic manager go to Endpoints and add 2 new endpoints.
* For india![image](https://user-images.githubusercontent.com/74852695/181176541-d4417af6-d44d-4beb-9701-85c4a68d2c56.png)
* For Others![image](https://user-images.githubusercontent.com/74852695/181176729-7f653dec-8e94-4c66-8b32-fdc6be83ab0b.png)


### Create a DNS zone
* Created DNS Zone using Azure search option and 'Create'
* Give same resource group as of US Servers
* Location will be global
* Create

### Used Freenom Free domain
* To get the free domain for my project i used www.freenom.com
* Registered there and searched for domain of my choice (azure-project.cf)
![image](https://user-images.githubusercontent.com/74852695/181171393-580427d7-5031-44f7-9dbd-a0ecadd090d9.png)

* Bought at 0.00$ 

### Attaching domain name to DNS zone
* Free domain to be attached to azure DNS zone
* Copy all the Name Servers and paste it in the domain in freenom.
* Open DNS Zone and click on 'Record Set'
* Enter Details as shown in image below,
* ![image](https://user-images.githubusercontent.com/74852695/181172291-077432fb-1d46-42f7-9e29-3ccc583e9699.png)
* Go to resource groups and add rules as per requirements

# The Project is Ready!
