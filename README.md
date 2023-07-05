# yummyrecipesforme
In this project I was tasked with analyzing DNS and ICMP traffic in transit using data from a network protocol analyzer tool. To identify which network protocol was utilized in assessment of the incident. 

As a cybersecurity analyst working at a company that specializes in providing IT consultant services. Several customers contacted our company to report that they were not able to access the company website <www.yummyrecipesforme.com>, and saw the error “destination port unreachable” after waiting for the page to load. 

I was tasked with analyzing the situation and determining which network protocol was affected during this incident. To start, I visited the website and I also received the error “destination port unreachable.” Next, I loaded my network analyzer tool, tcpdump, and load the webpage again. This time, I received a lot of packets in my network analyzer. The analyzer shows that when one sends UDP packets and receives an ICMP response returned to host, the results contained an error message: “udp port 53 unreachable.” 

In the DNS and ICMP log, I found the following information:

![Screenshot 2023-07-05 103918](https://github.com/MarcoSantibanez/yummyrecipesforme/assets/138132151/51ac626d-5293-4b1a-8214-cacb0e5b3e71)



In the first two lines of the log file, I saw the initial outgoing request from my computer to the DNS server requesting the IP address of yummyrecipesforme .com. This request is sent in a UDP packet.

Next I found timestamps that indicate when the event happened. In the log, this is the first sequence of numbers displayed. For example: 13:24:32.192571. This displays the time 1:24 p.m., 32.192571 seconds.

The source and destination IP address is next. In the error log, this information is displayed as: 192.51.100.15.52444 > 203.0.113.2.domain. The IP address to the left of the greater than (>) symbol is the source address. In this example, the source is your computer’s IP address. The IP address to the right of the greater than (>) symbol is the destination IP address. In this case, it is the IP address for the DNS server: 203.0.113.2.domain

The second and third lines of the log show the response to your initial ICMP request packet. In this case, the ICMP 203.0.113.2 line is the start of the error message indicating that the ICMP packet was undeliverable to the port of the DNS server.

Next are the protocol and port number, which displays which protocol was used to handle communications and which port it was delivered to. In the error log, this appears as: udp port 53 unreachable. This means that the UDP protocol was used to request a domain name resolution using the address of the DNS server over port 53. Port 53, which aligns to the .domain extension in 203.0.113.2.domain, is a well-known port for DNS service. The word “unreachable” in the message indicates the message did not go through to the DNS server. My browser was not able to obtain the IP address for yummyrecipesforme.com, which it needs to access the website because no service was listening on the receiving DNS port as indicated by the ICMP error message “udp port 53 unreachable.”

The remaining lines in the log indicate that ICMP packets were sent two more times, but the same delivery error was received both times. 

Now that I had captured data packets using a network analyzer tool, it is my job to identify which network protocol and service were impacted by this incident. Then, I wrote a follow-up report. 

This incident, in the meantime, is being handled by security engineers after I and other analysts had reported the issue to our direct supervisor. 

Report: 

![Screenshot 2023-07-05 105742](https://github.com/MarcoSantibanez/yummyrecipesforme/assets/138132151/becbce25-467b-446d-b105-742d6a0ced53)

