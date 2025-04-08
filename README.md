<h1 align="center">Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines using Wireshark</h1>

<h1 align="center"> Setting NSGs & Inspecting Traffic in Azure </h1> 

<p align="center">
<img src="https://media.licdn.com/dms/image/v2/D4D12AQGOxeJbAJEPWg/article-cover_image-shrink_600_2000/article-cover_image-shrink_600_2000/0/1694217648572?e=2147483647&v=beta&t=38G-4FyIB9rFftVAczYfUvZl5T8Ry5sf02MQdEJcrTU" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p align="center"> In this tutorial, we will observe various network traffic to and from Azure Virtual Machines with Wireshark and experiment with Network Security Groups. <br />
</p> 


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (ICMP, SSH, DHCP, DNS, RDP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create a Resource Group
- Create a Virtual Machine
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>
</br>
</br>
<h3 align="center">
  Set up your virtual environment
</h3>
</br>
<p>
  # Simple Guide: Watching Network Traffic in Azure with Wireshark

This guide shows you how to use Wireshark to watch network traffic between Azure Virtual Machines and test Network Security Groups (NSGs).

## Tools You’ll Use
- Microsoft Azure (to create Virtual Machines)
- Remote Desktop (to connect to your Windows VM)
- Command-Line Tools
- Network Protocols (ICMP, SSH, DHCP, DNS, RDP)
- Wireshark (to watch network traffic)

## Operating Systems
- Windows 10
- Ubuntu Server 20.04

## Steps Overview
1. Set up a Resource Group in Azure.
2. Create two Virtual Machines (Windows and Ubuntu).
3. Watch ICMP Traffic.
4. Watch SSH Traffic.
5. Watch DHCP Traffic.
6. Watch DNS Traffic.
7. Watch RDP Traffic.

## Step-by-Step Instructions

### Step 1: Set Up Your Azure Environment
- **Create a Resource Group in Azure**  
  Go to Azure and make a new Resource Group.  
  <img src="https://i.imgur.com/dOAeXqs.png" height="75%" width="100%" alt="Resource Group"/>

- **Create a Windows Virtual Machine (VM)**  
  In Azure, create a Windows 10 VM in the (US) East US region. Use the Resource Group you made. Let it create a new Virtual Network (Vnet) and Subnet. Choose the password option for the Administrator Account.  
  <img src="https://i.imgur.com/PHOwjLh.png" height="75%" width="100%" alt="Windows VM"/>

- **Create an Ubuntu Virtual Machine (VM)**  
  In Azure, create an Ubuntu Server 20.04 VM. Use the same Resource Group. Let it create a new Vnet and Subnet. Choose the password option for the Administrator Account.  
  <img src="https://i.imgur.com/N5zwQUH.png" height="75%" width="100%" alt="Ubuntu VM"/>

- **Check Your Network in Network Watcher**  
  In Azure, go to Network Watcher to see your Virtual Network setup.  
  <img src="https://i.imgur.com/Pn02GXF.png" height="75%" width="100%" alt="Network Watcher"/>

---

### Step 2: Watch ICMP Traffic
- **Connect to Your Windows VM and Set Up Wireshark**  
  Use Remote Desktop to connect to your Windows 10 VM. Install Wireshark, open it, and filter for ICMP traffic only.  
  <img src="https://i.imgur.com/0BsfNiS.jpg" height="75%" width="100%" alt="Microsoft Remote Desktop - Mac"/>

- **Ping the Ubuntu VM**  
  Find the private IP address of your Ubuntu VM. In the Windows VM, open a command prompt and ping the Ubuntu VM’s IP. Watch the ping requests and replies in Wireshark.  
  <img src="https://i.imgur.com/yYGKuAy.png" height="75%" width="100%" alt="Ubuntu private IP"/>  
  <img src="https://i.imgur.com/3h9QSEY.png" height="75%" width="100%" alt="ICMP traffic - private IP"/>

- **Ping a Website**  
  In the Windows VM, ping a website like www.google.com. Watch the traffic in Wireshark.  
  <img src="https://i.imgur.com/YduMvc7.png" height="75%" width="100%" alt="ICMP traffic - public IP"/>

- **Start a Non-Stop Ping**  
  In the Windows VM, start a non-stop ping to the Ubuntu VM by typing `ping [Ubuntu IP] -t` in the command prompt.  
  <img src="https://i.imgur.com/bihftKK.png" height="75%" width="100%" alt="ICMP traffic - perpetual ping"/>

- **Block ICMP Traffic**  
  In Azure, go to the Network Security Group (NSG) for your Ubuntu VM. Block incoming ICMP traffic. Watch the ICMP traffic stop in Wireshark and the command prompt in the Windows VM.  
  <img src="https://i.imgur.com/ovGk5dq.png" height="75%" width="100%" alt="ICMP traffic - perpetual ping"/>  
  <img src="https://i.imgur.com/NjuUANI.png" height="75%" width="100%" alt="ICMP traffic - ICMP denied"/>

- **Allow ICMP Traffic Again**  
  In the Ubuntu VM’s NSG, allow ICMP traffic again. In the Windows VM, watch the ICMP traffic start again in Wireshark and the command prompt. Stop the ping by pressing Ctrl+C.  
  <img src="https://i.imgur.com/nZbl2sA.png" height="75%" width="100%" alt="ICMP traffic - ICMP re-enabled"/>

---

### Step 3: Watch SSH Traffic
- In Wireshark, filter for SSH traffic only.
- In the Windows VM, open a command prompt and SSH into your Ubuntu VM using its private IP (type `ssh [username]@[Ubuntu IP]`). Run simple commands like `ls` or `pwd`. Watch the SSH traffic in Wireshark.
- Exit the SSH session by typing `exit` and pressing Enter.  
  <img src="https://i.imgur.com/6YEDJKu.png" height="75%" width="100%" alt="SSH traffic"/>

---

### Step 4: Watch DHCP Traffic
- In Wireshark, filter for DHCP traffic only.
- In the Windows VM, open a command prompt and type `ipconfig /renew` to get a new IP address. Watch the DHCP traffic in Wireshark.  
  <img src="https://i.imgur.com/mKyAHFr.png" height="75%" width="100%" alt="DHCP traffic"/>

---

### Step 5: Watch DNS Traffic
- In Wireshark, filter for DNS traffic only.
- In the Windows VM, open a command prompt and type `nslookup google.com` and `nslookup disney.com` to find their IP addresses. Watch the DNS traffic in Wireshark.  
  <img src="https://i.imgur.com/mYZ8CAK.png" height="75%" width="100%" alt="DNS traffic"/>

---

### Step 6: Watch RDP Traffic
- In Wireshark, filter for RDP traffic by typing `tcp.port==3389`.
- Notice the constant stream of traffic. This happens because RDP is always sending a live stream from one computer to another.  
  <img src="https://i.imgur.com/hNlhTVp.png" height="75%" width="100%" alt="RDP traffic"/>

---

### Step 7: Clean Up Your Azure Environment
- Close your Remote Desktop connection.
- In Azure, delete the Resource Group you created at the start.
- Check the bell notification in Azure to confirm the Resource Group is deleted. This prevents extra charges.
