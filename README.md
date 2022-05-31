<h1>Vulnerability Management Lab</h1>


<h2>Description</h2>
Demonstrate the difference between a credential and non-credential scan. Install deprecated software to view how a credentialed scan changes before and after deprecated software. Remediate vulnerabilities and another scan to view how many vulnerabilities are left. <br /> I wanted to operate within the vulnerability scanning and remediation parts of the vulnerability management lifecycle. 
<br />


<h2>Technologies Used</h2>

- <b>Nessus Essentials</b> 
- <b>VMware Workstation</b>

<h2>Lab walk-through:</h2>

<p align="center">
Open the VM and get the IP address. Turn off the Firewall so that you can try to ping the VM from your local machine. I start getting a reply after I turn off the firewall in the VM: 
<br/>
  <img src="https://imgur.com/Cn2KPqq.png" width="350" alt="Vulnerability Management Lab" hspace="20" />
  <img src="https://imgur.com/NXQTgS8.png" width="350" alt="Vulnerability Management Lab"/> 
<br />
<br />
 Setup a basic network scan in Nessus to see if I can get info information from the VM. Save and launch the scan: <br/>
<img src="https://imgur.com/1V1F3Jf.png" height="50%" width="50%" alt="Vulnerability Management Lab"/>
<br />
 <img src="https://imgur.com/Q18kB2K.png" height="80%" width="80%" alt="Vulnerability Management Lab"/>
<br />
<br />
Review the non-credential scan results when complete:  <br/>
<img src="https://imgur.com/vLjNTSj.png" height="50%" width="50%" alt="Vulnerability Management Lab"/>
<br />
<img src="https://imgur.com/GjK0nVY.png" height="70%" width="70%" alt="Vulnerability Management Lab"/>  
<br />
<br />
Edit the basic scan to run with Nessus/Tenable recommendations:
<br/>
- <b>Remote Registry enabled</b> <br />
  <img src="https://imgur.com/4K4flWQ.png" height="40%" width="40%" alt="Vulnerability Management Lab"/>
<br />
- <b>File and Printer Sharing on</b> <br />
  <img src="https://imgur.com/a44BgOC.png" height="50%" width="50%" alt="Vulnerability Management Lab"/>
<br />
- <b>Notifications disabled in User Account Control Settings</b> <br />
- <b>Add a policy in the Registry (for scanning a host that is not an admin). Documentation <a href="https://community.tenable.com/s/article/Scanning-with-non-default-Windows-Administrator-Account">here</a>.</b> <br />
<br />
  Now that the above changes are made in the VM, we can go into Nessus Essentials and setup the scan with Windows credentials. Doing this will allow the scanner to dig for more information and find more vulnerabilities:  <br/>
<img src="https://imgur.com/p4Wkonb.png" height="50%" width="50%" alt="Vulnerability Management Lab"/>

<br />
<br />
Look at the results of the credentialed scan. THere are more vulnerabilities listed now compared to when we ran a basic scan in the beginning of the lab:  <br/>
<img src="https://imgur.com/2Q2cDPw.png" height="80%" width="80%" alt="Vulnerability Management Lab"/>
<br />
<img src="https://imgur.com/RaxtoPF.png" height="80%" width="80%" alt="Vulnerability Management Lab"/>
<br />
<img src="https://imgur.com/BSpnFPc.png" height="80%" width="80%" alt="Vulnerability Management Lab"/>
<br />
<br />
I wanted to install a deprecated version of Firefox on my VM to see how that would affect the vulnerability scan. Once Firefox is installed, I am going to run the same scan to see how the results change:  <br/>
<img src="https://imgur.com/L6kGbKO.png" height="45%" width="45%" alt="Vulnerability Management Lab"/>
<br />
<br />
There are a lot more vulnerabilities on the VM after installing an old version of Firefox. If you look in the History tab, you can see that the amount of critical vulnerabilities has increased in the pie chart towards the right-side of the screen:  <br/>
<img src="https://imgur.com/ZNJBgO8.png" height="80%" width="80%" alt="Vulnerability Management Lab"/><br/>
<img src="https://imgur.com/jfQ7dgv.png" height="80%" width="80%" alt="Vulnerability Management Lab"/><br/>
<img src="https://imgur.com/DVXEaR3.png" height="80%" width="80%" alt="Vulnerability Management Lab"/><br/>


<br />
<br />
Start remediating vulnerabilities. A lot of critical vulnerabilities stem from Firefox and Windows 10 being out of date. Run Windows 10 updates and uninstall Firefox. I could have also updated Firefox, but since I installed a deprecated version of Firefox for the sake of this lab, I am just going to uninstall the software.<br/>
<img src="https://imgur.com/F4zV0ky.png" height="50%" width="50%" alt="Vulnerability Management Lab"/>

<br />
<br />
After updating Windows 10 and uninstalling Firefox, we can see that there are no more critical vulnerabilities:  <br/>
<img src="https://imgur.com/s60QJkt.png" height="80%" width="80%" alt="Vulnerability Management Lab"/> <br/><br/>
In the VPR Threat tab, we can see that the Firefox threat is no longer there. While here, we can click on the threat present and view more details. There is a "See Also" link that takes us to another site that gives more information on the threat as well:  <br/>
<img src="https://imgur.com/NuMAuKj.png" height="80%" width="80%" alt="Vulnerability Management Lab"/> <br/><br/>
The History tab here shows that as we remediated the vulnerabilities, there are less vulnerabilities present on the VM. Furthermore, there are no critical vulnerabilities:  <br/>
<img src="https://imgur.com/1iEDLRz.png" height="80%" width="80%" alt="Vulnerability Management Lab"/>

<br />
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
