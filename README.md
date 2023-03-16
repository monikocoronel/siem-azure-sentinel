# siem

<p align="center">
<img src="https://i.imgur.com/6BNNyX9.png" 
</p>

<h1> Azure-Sentinel</h1>
This tutorial outlines having a virtual machine in Azure, exposing that machine to the internet by disabling its security and watching the geolocation of the would-be attackers get mapped out.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Windows 10

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Create virtual machine in Azure</h2>
<p>
<img src="https://i.imgur.com/n3sWYz0.png" height="80%" width="80%" 
</p>

<p>
<img src="https://i.imgur.com/1vPK6aD.png" height="80%" width="80%" 
</p>

-Remove inbound rule in network security group
- Create a new inbound rule that allows everything into the VM. This allows all traffic from the internet into the virtual machine. 

<h2>Create Logs Analytics workspace</h2>

<p>
<img src="https://i.imgur.com/A7okadU.png" height="80%" width="80%" 
</p>

- This allows us to ingest logs into the VM
- Will create our own custom log which shows the attackers geolocation
-SIEM (Azure Sentinel) will connect to this log/ workspace and will be able to display the geodata on the map

<h2>Connect Log Analytics to VM</h2>

<p>
<img src="https://i.imgur.com/9pBPxtK.png" height="80%" width="80%" 
</p>

<h2>Setup Azure Sentinel</h2>

<p>
<img src="https://i.imgur.com/Nv1SBEn.png" height="80%" width="80%" 
</p>

- This is our SIEM which allows us to visualisze the attack data

<h2>Observe Event viewer logs in VM</h2>

<p>
<img src="https://i.imgur.com/cHC3EvK.png" height="80%" width="80%" 
</p>

<h2>Turn off windows firewall in VM</h2>

<p>
<img src="https://i.imgur.com/7psGzTa.png" height="80%" width="80%" 
</p>

- when pinging the IP address of the VM, it shows as timed out due to the firewall being active

<p>
<img src="https://i.imgur.com/BUqSTMo.png" height="80%" width="80%" 
</p>

-Turn off the firewall state for the domain, public, and private profiles

<p>
<img src="https://i.imgur.com/QiZK4hA.png" height="80%" width="80%" 
</p>

- Now the ping works because echo requests are allowed

<h2>Run PowershellISE script to get data from attackers</h2>

- The script looks through the event viewer to see the failed log ins, it takes them out and sends the IP address to the API where it shows the country and geodata and creates a failed log on file

<p>
<img src="https://i.imgur.com/9qRgtCi.png" height="80%" width="80%" 
</p>

-Failed log in attempt shows latitutde, longitude etc

<h2>Create custom log in Log Analytics workspace to bring in our custom log with geodata</h2>

<p>
<img src="https://i.imgur.com/7Gshth7.png" height="80%" width="80%" 
</p>

<h2>Create Custom Fields/ Extract fields from raw  custom log data</h2>

<p>
<img src="https://i.imgur.com/tszoVx4.png" height="80%" width="80%" 
</p>

 -Extract the raw data so each piece has its own field e.g latitude, logitude etc.
  
<p>
<img src="https://i.imgur.com/DvNrx38.png" height="80%" width="80%" 
</p>

- Highlight the particular value e.g latitude and click extract
- Do this for latitude, longitude, destinationhost, source host, state, country, label, time stamp

<p>
<img src="https://i.imgur.com/6FMAIlY.png" height="80%" width="80%" 
</p>

- Custom fields created from custom log

<h2>Setup map in Sentinel with latitude, longitude etc.</h2>

<p>
<img src="https://i.imgur.com/4A98IK3.png" height="80%" width="80%" 
</p>

<h2>Check on map</h2>

<p>
<img src="https://i.imgur.com/hbmaQ49.png" height="80%" width="80%" 
</p>
