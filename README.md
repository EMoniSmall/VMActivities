<h1>Observing Different Network Protocols 🔍 </h1>
<h2>Expectations 🤔</h2>

> [!Important]
> You will need **two** VMs to continue with this guide. One Microsoft 10 VM and one Linux (Ubuntu) VM. For assistance creating a VM through Azure, refer to [Microsoft Azure: Crash Course](https://github.com/EMoniSmall/azurecrashcourse). Make sure both VMs are created in the same resource group.

- Download Wireshark into an Azure VM
- Observe and Filter ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Set-Up 🏗</h2>

Step 1: Use Remote Desktop to connect to your Windows 10 VM.
Step 2: Inside your Windows 10 VM, visit www.wireshark.org and install Wireshark

![image](https://github.com/EMoniSmall/VMActivities/assets/166156618/8bac0873-df59-4ec2-ad39-92e7819b7817)

Step 3: Open Windows Powershell on your Windows 10 VM.

![image](https://github.com/EMoniSmall/VMActivities/assets/166156618/e9042164-67f6-478b-b051-f8a157d194b9)

<h2>Observing ICMP and Filtering Traffic 🚦</h2>

> [!Note]
> What is ICMP?
> 
>ICMP stands for Internet Control Message Protocol. It is used to send error messages and operational information during packet processing. It's often utilized by network devices like routers to communicate with each other and with hosts about network-related issues like unreachable destinations or congestion. It is crucial when diagnosing and troubleshooting connectivity problems.

Step 1: On Wireshark, select the Ethernet Connection and click the bluefin in the top left to capture packets. 

![mstsc_eOg2fhb6QQ](https://github.com/EMoniSmall/VMActivities/assets/166156618/0d2b3871-10f9-4887-9fe5-6d9c8c258067)

Step 2: In the search bar, "Apply a display filter", type "icmp". Observe the Virtual Network within Wireshark. You should now only see icmp traffic. 

Step 3: In Azure, retrieve the private IP for your Ubuntu (Linux) VM. This can be found under Networking in VM2 Properties.

Step 4: Inside VM1, in Windows Powershell, type ping, the private IP address, then "-t". This will initiate a perpetual ping to your Ubuntu VM. Observe the ping activity. 

![mstsc_FlzMu1O6j7](https://github.com/EMoniSmall/VMActivities/assets/166156618/c60aa471-bdc5-4910-9976-495391dc7781)

Step 5: In Azure, Find Network Security Group. Locate your Ubuntu Network security group, in this case VM2-nsg. Un the Left Click into Inbound Security Rules. Create a new Port Rule for Inbound Traffic. Click ICMP Protocol and Deny. Under Priority, enter a number below 300 and hit Add.

![chrome_QGzrRnkXrg](https://github.com/EMoniSmall/VMActivities/assets/166156618/c60e29db-aee5-4a75-ae19-b69e4805e700)

Step 6: Return to your Windows VM, Powershell and observe the ping requests. They should start to time out. Removing the protocol should allow the ping requests through again. 

Step 7: You can stop the perpetual ping in Powershell by pressing Ctrl + C.

<h2>Observing SSH Traffic 🚦</h2>

> [!Note]
> What is SSH?
> 
>SSH, or Secure Shell, is a cryptographic network protocol used for secure communication over an unsecured network. It provides encrypted connections between devices, typically allowing users to remotely access and manage systems securely, execute, comments, and transfer files. It is widely used in system administration, managing network devices, and secure file transfer.

Step 1: In your Windows VM, in Wireshark filter for SSH traffic only.

Step 2: In Windows Powershell, Type ssh, [your username for Ubuntu]@[Private IPaddress for VM2]. What this does is it allows VM1 to log into VM2. You can find the Private IP address for VM2 in Home> Virtual Machines > VM2 > Networking.

![Screenshot 2024-04-15 110134](https://github.com/EMoniSmall/VMActivities/assets/166156618/f167ffe9-f7e0-4f81-b05c-b6e8500117b9)

> [!Note]
> When entering the password for VM2 into the SSH terminal, it will not show up and will appear to not be typing. It will be typing in. Just keep faith that it is working.
>
> ![mstsc_RhnmUpif6x](https://github.com/EMoniSmall/VMActivities/assets/166156618/c6bed7c3-f614-4e55-95c4-5e88ad793036)

Step 3: Observe the SSH Traffic. From here, typing any commands, such as $ id, for example, will generate traffic on Wireshark. You can look up and play with some linux commands if you'd like.

Step 4: When finished, type $ exit to close the connection. 

> [!Note]
> Another way to filter for SSH on Wireshark is to type tcp.port==22. It is equivalent to typing SSH. 

<h1>Observing DHCP Traffic 🚦</h1>

> [!Note]
> What is DHCP?
> DHCP is traffic involving messages between a client and server for automatic network configuration. The client sends a request, the server responds with an offer, the client confirms and the server acknowledges. It's used to automatically assign an IP address.

Step 1: In Wireshark, filter for DHCP.

Step 2: Type in [ipconfig /renew]. This will tell the virtual network to assign a new IP address to VM1. 

Step 3: Once you hit Enter, you can observe the dhcp traffic on wireshark.

![mstsc_3tkaiDd3ks](https://github.com/EMoniSmall/VMActivities/assets/166156618/bc524757-0e7c-429d-b0d3-9d9a4ee9ac54)

<h1>Observing DNS Traffic 🚦</h1>

> [!Note]
> What is DNS?
> DNS stands for Domain Name System. It refers to the communication between DNS clients and DNS servers on a network. It involves clients asking servers for IP addresses that correspond to domain names. Clients send queries, and servers respond with IP addresses.

Step 1: On Wireshark, filter for DNS. You may notice it's already capturing DNS traffic.

Step 2: On Powershell, type [nslookup www.google.com]. You should see google.com responding with its ip address and other information.

![mstsc_EESfTlfqiA](https://github.com/EMoniSmall/VMActivities/assets/166156618/350f1e87-a7e5-45ee-8fd3-8492f91618f4)

<h1>Observing RDP Traffic 🚦</h1>

> [!Note]
> What is RDP Traffic?
> RDP stands for Remote Desktop Protocol. It is the data exchanged between a client and a server during a remote desktoip session. it allows users to control a remote computer as if they were physically present at that computer.

Step 1: In Wireshark, to filter for RDP traffic, type [tcp.port==3389]. You'll notice the immediate traffic on wireshark caused by our own current remote connection. Everything we type every mouse movement is transmitted here. 

![mstsc_cpjlHKlycg](https://github.com/EMoniSmall/VMActivities/assets/166156618/b6b23444-929e-44a5-abe4-160f3bdc57d7)


<h2>This concludes this guide. Thank you for reading. </h2>
