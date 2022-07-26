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
* Opened my public ip on browser and check if it is running. (it works)
