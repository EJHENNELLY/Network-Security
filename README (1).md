# Cybersecurity Incident Report: Analyze Network Layer Communication
> Network layer communication.

> Please visit this [link](https://www.coursera.org/learn/networks-and-network-security?specialization=google-cybersecurity) for further information.

## Scenario

You are a cybersecurity analyst working at a company that specializes in providing IT consultant services. Several customers contacted your company to report that they were not able to access the company website www.yummyrecipesforme.com, and saw the error “destination port unreachable” after waiting for the page to load. 

You are tasked with analyzing the situation and determining which network protocol was affected during this incident. To start, you visit the website and you also receive the error “destination port unreachable.” Next, you load your network analyzer tool, tcpdump, and load the webpage again. This time, you receive a lot of packets in your network analyzer. The analyzer shows that when you send UDP packets and receive an ICMP response returned to your host, the results contain an error message: “udp port 53 unreachable.” 

![chrome_jd8ezyb2V1](https://github.com/Kwangsa19/Ketmanto-Cybersecurity-Portfolio/assets/135963482/7e41f4c7-d22c-4c64-8fb9-b73c85397403)

In the DNS and ICMP log, you find the following information:

1. The first two lines of the log file show the initial outgoing request from your computer to the DNS server requesting the IP address of yummyrecipesforme.com. This request is sent in a UDP packet.

2. The third and fourth lines of the log show the response to your UDP packet. In this case, the ICMP 203.0.113.2 line is the start of the error message indicating that the UDP packet was undeliverable to port 53 of the DNS server.

3. In front of each request and response, you find timestamps that indicate when the incident happened. In the log, this is the first sequence of numbers displayed: 13:24:32.192571. This means the time is 1:24 p.m., 32.192571 seconds.

4. After the timestamps, you will find the source and destination IP addresses. In the first line, where the UDP packet travels from your browser to the DNS server, this information is displayed as: 192.51.100.15 > 203.0.113.2.domain. The IP address to the left of the greater than (>) symbol is the source address, which in this example is your computer’s IP address. The IP address to the right of the greater than (>) symbol is the destination IP address. In this case, it is the IP address for the DNS server: 203.0.113.2.domain. For the ICMP error response, the source address is 203.0.113.2 and the destination is your computers IP address 192.51.100.15.

5. After the source and destination IP addresses, there can be a number of additional details like the protocol, port number of the source, and flags. In the first line of the error log, the query identification number appears as: 35084. The plus sign after the query identification number indicates there are flags associated with the UDP message. The "A?" indicates a flag associated with the DNS request for an A record, where an A record maps a domain name to an IP address. The third line displays the protocol of the response message to the browser: "ICMP," which is followed by an ICMP error message.

6. The error message, "udp port 53 unreachable" is mentioned in the last line. Port 53 is a port for DNS service. The word "unreachable" in the message indicates the UDP message requesting an IP address for the domain "www.yummyrecipesforme.com" did not go through to the DNS server because no service was listening on the receiving DNS port.

7. The remaining lines in the log indicate that ICMP packets were sent two more times, but the same delivery error was received both times. 
The remaining lines in the log indicate that ICMP packets were sent two more times, but the same delivery error was received both times. 

Now that you have captured data packets using a network analyzer tool, it is your job to identify which network protocol and service were impacted by this incident. Then, you will need to write a follow-up report. 

## Provide a Summary of the Problem Found in the DNS and ICMP Traffic Log

*DNS Server is down as a result of port 53 being unreachable. The ICMP packet request indicates that the packet has not been delivered to the port of DNS server successfully. 

*The UDP protocol reveals that: The UDP message requesting an IP address for the domain “www.yummyrecipesforme.com” did not go through to the DNS server

*This is based on the results of the network analysis, which show that the ICMP echo reply returned the error message: udp port 53 unreachable

*The port noted in the error message is used for: DNS server

*The most likely issue is: No service was listening on the receiving DNS port

## Explain Your Analysis of the Data and Provide at Least One Cause of the Incident

*Time incident occurred: 1:24 pm

*Explain how the IT team became aware of the incident: Customers of clients reported that they were not able to access the client website yummyrecipesforme, and saw the error message “destination port unreachable”

*Explain the actions taken by the IT department to investigate the incident: Attempted to visit the website. When that did not work, we used tcpdump to attempt to load the webpage again. Analyzer showed that udp port 53 unreachable. Reported the issue to my supervisor.

*Note key findings of the IT department's investigation (i.e., details related to the port affected, DNS server, etc.): Query identification number appears as: 35084. This is followed by a + sign to indicate that there are flags associated with the UDP message. “A?” indicates a flag associated with the DNS request for an A record, where an A record maps a domain name to an IP address. 

* Note a likely cause of the incident:
Determine whether port 53 is working or not. IF it’s fine, then check firewall. <br>
-Firewall: The ability to block network traffic on specific ports. Port blocking can be used to stop or prevent an attack. <br>
-DOS: There could be flood of information being sent to the network device to make it crash or unable to function. The hacker could disable dns server using DOS attack. Or someone within the organization might have disabled port 53 on firewalls. <br>
