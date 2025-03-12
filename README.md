<h1>Setting Up the Environment</h1>

<h2>Overview:</h2>

- <b>Create Resource Group and Virtual Network – Establish the foundation in Azure</b> 
- <b>Create Domain Controller VM (DC-1) – Install Windows Server 2022 and configure networking.</b>
- <b>Create Client VM (CLIENT-1) – Connect to the same Virtual Network as DC-1 and configure DNS settings.</b>
- <b>Verify Connectivity – Test the connection between DC-1 and Client-1.</b>

<h2>Setup Domain Controller in Azure</h2>

Create a Resource Group  <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/1.1%20create%20resource%20group.PNG)
<br />

Create a Virtual Network and Subnet <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/1.2%20create%20virtual%20network.PNG)
<br />

Create the Domain Controller VM (Windows Server 2022) named “DC-1”  <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/1.3%20create%20vm%20dc-1.PNG)
![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/1.3a%20create%20vm%20dc-1.PNG)
<br />

Go to DC-1 VM <br/>
Go to Networking -> Network Settings -> Network interface/IP configuration <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/1.4%20set%20private%20ip%20nic%20to%20static.PNG)
<br />

After VM is created, set Domain Controller’s NIC Private IP address to be static <br/>
Go to settings -> IP Configurations <br/>

- <b>Click on ipconfig1</b> 
- <b>Set allocation to Static and Private IP address to 10.0.0.4</b>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/1.4a%20set%20private%20ip%20nic%20to%20static.PNG)
<br />

Connect to DC-1 via remote connection <br/>
Log in using credentials <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/1.5%20rdp%20into%20dc-1.PNG)
![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/1.5a%20rdp%20into%20dc-1.PNG)
<br />

Go to Window Defender Firewall  <br/>
Click on Windows Defender Firewall Properties <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/1.5b%20disable%20firewall.PNG)
<br />

Turn Firewall State OFF for the following: <br/>

- <b>Domain Profile</b> 
- <b>Private Profle</b>
- <b>Public Profile</b>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/1.5c%20disable%20firewall.PNG)
![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/1.5d%20disable%20firewall.PNG)
![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/1.5e%20disable%20firewall.PNG)
<br />

<h2>Setup CLIENT-1 in Azure</h2>

Create the Client VM (Windows 10) named “ClIENT-1” <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/2.1%20create%20client%20vm.PNG)
<br />
<br />
<h3>After VM is created, set Client-1’s DNS settings to DC-1’s Private IP address</h3>

Take note of DC-1 private IP address <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/2.2%20set%20Client-1%E2%80%99s%20DNS%20settings%20to%20DC-1%E2%80%99s%20Private%20IP%20address.PNG)
<br />

Click on CLIENT-1 VM <br/>
Go to Networking -> Network Settings -> Network Interface/IP Configuration <br/> 

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/2.2a%20set%20Client-1%E2%80%99s%20DNS%20settings%20to%20DC-1%E2%80%99s%20Private%20IP%20address.PNG)
<br />

Go to Settings -> DNS Servers <br/>

- <b>Set DNS Servers to Custom</b> 
- <b>Set DNS Server to 10.0.0.4 (DC-1 private IP address)</b>
- <b>Save</b>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/2.2b%20set%20Client-1%E2%80%99s%20DNS%20settings%20to%20DC-1%E2%80%99s%20Private%20IP%20address.PNG)
<br />

Go to virtual machines, select CLIENT-1 <br/>
Restart<br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/2.3%20restart%20client%20vm.PNG)
<br />

Connect to CLIENT-1 via remote connection  <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/2.4%20rdp%20into%20client%201%20vm.PNG)
![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/2.4a%20rdp%20into%20client%201%20vm.PNG)
<br />

Ping the DC-1 private ip address 10.0.0.4 <br/>
Make sure the ping succeeded <br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/2.5.1%20ping%20dc%20vm.PNG)
<br />

Run ipconfig /all <br/>
The output for the DNS settings should show DC-1’s private IP Address 10.0.0.4<br/>

![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/2.5.2%20ipconfig%20all.PNG)
![](https://github.com/rbrianshutt/active_directory/blob/main/Active%20Directory%202.0/2.6%20hostname.PNG)
