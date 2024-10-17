# Project-Control-traffic-using-azure-load-balancer

**2types:**
Public load balancer->handling requests comes from outside of the vnet
Private load balancer->handling requests comes from inside of the vnet

**Description:**
Here we are going to configure two websites in 2 virtual machines. Then hit request and check how load balancer handles the request and sent to virtual machines

**Procedure:**
Step 1 : **create availability set**
Go to azure portal->search availability set->click create->give faultdomain 2, update domain1

Step2 : **create 2 virtual machines and set into availability set**
Go to azure portal->search virtual machines->click create vm1->give name,subscription,resource group,vnet,region->select availability option as availability set->allow ports3389,80(http,rdp) ->click review and create.
Go to azure portal->search virtual machines->click create vm2->give name,subscription,resource group,vnet,region->select availability option as availability set->allow ports3389,80(http,rdp) ->click review and create.

Step3 :**configure websits in both virtual machines**
login virtial machine1->go to server managaer->click add rules and features->click next->select role based or feature based->clicck next->select webserver(IIS)->clicck next->click install.

After installing,
Go to Internet Information Service(IIS) manager->right click vm1->right click default website->click explorer->edit png file and save(i.e)adding extra keyword on png pic

Similarly, you can login virtual machine2 inside virtual machine1 and configure another website in vm2.

To view your webpage, type localhost in browser insider your virtual machines.

Step 4: **Create load balancer**
Go to azure portal->search load balancer->click create->give subscription,resourcegroup,region->load balancer type as standard->select public load balancer->create new public ip for load balancer in frontend details->select vnet as backend and add both virtual machines by selecting NIC card->add load balancer rules such as frontend(loadbalancer),backend(backendpools),protocol(tcp),port(80),create healthprobe(tcp,80),session persistance(client iP),ideal timeout(4mins)-> click create

Step5:**To check how it's worked**

copy the public ip of load balancer and enter in your localsystem browsers to see which vitual machine webpage is shown whther it is vm1 webpage or vm2 webpage.
