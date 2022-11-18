<p align="center">
<img src="https://i.imgur.com/WX4Kjzt.png" height="80%" width="80%" alt="VPN logo"/>
</p>    
    
<h1>Failed RDP Attacks to Geolocation Information (SIEM Lab)</h1>

The Powershell script in this repository is responsible for parsing out Windows Event Log information for failed RDP attacks and using a third party API to collect geographic information about the attackers location.<br />

<h2>Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- PowerShell: Extract RDP failed logon logs from Windows Event Viewer

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)

<h2>High-Level Deployment of Operations</h2>

Operation 1

Generating your Virtual Machine within Microsoft Azure

1. Create a text file or note pad to keep track of your information.
2. Create a Virtual Machine (You can create a Resource Group when creating your VM).
3. Create Virtual Machine in a country (try your country or a country close, so your vm isn’t too slow).

4. When creating vm before you are completely finished, got to networking.

   a. Find Nic (Network Security Group) then you will create your own firewall.
   
   b. Click advanced option create new. Remove the default rule them add your own.
   
   c. Destination port for the rule will be *. The priority will be 100.

Operation 2

Create Log Analytics Workspace

5. When creating LAW (Log Analytics Workspace0 make sure to use same RG (Resource Group).

6. Head over to Microsoft Defender For Cloud to enable the abilty to gather logs. 

      a. Enable in environment settings and disable SQL severs.
      
      b. Tap Data collection underneath defender plan where you enabled settings, then click All Events. 
      
7. Connect log analytics workspace to VM (Virtual Machine).

      a. Click on your Law, below it will be an option that says VM.
      
      b. Click on the VM tab to connect your law to your VM.

Operation 3

Setting up Microsoft Sentinel 

8. In Microsoft sentinel connect your LAW.
9. Remote into VM’s public IP.
10. In your VM go to the start menu and type in Event Viewer (you can see the failed attempts).
11. Turn off firewall used cmd “wf.msc” .

12. Download custom security log exporter https://github.com/aaronrucker990/SIEM-LAB/blob/main/_LOG_EXPORTER.rtf

      a. Paste in Powershell ISE.
      
      b. Click on the VM tab to connect your law to your VM.
      
Sign up with https://ipgeolocation.io/ to get API to use for code. 

13. Add custom log to LAW.
14. Find logs from desktop and find logs from windows. 
15. Open note pad to paste logs from Event Viewer on your actual desktop. 
16. Then Use C:\ProgramData\failed_rdp.log to put in for collection path for custom log in law then press Enter. 

17. Right click on random log to Exact RAW data

      a. Highlight latitude then save exactration of raw data.
      
      b. Highlight longitude then save exactration of raw data (check longitude and latitude to ensure logs are correct. If they are off modify and highlight to train proper algorithm).
      
      c. Start breaking key names : username, state, destination source and saving exaction.
      
operation 4

Setting up Geo Map

18. In Microsoft Defender for cloud click on Workbooks. 
19. Edit workbooks and add query. 

20. Type command to find logs.

       a. 
       
FAILED_RDP_WITH_GEO_CL | summarize event_count=count() by sourcehost_CF, latitude_CF, longitude_CF, country_CF, label_CF, destinationhost_CF
| where destinationhost_CF != "samplehost"
| where sourcehost_CF !=

19. Once you have your log you can now pin point with your geo map.

<h1>Visual Deployment of Operations</h1>


<h2>Operation 1</h2>

<p>
<img src="https://i.imgur.com/qrASvaA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

As demonstrated in this visual you just want to make sure you are setting up your Honey Pot correctly, so it is open for (Brute Force RDP Attacks). 

</p>
<br />


<h2>Operation 2</h2>


<p>
<img src="https://i.imgur.com/YIxsr5d.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/imqEsNv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

We are still setting up the basics with our virtual machine, turning it into our Honey Pot, as demonstrated in the visual. What is now being implented is the merging of our logs to our vm, to keep track of our Failed Brute Force attempts in our event logger.

</p>
<br />

<h2>Operation 3</h2>


<p>
	
<img src= "https://i.imgur.com/if1giu3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src= "https://i.imgur.com/0SHQYlh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src= "https://imgur.com/a/McDR2pI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
	
<img src= "https://i.imgur.com/SNzChz2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>	
	
</p>
<p>
    
This is the operation has to be implemented very perice in order to for the SIEM Lab to become a success. When deploying the Powershell script be sure to Sign up with https://ipgeolocation.io/ to get your API Key. You have to have your own API in order for the API to work. 

</p>
<br />


<h2>Operation 4</h2>

<p>
<img src="https://i.imgur.com/UbWvEGh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
	
<img src="https://i.imgur.com/Adv7kKC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
	
<img src="https://i.imgur.com/nxmZQI5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
	


	
</p>
<p>

In this operation where I setup Microsoft Sentinel (SIEM) and connected it to a live virtual machine. You can see the live attacks (RDP Brute Force) from all around the world, demonstrated in the visual. The custom PowerShell script was used to look up the attackers Geolocation information and plot it on a Microsoft Sentinel Map!

</p>
<br />


<img src="https://i.imgur.com/5iqkRwr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

