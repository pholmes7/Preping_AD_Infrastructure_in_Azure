<p align="center">
<img src="https://i.imgur.com/Oa3gvSd.png" alt="Azure Virtual Network"/>
</p>

<h1> Preping AD Infrastructure in Azure </h1>
In this tutorial, we will be creating a domain controller and spinning up an Azure Vm to help us in simulating an Active Directory environment. This tutorial is just the 1st step in creating this lab. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Powershell

<h2>Operating Systems Used </h2>

- Windows 10
- Windows Server 2022

<h2>List of Prerequisites</h2>

- Create an Azure Account (free)


<h2>High-Level Steps</h2>

- STEP 1 - Create Resources
- STEP 2 - Edit Domain Controller 
- STEP 3 - Install Active Directory
- STEP 4 -
  
<h2>Instillation Steps</h2>
<h3> STEP 1 - Create Resources </h3>
 
 <p> We will start by creating our resource group. Navigate to the "Resource Group" page and click "Create."
   </p>

<p>
<img src="https://i.imgur.com/7VJe4H7.png"/>
</p>

 <p> For this lab, I am naming my resource group Active_Directory_Lab. </p>

 <p>
<img src="https://i.imgur.com/jWtdgTr.png"/>
</p>

 <p> After you have completed setting up the resource group, click "Create". </p>

<p>
<img src="https://i.imgur.com/jTrKBGU.png"/>
</p>


 <p> While the resource group is being created we will move on to creating the Virtual Network. Start by going to the "Virtual Networks" page and click "Create". </p>

<p>
<p>
<img src="https://i.imgur.com/a495ByQ.png"/>
</p>

  <p> For this lab, I am naming my virtual network Active_Directory_Vnet. </p>

<p>
<p>
<img src="https://i.imgur.com/K7eKVem.png"/>
</p>

 <p> After you have completed setting up the virtual network, click "Create". </p>

<p>
<img src="https://i.imgur.com/YAbcJRG.png"/>
</p>

 <p>You will know that the virtual network has been created once you see a page similar to this. </p>

<p>
<img src="https://i.imgur.com/isHrScF.png"/>
</p>

 <p>Now we will create our domain controller. We will start by going to the "Virtual Machines" page and clicking "Create". </p>

<p>
<img src="https://i.imgur.com/ZySk0R9.png"/>
</p>

 <p>We want to make sure that we have the right resource group selected. You can name the virtual machine what you would like. I named my machine DC-1. Make sure the availability zone you have selected is the same as your virtual network. We will also select "Windows Server 2022 Datacenter: Azure Edition - x64 Gen2" for our image. </p>

<p>
<img src="https://i.imgur.com/IsPpWc4.png"/>
</p>


<p> For image size, 2 vpus will do the job. Create a username and password for this virtual machine. Don't forget to check the box for the licensing agreement. </p>

<p>
<img src="https://i.imgur.com/tlBFach.png"/>
</p>

 <p> Next, we are going to select the networking tab at the top of the screen. We want to verify that we have the correct virtual network selected. We can click "Review + create".  </p>

<p>
<img src="https://i.imgur.com/GLJnStA.png"/>
</p>

 <p> You should see this screen once the virtual machine has been created.  </p>

<p>
<img src="https://i.imgur.com/ORbhSxD.png"/>
</p>

 <p>Now we will create our virtual machine for our client. We will start by going back to the "Virtual Machines" page and clicking "Create". </p>

<p>
<img src="https://i.imgur.com/ZySk0R9.png"/>
</p>

 <p>We want to make sure that we have the right resource group selected. You can name the virtual machine what you would like. I named my machine client-1. Make sure the availability zone you have selected is the same as your virtual network. We will also select "Windows 10 Pro, version 22H2 - x64 Gen2" for our image. </p>

<p>
<img src="https://i.imgur.com/b17rbiH.png"/>
</p>


<p> For image size, 2 vpus will do the job. Create a username and password for this virtual machine. Don't forget to check the box for the licensing agreement. </p>

<p>
<img src="https://i.imgur.com/Nw5SqGr.png"/>
</p>

 <p> Next, we are going to select the networking tab at the top of the screen. We want to verify that we have the correct virtual network selected. We can click "Review + create".  </p>

<p>
<img src="https://i.imgur.com/ersyuvQ.png"/>
</p>

 <p> You should see this screen once the virtual machine has been created.  </p>

<p>
<img src="https://i.imgur.com/TbsWul3.png"/>
</p>

 <p> Let's go back to the "virtual Machines" homepage. You should see both VMs there and they should be running  </p>

<p>
<img src="https://i.imgur.com/DWU0H06.png"/>
</p>


<h3> Step 2 - Edit Domain Controller Settings </h3>

 <p>In this step, we are going to be edit the Domain Controllers Virtual Network Interface Card (NIC) to be static. This is important because as we get into the lab, we will want the client to always to connect to the domain controller. If the domain controller's private IP is dynamic,c then there is a great chance that the IP address will change, making it hard for the client to connect successfully. We will start by clicking on our domain controller on our "Virtual Machines"page. </p>
 
<p>
<img src="https://i.imgur.com/meU9lFQ.png"/>
</p>

<p> After clicking on the domain controller, on the left sidebar, click on the drop-down menu for Networking and select Network Settings. On this page,e you can see the public IP, private IP, network interface (green icon), and other things. Click on the network interface that has the green icon. </p>

<p>
<img src="https://i.imgur.com/o1FdReH.png"/>
</p>

<p> When can now see that the private IP for our domain controller is dynamic. We have to change it to static. Click on ipconfig1. </p>

<p>
<img src="https://i.imgur.com/o1FdReH.png"/>
</p>

<p> Underneath "Private IP address settings select static for the allocation. Then hit save. </p>

<p>
<img src="https://i.imgur.com/woxCVxa.png"/>
</p>


<p> Our next step will be to disable the firewall of the domain controller so that the client vm will be able to connect with no problems. This is not recommended in real environments as it will leave your machine open to attack. We will start by rdp'ing into the domain controller vm. </p>

<p>
<img src="https://i.imgur.com/7CWsbQk.png"
</p>

<p>
<img src="https://i.imgur.com/mCho8ZR.png"
</p>

<p> Once you have successfully rdp'ed into the machine you should see Windows Server Manager. While it is not pictured here, you can check by right-clicking the start menu and selecting system. You should see underneath Windows specification next to edition windows server 2022 Datacenter Azure edition. If you dont see this you have messed up somewhere.  </p>


<p> Now we will edit the firewall by right-clicking the start menu and selecting run. Type in wf.msc   </p>
<p>
<img src="https://i.imgur.com/iCI3Hjx.png"
</p>

<p> On the Domain Profile, select Off for the Firewall state. On the Public Profile, select Off for the firewall state.    </p>

<p>
<img src="https://i.imgur.com/ObmOPRd.png"
</p>
<p>
<img src="https://i.imgur.com/7t9NeEK.png"
</p>

<p> After you have saved your changes by clicking Apply. The screen should look similar to the picture below.  </p>

<p>
<img src="https://i.imgur.com/eC2C6OW.png"
</p>

<p> ------------- Start Here ----------- </p>
<p>
Click the "Create -> Azure Virtual Machine" button to begin creating the VM. Create a new Resource Group for the VM. Name your VM. Choose an availability zone that allows you to create an instance. I choose Zone 2. See the screenshot below.  
</p>

<p>
<img src="https://i.imgur.com/wUW2Kgi.png"/>
</p>

<p>
  Choose a Windows 10 version as your Image. For the size, 2 vcpus and 4GB will do.
</p>

<p>
<img src="https://i.imgur.com/IscBjnC.png"/>
</p>

<p>
  For the Username and Password you can create your custom information, just record it personally. Then select “Review and Create”, once it passes validation select “Create” at the bottom.
</p>

<p>
<img src="https://i.imgur.com/Z5dmmm6.png"/>
</p>
<br />

<h3> Step 3 - Locating IP Through VM </h3>
<p> Now that we have set up the Virtual Machine we will be connecting to it using the application “Remote Desktop Connection” or RDP. We will input the IP address for the VM that was assigned after we created the VM (see 1st screenshot below) and then input the credentials we set when creating the VM. (see 2nd screenshot) </p>

<p>
<img src="https://i.imgur.com/GYz4vSd.png"/>
</p>

<p>
<img src="https://i.imgur.com/IZvQ9g7.png"/>
</p>


<p>Once logged in, we will open the web browser and again look up www.whatismyipaddress.com. Take note of the IP address of the VM. This is a different IP from your local machine's IP. </p>

<p>
<img src="https://i.imgur.com/gNYpFFR.png"/>
</p>

<h3> Step 4 - Setup VPN </h3>

<p> Using the local computer go to protonvpn.com and create a free account.  Once you are logged into your newly created account, copy the URL from the Proton VPN website and then paste the URL to the VM web browser.</p>
<p> You will have to log into Proton VPN again.
 <p>
<img src="https://i.imgur.com/EbNLNaY.png"/>
</p>

<p> Navigate to Downloads. Select Download for Windowns 11/10 (x64). Begin the Download process. </p>
 <p>
<img src="https://i.imgur.com/MQAVEDm.png"/>
 </p>
  <p>
<img src=" https://i.imgur.com/Mh4u89R.png"/>
 </p>

<p> After successfully downloading Proton VPN you will be greeted with a "Welcome on Board" screen. </p>

 <p>
<img src="https://i.imgur.com/fEoVBPU.png"/>
 </p>

<h3> Step 5 - Connecting to VPN Through VM </h3>

<p> After exiting the "Welcome on Board" message. Click on the button that says, "Quick Connect" on the left-hand side. Proton VPN will then assign a new IP for your machine. </p>
 <p>
<img src="https://i.imgur.com/3e7AyBT.png"/>
 </p>

<h3> STEP 6 - Locating IP Through VPN </h3>
 <p> Now we will open the web browser and again look up www.whatismyipaddress.com. Take note of the new IP address of the VM. This is a different IP from your local machine's IP and the original IP address of the VM. </p>
  <p>
<img src="https://i.imgur.com/RvibhMx.png">
 </p>

 <h2>Conclusion</h2>
<p> Congrats! You have successfully used a VPN within a VM. This lab highlights the power a VPN has in terms of privacy and how it affects IP addresses. </p>
