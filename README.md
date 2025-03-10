<p align="center">
<img src="https://i.imgur.com/Oa3gvSd.png" alt="Azure Virtual Network"/>
</p>

<h1> Prepping AD Infrastructure in Azure </h1>
In this tutorial, we will be creating a domain controller and spinning up an Azure VM to help us in simulating an Active Directory environment. This tutorial is just the 1st step in creating this lab. <br />

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
- STEP 3 - Edit Client Configuration
  
  
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


 <p> While the resource group is being created, we will move on to creating the Virtual Network. Start by going to the "Virtual Networks" page and clicking "Create". </p>

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

 <p>Now, we will create our domain controller. We will start by going to the "Virtual Machines" page and clicking "Create". </p>

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

 <p>Now, we will create our virtual machine for our client. We will start by going back to the "Virtual Machines" page and clicking "Create". </p>

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

 <p> Let's go back to the "Virtual Machines" homepage. You should see both VMs there, and they should be running  </p>

<p>
<img src="https://i.imgur.com/DWU0H06.png"/>
</p>


<h3> Step 2 - Edit Domain Controller Settings </h3>

 <p>In this step, we are going to edit the Domain Controllers Virtual Network Interface Card (NIC) to be static. This is important because as we get into the lab, we will want the client to always to connect to the domain controller. If the domain controller's private IP is dynamic, then there is a great chance that the IP address will change, making it hard for the client to connect successfully. We will start by clicking on our domain controller on our "Virtual Machines" page. </p>
 
<p>
<img src="https://i.imgur.com/meU9lFQ.png"/>
</p>

<p> After clicking on the domain controller, on the left sidebar, click on the drop-down menu for Networking and select Network Settings. On this page, you can see the public IP, private IP, network interface (green icon), and other things. Click on the network interface that has the green icon. </p>

<p>
<img src="https://i.imgur.com/o1FdReH.png"/>
</p>

<p> We can now see that the private IP for our domain controller is dynamic. We have to change it to static. Click on ipconfig1. </p>

<p>
<img src="https://i.imgur.com/o1FdReH.png"/>
</p>

<p> Underneath "Private IP address settings select static for the allocation. Then hit save. </p>

<p>
<img src="https://i.imgur.com/woxCVxa.png"/>
</p>


<p> Our next step will be to disable the firewall of the domain controller so that the client vm will be able to connect with no problems. This is not recommended in real environments as it will leave your machine open to attack. We will start by RDPing into the domain controller VM. </p>

<p>
<img src="https://i.imgur.com/7CWsbQk.png"
</p>

<p>
<img src="https://i.imgur.com/mCho8ZR.png"
</p>

<p> Once you have successfully RDP'ed into the machine, you should see Windows Server Manager. While it is not pictured here, you can check by right-clicking the start menu and selecting system. You should see underneath Windows specification next to edition windows server 2022 Datacenter Azure edition. If you dont see this, you have messed up somewhere.  </p>


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

<h3> Step 3 - Edit Client Configuration </h3>

<p> Now that we have disabled the domain controller's firewall, we need to edit our client to automatically use the domain controller as its DNS server. We will start by locating the private IP address of the domain controller. You can get there by going to the Virtual Machines page and clicking on your domain controller VM. I have highlighted my private IP in the picture below. </p>

<p>
<img src="https://i.imgur.com/IXALsLf.png"
</p>

<p> With the domain controller's private IP, we can navigate to our client VM.  On the left sidebar, click on the drop-down menu for Networking and select Network Settings. On this page, you can see the public IP, private IP, network interface (green icon), and other things. Click on the network interface that has the green icon.  </p>

<p>
<img src="https://i.imgur.com/TcSzn97.png"
</p>

<p> Select DNS servers from the life sidebar. Click the custom option and enter the private IP address you got from your domain controller. This means that whenever we look something up on the internet, it will use the domain controller as the DNS server. Make sure you save your settings. </p>

<p>
<img src="https://i.imgur.com/L1UUYCk.pngg"
</p>


<p> To make sure the changes are saved, restart your client machine.  </p>

<p>
<img src="https://i.imgur.com/0EcPJ0O.png"
</p>


<p> We will now rdp into our client machine. Grab the public IP for your client to log into it.    </p>

<p>
<img src="https://i.imgur.com/ewiaEw5.png"
</p>

<p> Now, we are going to ping the domain controller's private IP address. Type Powershell in the search bar of your machine. </p>

<p>
<img src="https://i.imgur.com/HMaRghj.png"
</p>

<p> Type "ping" and "domain controller private IP". You should get a similar screen below. If you get an error, your domain controller and client could be in different virtual networks, or the domain controller's firewall could still be on. </p>

<p>
<img src="https://i.imgur.com/EH4JqRB.png"
</p>

<p> Type "ipconfig /all". We are looking to make sure the domain controller's private IP address is showing up as the DNS Server for the client. Your screen should look like the one below. </p>

<p>
<img src="https://i.imgur.com/9BvSX75.png"
</p>
  

 <h2>Conclusion</h2>
<p> Congrats! You have successfully set up the domain controller and client vm for this active directory lab. Look for part two titled ".....". </p>
