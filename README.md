

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
- STEP 2 - Verify connectivity between VM and Domain Controller
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
<p> ------------- Start Here ----------- </p>
<h3> Step 2 - Set Up VM Using Azure</h3>
 <p>Go to www.portal.azure.com and find Virtual Machines.   See the screenshot below.</p>
</p>
<p>
<img src="https://i.imgur.com/DRGwczk.png"/>
</p>

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
