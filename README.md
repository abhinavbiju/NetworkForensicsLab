<h1>Network Forensics Lab</h1>

  <p>
    You’ve been hired to the Security Operations Center of the company <b>XYZ, LLC.</b> to help track down the employee behind some nefarious activity.  
    On <b>April 19th, 2023, at 12:50 PM</b>, an employee at XYZ, LLC. sent their deepest, darkest secrets to everyone within the company.  
    Or did they? This employee claims that someone else is impersonating them — your job is to hunt for who this rogue user is.
  </p>

  <h2>Description</h2>
  <p>
    Set up a home lab environment using <b>Kali Linux</b> within <b>VirtualBox</b> to practice network forensics and incident response.  
    Analyzed network traffic with <b>Wireshark</b>, identified a rogue user through DHCP and security logs, and successfully correlated the activity  
    to a specific host device — demonstrating proficiency in forensic investigation.
  </p>

  <h2>Tools Needed</h2>
  <ul>
    <li><b>Kali Linux</b></li>
    <li><b>Wireshark</b></li>
    <li><b>VirtualBox</b></li>
  </ul>

  <h2>Goals</h2>
  <ul>
    <li><b>Set up</b> a home lab environment with Kali Linux for network forensics.</li>
    <li><b>Use Wireshark</b> to analyze a .pcap file and identify suspicious activity.</li>
    <li><b>Correlate</b> the identified IP address with a host device using DHCP logs.</li>
    <li><b>Determine</b> the responsible user by analyzing security logs.</li>
  </ul>

  <h2>1 - Find the IP Address</h2>
  <p><b>Open up the .pcap file in Wireshark.</b></p>

  <img src="https://i.imgur.com/c2wPPFH.png" width="80%" alt="Wireshark view">

  <p class="note">
    Note: There are 60 packets, so use a display filter to narrow down relevant ones.  
    Hint: We are looking for an email, so use the filter <code>smtp</code>.
  </p>

  <img src="https://i.imgur.com/c3G9R7I.png" width="80%" alt="SMTP filter results">

  <p>
    With the applied filter, we should now see a refined list where all remaining packets use SMTP.  
    We are close — apply a more specific filter for the “FROM” field.
  </p>

  <img src="https://i.imgur.com/pp8FY0q.png" width="80%" alt="FROM filter results">

  <p>
    After filtering, we identify the sender’s email and the corresponding IP address: <b>10.10.1.4</b>.  
    This IP tells us where in the network the rogue user acted from.  
    By consulting the DHCP log, we can match this IP to a specific host device.
  </p>

  <h2>2 - Correlate to the Host Computer</h2>
  <p>
    <b>Use the DHCP log file</b> to match the found IP address. DHCP (Dynamic Host Configuration Protocol)  
    assigns IP addresses to devices on the network.
  </p>

  <ul>
    <li>Open the DHCP log.</li>
    <li>Identify the six events before 12:50 PM and check who owns IP <b>10.10.1.4</b>.</li>
    <li>Hint: Look at the event at <b>12:11:27 PM</b>.</li>
  </ul>

  <p>
    The event at 12:11:27 PM assigns IP 10.10.1.4 to the host <b>USER2</b>.  
    Now we know which computer the rogue user acted from.  
    Next, we’ll review the security log from this host to identify the logged-in employee.
  </p>

  <h2>3 - Analyze the Security Log</h2>
  <ul>
    <li>Open the Security Log with any word-processing tool (e.g., Word, WordPad, Pages, or TextEdit).</li>
    <li>The first two entries show a logon/logoff session on host <b>USER1</b> (Jane Doe).</li>
    <li>The last two entries show a logon/logoff session on host <b>USER2</b>.</li>
    <li>Find the corresponding user for USER2 — this will reveal our culprit.</li>
  </ul>

  <p>
    The user logged into USER2 during the time the emails were sent was <b>John Doe</b>.  
    The duration of John’s session perfectly overlaps with the time the sensitive emails were transmitted.  
    Case closed — we’ve identified the rogue user.
  </p>

</body>
</html>
