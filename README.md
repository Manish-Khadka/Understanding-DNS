# Understanding DNS
In this lab, I demonstrate DNS in action
<p align="center">









</p>

This lab explores DNS and its practical applications. As a foundational concept in IT, DNS is widely covered in theoretical resources, but this lab focuses on configuring DNS records to see it in action.  <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Command Prompt

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)

<h2>Configuration Steps</h2>

<p>
  <img width="857" alt="pinging mainframe" src="https://github.com/user-attachments/assets/a10bf5de-cbfe-46be-80b2-a46b62283172" />

<img width="1137" alt="adding mainframe" src="https://github.com/user-attachments/assets/c400dbc3-c0fc-4ba2-b457-7a78637fc527" />
<img width="855" alt="ping mainframe again" src="https://github.com/user-attachments/assets/5f70b5fc-c698-491c-a91a-056b52f60385" />



</p>
<p>
Log in to the client as an admin and open the command prompt. Pinging "mainframe" will fail because there's no DNS record for it. To fix this, log in to the domain controller, open DNS Manager, and navigate to Forward Lookup Zones under your domain. Right-click and create a New Host (A or AAAA) record. Name it "mainframe" and assign the domain controller's IP address. Refresh the DNS server. Go back to the client and ping "mainframe" again—it should now resolve.







</p>
<br />

<p>
 <img width="794" alt="changong ip address" src="https://github.com/user-attachments/assets/9b7fedd0-e047-426e-921b-efe70852d416" />
 <img width="855" alt="ping mainframe again" src="https://github.com/user-attachments/assets/04c0162e-cc1a-44e9-9763-4af4b2681927" />
 <img width="858" alt="Screenshot 2024-12-02 at 3 33 43 PM" src="https://github.com/user-attachments/assets/cb20118f-5c59-4e48-a659-44e6dc29d2c9" />
 <img width="857" alt="Screenshot 2024-12-02 at 3 37 23 PM" src="https://github.com/user-attachments/assets/a7bf812d-6d80-489f-ab33-4f1def4c3a88" />



 

</p>
<p>
This exercise demonstrates how the DNS cache works. On the domain controller, I updated "mainframe's" record to use Google's IP address (8.8.8.8) and refreshed the DNS server. However, when pinging "mainframe" on the client, it still shows the old IP address. Running ipconfig /displaydns on the client reveals that the DNS cache has the old IP. To update it, clear the cache with ipconfig /flushdns. After this, pinging "mainframe" will show the new IP address.
</p>
<br />

<p>
<img width="819" alt="Screenshot 2024-12-02 at 3 41 35 PM" src="https://github.com/user-attachments/assets/31f0b771-42c5-4c22-9b76-b8d25d3fc951" />
<img width="855" alt="Screenshot 2024-12-02 at 3 42 12 PM" src="https://github.com/user-attachments/assets/5130b549-61fe-4daf-a7eb-edfd6c7e51c4" />


</p>
<p>
Let's create a CNAME record on the DNS server to point "search" to Google. In the DNS Manager, under Forward Lookup Zones, select your domain. Add a new CNAME record named "search" and set it to point to Google. Refresh the server to save the changes. On the client, using ping search or nslookup search will now show the CNAME record results.
</p>
<br />

<h2>Lessons Learned </h2>

This lab helped me understand how DNS works on a computer and within a network. I learned that DNS records can change, which may cause connectivity issues if the DNS cache still holds old records. The ipconfig /flushdns command clears the cache, allowing the system to update to the new records. At the start of the lab, when pinging "mainframe," the DNS cache is checked first. If no result is found, the host file is checked, followed by the DNS server. By creating a record on the DNS server, I ensured that "mainframe" could resolve. Additionally, I learned that a CNAME record maps an alias name to another domain, such as mapping "search" to Google.
