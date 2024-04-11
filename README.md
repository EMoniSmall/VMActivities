<h1>Observing Different Traffic Types in a Virtual Network 🔍 </h1>
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

Step 3: Open another Remote Desktop connection and log into your Linux (Ubuntu) VM.

<h2>Observing ICMP Traffic 🚦</h2>

Step 1: On Wireshark, select the Ethernet Connection and click the bluefin in the top left to start capturing packets. 

![mstsc_eOg2fhb6QQ](https://github.com/EMoniSmall/VMActivities/assets/166156618/0d2b3871-10f9-4887-9fe5-6d9c8c258067)

Step 2: In the search bar, "Apply a display filter", type "icmp". Observe 
