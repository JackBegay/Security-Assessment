# Security Assessment Report

## Objective

For a course I had to keep an incident handler's journal to record all my findings after completing certain activities and the tools I used to complete it. I kept this to log my key takeaways, decription of incident, and what I did to accomplish it.

### Skills Learned

-Documenting a cybersecurity incident
-Analyzing a packet capture file
-Capturing a packet
-Investigating a suspicious file hash

### Tools Used

-Wireshark
-Tcpdump
-VirusTotal

## Steps

Date: February 23rd, 2024
Entry: #1
Description: For this entry I am documenting a cybersecurity incident that has occured at a health care company.
Tools used: None
The 5 W's: 
-Who: An organized ethical hacker group
-What: A security incident with ransomware
-Where: At a local health care company
-When: Today at 9 a.m.
Why: The group of unethical hackers used a phishing attack to be able to access the company's system. Once they were able to breach the system they launced their ransomware, encrypting crucial files. They seem to be motivated by financial gain only as they left a note explaining they demand a large amount of money in exchange for the decryption key to reverse the damage done.
Notes: 
-How will the health care company prevent a similar incident from happening again?
-Should health care company pay the large sum of money for the decryption key. 


Date: February 24th, 2025
Entry: #2
Description: Analyzing a packet capture file
Tools used: 
-Machine with linux running on it
-Wireshark
The 5 W's: None
Notes: For this entry I took a .pcap file and put it into Wireshark to see the contents inside. I used filtering to find specific IP addresses in the packet and details on the packets they were involved in. I was able to find source and destination IP addresses, protocol being used, and source and desination ports. I also filterd to select traffic based on MAC address to find specfic device's network interface cards sending and receiving packets on the network. For these specifc MAC addresses I searched for, I had to find the DNS query they were looking for, which were all for a Google Docs file.


Date: February 25th, 2025
Entry: #3
Description: Capturing my first packet
Tools used:
-Machine using Linux
-Tcpdump
The 5 W's: None
Notes: I used tcpdump instead of wireshark, but they both accomplish similar objectives like capturing, filtering, and analyzing network traffic. Using the command-line interface was a bit different than the graphical user interface on Wireshark and took a bit of adjusting. 

1.I first looked to see what interfaces were available using  sudo tcpdump -D  and found the Ethernet network interface was open to packet capture. 

2.I then filtered 5 packets from the eth0 interface with  sudo tcpdump -i eth0 -v -c5   with the -v added to display detailed packet information. I examined the packet output to find timestamp, protocol used, IP address, along with the detailed information like type of service, time to live, and any flags with each packet. 

3. Next I had to capture 7 packets on port 80 but this time I had to put save the captured data to a specfic file and ensure no IP addresses or port names were resolved during this process to not alert attackers. I used  sudo tcpdump -i eth0 -nn -c7 port 80 -w capture.pcap &   which captured the 7 packets through port 80 and ethernet interface, but this time added -nn to not resolve any IP addresses or ports to their names, as well as  -w capture.pcap  to move captured data and save it on this file.

4. Lastly I need to examine the packet header data from the capture file. I use a similar command to the last with       sudo tcpdump -nn -r capture.pcap -v   with the -r to read the file capture.pcap with detaled packet data and not still not looking up ports or IP addresses.


Date: February 25th, 2025
Entry: #4
Description: Investigate a suspicious file hash
Tools Used:
-VirusTotal
The 5 W's: 
Who: An unknown malicious actor
What: An suspicious email sent to an employee containing a malicious file that was opened with the SHA-256 file hash of 54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b
Where: An employee's computer at a financial consulting company
When: At 2 p.m. today, an alert was sent directly to the SOC of the organization once the IDS detected the file
Why: The employee who was sent the email opened and downloaded the malicious attachment
Notes:
Found the suspicious email to have multiple grammatical errors and a file attachment that needed the given password. Once the password was used, the file downloaded infected the employee's machine. After researching I found the file to be seen as malicious by 75% of security vendors using VirusTotal and labeled as a Trojan malware, so I recommended the incident be looked into further.


