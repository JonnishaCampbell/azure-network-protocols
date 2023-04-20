<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create our Resources
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>

1. Create our Resources
In Azure
	- create a Resource Group
	- create a Windows 10 virtual machine with the resource group, just created
	- create another virtual machine but with Linux (Ubuntu) and use the same resource group and virtual network

<p>
<img src="https://i.imgur.com/NL3aqMI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

2. Observe ICMP Traffic
	- Use RDP to connect to Windows 10 VM
	- Install Wireshark
	- Open Wireshark and filter ICMP traffic only
	- Get the private IP address of the Ubuntu VM and attempt to ping it from the Windows 10 VM
	- Observe the ping request and replies within Wireshark
	- Open the command line or PowerShell and attempt to ping a public website of your choice, and observe the traffic in Wireshark
	- Open the network security group in the Ubuntu VM and disable incoming (inbound) ICMP traffic
	- In the Windows 10 VM, you'll observe the ICMP traffic in WireShark and ping activity in the command line
		- You'll notice that the firewall (NSG) is prohibiting the ICMP inbound traffic
	- Re-enable the ICMP traffic by going back into the Ubuntu VM and enable the traffic through the Network Security Group
	- Back in Windows 10 VM, you'll see the ICMP traffic is pinging in WireShark and the command line
	- You can stop the ping activity by pressing "ctrl-c."
<p>
<img src="https://i.imgur.com/HSQQcn8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/4k6Sk1x.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/6lAdQII.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

3. Observe SSH Traffic
	- Go back to Wireshark and filter for SSH traffic
	- SSH into the Ubuntu VM by its private IP address
		- Type commands into Linux SSH like username, pwd, etc
		- Type exit and press enter to close the SSH connection

<p>
<img src="https://i.imgur.com/g5MT6AI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

4. Observe DHCP Traffic
	- Filter for DHCP traffic only in WireShark
	- Attempt to issue your Windows VM a new IP address by typing ipconfig/renew in the command line
	- Observe the DHCP traffic appearing in WireShark

<p>
<img src="https://i.imgur.com/OpgyITe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

5. Observe DNS Traffic
	- In Wireshark, filter DNS traffic
	- In the Windows 10 VM, use nslookup in the command line to look up common websites IP addresses, e.g., google.com
		- Observe the DNS traffic in Wireshark
    
<p>
<img src="https://i.imgur.com/GWBPwom.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>    

6. Observe RDP Traffic
	- Filter for RDP traffic in Wireshark
		- You can also type tcp.port==3389 instead of typing RDP
	- Observe the traffic in Wireshark
		- You'll see the traffic is endless since it's constantly showing a live stream from the actual computer to the VM computer


<p>
<img src="https://i.imgur.com/Bq9oEqB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
