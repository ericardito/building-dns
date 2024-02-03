<p align="center">
<img src="https://github.com/ColtonTrauCC/dns/assets/147654000/8efa60be-b00d-4932-9438-3a8640ff3cd5" height = 20% width = 20%/>
</p>

<h1 align = "center">Understanding & Building Intuition for DNS</h1>
This lab showcases the utilization and configuration of DNS. The Domain Name System serves as a naming database, facilitating the translation of internet domain names into corresponding IP addresses. It functions by mapping the user-friendly names used to locate websites to the IP addresses that computers use for the same purpose. Following configuration and installation, we will engage in exercises involving client and domain controller virtual machines to enhance our understanding of DNS.
<br />

<h2>Environments and Technologies Used</h2>
<ul>
  <li>Microsoft Azure (Virtual Machines/Compute)</li>
  <li>Remote Desktop</li>
  <li>Active Directory Domain Services</li>
  <li>Command Prompt</li>
</ul>

<br />

<h2>Operating Systems Used</h2>
<ul>
  <li>Windows Server 2022</li>
  <li>Windows 10 Pro (21H2)</li>
</ul>

<br />

<h2>DNS Exercises</h2>


<h3>A-Record Exercise</h3>

</ul>

<br />
The "A" in A Record represents address, signifying the most fundamental DNS record type. It specifies the IP address associated with a particular domain and exclusively holds IPv4 addresses.
</p>
Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin) and then Connect/log into Client-1 as an admin (mydomain\jane_admin)
<p>
From Client-1 try to ping “mainframe” notice that it fails
</p>
<img src="https://i.imgur.com/iNNW8lJ.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
To understand this process:
  
Initially, Client-1 examines its local cache for information about "mainframe." If no relevant data is found, it proceeds to check the Host File. Subsequently, Client-1 cehcks the DNS server linked to its network interface card, encountering failure. In this case, it requests DC-1 to provide the IP address of "mainframe." The DNS A Records in the file comprise entries such as DC-1.mydomain.com - 10.0.0.4 and Client-1.mydomain.com - 10.0.0.5. - Realizing it lacks information about the entity, and the DNS server is also unaware, Client-1 encounters an error message on the command prompt, indicating a ping failure due to the absence of an IP address for the intended target.
<p>

To create a DNS A Record go to the Domain Controller vm and open the DNS Manager. In the Server Manager Board go to the domain created within the Forward Lookup Zones tab (mydomain.com)
<p>
Right click on the page and create a New Host (A or AAA). Name the host mainframe and IP Address the same as domain controller. Then click "Add Host" and refresh the DNS server so it can update.
<p>
<img src="https://i.imgur.com/sQUfbky.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
In the Client vm on Command Prompt ping mainframe again. Observe that it works
  
<img src="https://i.imgur.com/z23YSDy.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
Perform nslookup
<p>
<img src="https://i.imgur.com/zzlcDQD.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
</p>

<br />

<h3>Local DNS Cache Exercise</h3>

<p>

Go back to DC-1 and change mainframe’s record address to 8.8.8.8
<p>

</p>
<img src="https://i.imgur.com/VJALvFR.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
<p>
Go back to Client-1 and ping “mainframe” again. Observe that it still pings the old address
<p>
<img src="https://i.imgur.com/CSTk9zQ.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
Flush the DNS cache (ipconfig /flushdns). Observe that the cache is empty (make sure command line is open as an admin)
<p>
<img src="https://i.imgur.com/yBa71iJ.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
Attempt to ping “mainframe” again. Observe the address of the new record is showing up
<p>
<img src="https://i.imgur.com/N1stIr2.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
</p>

<br />

<h3>CNAME Record Exercise</h3>

<p>

<p>
A canonical name (CNAME) record points from a domain to another domain, never to an IP Address.
<p>
Go back to DC-1 and create a CNAME record (new alias) that points the host “search” to “www.google.com” - To create a DNS A Record go to the Domain Controller vm and open the DNS Manager. In the Server Manager Board go to the domain created within the Forward Lookup Zones tab (mydomain.com)

Right click on the page and create a New Alias (CNAME). Name the alias search and refresh the DNS server so the new record can be updated
<p>
<img src="https://i.imgur.com/t91Q307.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
Let's engage in a DNS exercise involving A Records, Local DNS Cache, and CNAME to enhance our comprehension. Navigate to the client VM, initiate a ping search, and observe the resolution to Google, which is associated with its respective IP address.
<p>
<img src="https://i.imgur.com/qVN2hRw.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
Open microsoft edge and enter search.mydomain.com and observe the results of the CNAME record
<p>
<img src="https://i.imgur.com/LANAYT9.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
In the command prompt enter ipconfig /displaydns and notice theres too much cache. Enter ipconfig /flushdns to flush it out. Ping search again and enter ipconfig /flushdns. Then ipconfig /displaydns, observe the results
<p>
<img src="https://i.imgur.com/lXJ1Azr.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
This is the end of the lab
