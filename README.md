<h1>Vulnerability Management Lab</h1>


<h2>Description</h2>
Demonstrate the difference between a credential and non-credential scan. Install deprecated software and run a scan and then remediate vulnerabilities.
<br />


<h2>Technologies Used</h2>

- <b>Nessus Essentials</b> 
- <b>VMware Workstation</b>



<h2>Lab walk-through:</h2>

<p align="center">
Create the Resources in Azure Portal. Add a rule to allow any traffic to the VM. Allowing any traffic in and outbound will let us ping the VM and allow others to see the VM and try to login: <br/>
<img src="https://imgur.com/ncN7v5I.png" height="80%" width="80%" alt="Microsoft Sentinel SIEM Lab"/>
<br />
<br />
Turn off the firewall in the VM. This leaves the VM open and easier to target. We want an easy target so that others are encouraged to try to login to the VM:  <br/>
<img src="https://imgur.com/B3e4bvM.png" height="80%" width="80%" alt="Microsoft Sentinel SIEM Lab"/>
<br />
<br />
I used a powershell <a href="https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1">script</a> from Josh Madakor's <a href="https://www.youtube.com/watch?v=RoZeVbbZ0o0&t=2452stutorial">YouTube tutorial</a> and added my own API key to his script. The API key is to an <a href="https://ipgeolocation.io/">IP Geolocation database</a>, which ties a location to an IP address. This script will grab Security event 4625 from the Event Viewer in the VM and log them in a "failed_rdp" file: <br/>
<img src="https://imgur.com/Th1gy1A.png" height="80%" width="80%" alt="Microsoft Sentinel SIEM Lab"/>
<br />
<br />
Run the script to see the failed logins grabbed from the Security Events. I failed 3 logins with a vfailtest user to test the script:  <br/>
<img src="https://imgur.com/kJqXdgl.png" height="80%" width="80%" alt="Microsoft Sentinel SIEM Lab"/>
<br />
<br />
The script automatically created a failed_rdp log because I didn't have one already:  <br/>
<img src="https://imgur.com/c9Dubra.png" height="80%" width="80%" alt="Microsoft Sentinel SIEM Lab"/>
<br />
<br />
Add a custom log to the Log Analytics Workspace in the Azure Portal. This sample log will help tune the raw data extraction later. Add the path to the failed_rdp log after adding this sample log:  <br/>
<img src="https://imgur.com/guqZe69.png" height="80%" width="80%" alt="Microsoft Sentinel SIEM Lab"/>
<br />
<br />
Run a query with the failed logins file path created in the last step. This will pull in the raw data from the failed_rdp log into Log Analytics workspace. We can extract the information we need from this raw data:  <br/>
<img src="https://imgur.com/MSF9Z1K.png" height="80%" width="80%" alt="Microsoft Sentinel SIEM Lab"/>
<br />
<br />
Extract fields from the raw data (latitude, longitude, country, etc.). Tune the extraction if necessary (data may not get extracted correctly), and then save the results. These saved results should allow for auto-extraction of future incoming raw data: <br/>
<img src="https://imgur.com/A9QRIYW.png" height="80%" width="80%" alt="Microsoft Sentinel SIEM Lab"/>
<br />
<br />
Create a workbook in Azure Sentinel. Add the same query from above and include the fields we created above to the query so that we can edit the map:  <br/>
<img src="https://imgur.com/PLnDIHk.png" height="80%" width="80%" alt="Microsoft Sentinel SIEM Lab"/>
<br />
<br />
Edit the map settings by choosing which fields will be represented in the visual map. You can test the latitude and longitude data points to see if the map will accurately display the data. If it doesn't, you can choose to display the data by country/region instead. You can also add a metrics label, which we used to show the event count, to track how many failed logins occured at specific data points:  <br/>
<img src="https://imgur.com/DuBaKlG.png" height="80%" width="80%" alt="Microsoft Sentinel SIEM Lab"/>
<br /> 
<br />
Apply the map settings and verify that the locations are accurately depicted:  <br/>
<img src="https://imgur.com/8SPs7zW.png" height="80%" width="80%" alt="Microsoft Sentinel SIEM Lab"/>
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
