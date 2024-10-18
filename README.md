# Monitoring Traffic
Tools used to monitor traffic during an engagement.


## TCPDump
Tcpdump is a powerful command-line utility used to capture and analyze network traffic on a Linux system. It is widely used by network administrators for troubleshooting and security testing. Despite its name, tcpdump can capture various types of traffic, including TCP, UDP, ARP, and ICMP

**Initial Usage**

    $ tcpdump -i eth0

**Monitor a specific IP address:**

    $ tcpdump host <Target_IP>

**Monitor ipv6 traffic:**

    $ tcpdump ip6

Target an IP Address to monitor the traffic that is going to or from the specified IP. 

    $ tcpdump -i eth0 -nn -s0 -v port 80

**Read/Write Captures to a .pcap file.**

    $ tcpdump tcp port 80 -w output.pcap -i eth0 

Example: Tcpdump for port 80 on interface eth0 outputs to file output.pcap.

## Wireshark
Wireshark is a network packet analyzer. A network packet analyzer presents captured packet data in as much detail as possible.

**Initial Usage:**

    $ wireshark &

**Import tcpdump file into Wireshark:**

    $ tcpdump -s 0 -i eth0 -w /Desktop/Wireshark/mycap.pcap

Begin with running a tcpdump and transferring it to a pcap file to import into WireShark.
Go to Capture, Options- and uncheck permiscuous. 

**Exclude Packets:** 

To remove specified ports from wireshark output go to the filter bar and enter:
      
    Filter: not(tcp.port==<port>) and not (tcp.port==<port>)
    not(udp.srcport==<port> and not udp.dstport==<port>)

**Exclude an IP:**

    Filter: ! (ip.addr == <Specified_IP>)

**Filter by port or service name:**

    Filter: telnet
  Right click on packet, select Follow TCP Stream and review packet.

**Search for Passwords:**

    1. In the Wireshark window, box, click Edit, "Find Packet".
    2. In the "Wireshark: Find Packet" box, click the String button. Enter a search string of secret, as shown below.
    3. In the "Search In" section, click "Packet bytes".
    4. Click Find.

**Search for HTTP Creds:**

    Filter: http.request.method==POST
Search for .login or /login in the Info Column

**Search for HTTP Requests:**

    Filter: Http.request 
or
    
    Filter: http.response.code == 200 

**Search for TCP Port:** 

    Filter: tcp.dstport == 23 

**Convert pcapng to pcap file:**

    Editcap <name.pcapng> <name.pcap>

**References:** 
- https://danielmiessler.com/p/tcpdump/
- https://www.tcpdump.org/
- https://www.wireshark.org/
- https://www.wireshark.org/docs/dfref/
