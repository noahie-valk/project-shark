# Introduction

Lately I've been coming to understand the basics of networking through learning how to use [Wireshark](https://wireshark.org) and it's definitely a complicated process. I think I have the basics down, though, at least regarding packet capturing and interpretation. My next step, though, is to try and put my knowledge to practice through some kind of application either through a free exercise on [TryHackMe](https://tryhackme.com) or through participating in a CTF competition. 

I will publish my notes that I've taken on how to use Wireshark and general best practices for packet capturing. 

## Packet Analysis Basics

**Packet analysis**—sometimes called protocol analysis or packet sniffing—is all about capturing, inspecting, and understanding the data packets zipping around a network. These packets carry key details like source and destination IP addresses, protocols being used, and the actual data being transmitted. By breaking these packets down, network administrators and cybersecurity pros can uncover valuable insights about how networks behave and perform.

Why does packet analysis matter so much in networking and cybersecurity? In networking, it’s your go-to for diagnosing problems like latency, packet loss, and configuration hiccups. When you understand how data flows, you can fine-tune network performance, fix connectivity issues, and make sure everything runs smoothly. On the cybersecurity front, packet analysis is critical for spotting malicious activity—things like unauthorized access, data breaches, or malware communications. By keeping a close eye on network traffic, security experts can detect anomalies, investigate incidents, and put safeguards in place to protect sensitive information.

Enter **Wireshark**—one of the most popular tools for packet analysis. This open-source network protocol analyzer lets you capture and explore network traffic in real-time. Its intuitive interface and powerful filters make it a breeze to dissect even the most complex protocols. Whether you're troubleshooting network glitches, diving into protocol behavior, or tracking down security threats, Wireshark equips you with everything you need to get the job done right.

## Setting Up Wireshark

1. **Update System Packages**  
    Open the terminal and run the following command to ensure all packages are up to date:
    
    ```bash
    sudo apt update && sudo apt upgrade -y
    ```
    
2. **Install Wireshark**  
    Install Wireshark by running the following command:
    
    ```bash
    sudo apt install wireshark -y
    ```
    
3. **Configure Permissions**  
    During installation, a prompt may appear asking if non-superusers should be allowed to capture packets. Select **Yes** to grant this permission.
    
4. **Add the User to the Wireshark Group**  
    To enable packet capturing without root privileges, add the user to the Wireshark group:
    
    ```bash
    sudo usermod -aG wireshark $USER
    ```
    
    After executing this command, it is necessary to log out and log back in for the changes to take effect.
    
5. **Verify the Installation**  
    Confirm that Wireshark is installed correctly by running:
    
    ```bash
    wireshark --version
    ```
    
6. **Launch Wireshark**  
    Wireshark can be started from the terminal with the following command:
    
    ```bash
    wireshark
    ```
    
    Alternatively, it can be launched from the applications menu.
    
7. **Test Packet Capturing**  
    Select a network interface and begin capturing packets to verify that everything is functioning properly.
    
8. **Optional: Install TShark (Command-Line Version)**  
    For those who prefer command-line tools, TShark, the terminal-based version of Wireshark, can be installed with:
    
    ```bash
    sudo apt install tshark -y
    ```
    
    Verify the TShark installation by running:
    
    ```bash
    tshark --version
    ```

## Capturing Network Traffic

1. **Selecting the Correct Network Interface**
    - Open Wireshark and navigate to the home screen where all available network interfaces are listed.
    - Identify the correct network interface based on the active connection (e.g., Ethernet, Wi-Fi). Interfaces with active traffic are typically highlighted with a live graph.
    - If unsure, disable and enable the network connection to observe which interface shows activity.
2. **Starting and Stopping a Packet Capture**
    - Click on the desired network interface to start capturing packets.
    - Wireshark will begin displaying real-time network traffic.
    - To stop capturing, click the red square "Stop" button in the toolbar.
    - It’s recommended to capture only the necessary amount of data to avoid large, unmanageable files.
3. **Saving and Exporting Capture Files for Later Analysis**
    - After stopping the capture, go to **File > Save As** to save the capture file in the default `.pcapng` format.
    - To export specific packets, use **File > Export Specified Packets**, applying filters to narrow down the data.
    - Saved capture files can be reopened later for detailed analysis by selecting **File > Open** and navigating to the saved file.
## Filtering and Navigating Packets

1. **Using Display Filters to Narrow Down Traffic**
    - Disp
    - lay filters allow users to focus on specific types of network traffic by filtering out unrelated packets.
    - To apply a display filter, enter the desired filter syntax in the filter bar at the top of the Wireshark interface and press Enter.
    - Common display filters include:
        - `http` – Displays only HTTP traffic.
        - `dns` – Shows DNS queries and responses.
        - `ip.addr == 192.168.1.1` – Filters traffic to or from a specific IP address.
        - `tcp.port == 80` – Displays traffic on a specific port (in this case, HTTP on port 80).
    - Filters can be combined using logical operators, such as `and`, `or`, and `not`. For example: `http and ip.addr == 192.168.1.1`.
2. **Applying Capture Filters Before Starting the Capture**
    - Capture filters limit the traffic that Wireshark collects, reducing the amount of data to analyze.
    - Unlike display filters, capture filters must be set before starting the packet capture.
    - To apply a capture filter, click on the interface options before starting the capture and enter the desired filter syntax.
    - Common capture filters include:
        - `port 80` – Captures only HTTP traffic.
        - `host 192.168.1.1` – Captures traffic to or from a specific IP address.
        - `net 192.168.1.0/24` – Captures traffic within a specific subnet.
        - `icmp` – Captures only ICMP (ping) traffic.
3. **Understanding the Packet List, Details, and Bytes Panes**
    - **Packet List Pane:** Displays a summary of all captured packets, including columns like No., Time, Source, Destination, Protocol, and Info.
        - Click on any packet to view more details.
    - **Packet Details Pane:** Shows a hierarchical breakdown of the selected packet, organized by protocol layers.
        - Expand or collapse each section to inspect specific protocol fields.
    - **Packet Bytes Pane:** Displays the raw data of the selected packet in both hexadecimal and ASCII formats.
        - Useful for low-level analysis and understanding the exact contents of the packet.

## Analyzing Different Protocols

1. **Identifying Common Protocols (TCP, UDP, ICMP, etc.)**
    - Wireshark captures a wide variety of network protocols, each serving different purposes.
    - **TCP (Transmission Control Protocol):** Ensures reliable data transmission with error checking and acknowledgment features.
    - **UDP (User Datagram Protocol):** Provides faster, connectionless communication without error checking, often used in streaming.
    - **ICMP (Internet Control Message Protocol):** Used for diagnostic purposes like ping tests and network troubleshooting.
    - To filter specific protocols, use display filters like:
        - `tcp` – Displays only TCP packets.
        - `udp` – Shows only UDP packets.
        - `icmp` – Filters for ICMP traffic.
2. **Analyzing HTTP Traffic: Requests and Responses**
    - HTTP (Hypertext Transfer Protocol) is the foundation of data communication on the web.
    - Use the display filter `http` to isolate HTTP packets.
    - Examine **HTTP Requests** (e.g., GET, POST) and **Responses** (e.g., status codes like 200 OK, 404 Not Found).
    - Inspect headers to analyze cookies, user agents, and other metadata.
    - To focus on a specific website’s traffic, use:
        
        ```
        http.host == "example.com"
        ```
        
3. **Investigating DNS Queries and Responses**
    - DNS (Domain Name System) translates human-readable domain names into IP addresses.
    - Use the display filter `dns` to view DNS traffic.
    - Analyze **DNS Queries** to see which domains are being requested.
    - Review **DNS Responses** to identify resolved IP addresses.
    - Identify any unusual or suspicious domains that may indicate malicious activity.

## Deep Dive into Packet Structure

1. **Breaking Down the OSI Model Layers**
    - The OSI (Open Systems Interconnection) model is a conceptual framework that standardizes the functions of a network into seven distinct layers:
        - **Layer 1 - Physical:** Deals with the hardware transmission of raw data bits (e.g., cables, switches).
        - **Layer 2 - Data Link:** Manages node-to-node data transfer and error detection (e.g., Ethernet frames).
        - **Layer 3 - Network:** Handles routing and forwarding of packets (e.g., IP addresses).
        - **Layer 4 - Transport:** Ensures reliable data transfer (e.g., TCP, UDP).
        - **Layer 5 - Session:** Manages sessions between applications.
        - **Layer 6 - Presentation:** Translates data formats (e.g., encryption, compression).
        - **Layer 7 - Application:** Provides network services to end-users (e.g., HTTP, DNS).
    - In Wireshark, packets are dissected according to these layers, allowing users to analyze data at each level.
2. **Examining Ethernet Frames, IP Packets, and TCP Segments**
    - **Ethernet Frames (Layer 2):**
        - Contain MAC addresses for source and destination devices.
        - Include an EtherType field to indicate the protocol used in the payload (e.g., IPv4, IPv6).
    - **IP Packets (Layer 3):**
        - Contain source and destination IP addresses.
        - Include a header with fields like Time-to-Live (TTL) and Protocol Type.
        - Fragmentation fields manage packet splitting and reassembly.
    - **TCP Segments (Layer 4):**
        - Contain source and destination port numbers.
        - Include sequence and acknowledgment numbers to ensure reliable data transfer.
        - Have control flags like SYN, ACK, FIN, and RST to manage connection states.
3. **Understanding Flags, Sequence Numbers, and Acknowledgments**
    - **Flags:** Control bits in the TCP header that manage the state of connections.
        - **SYN:** Initiates a connection.
        - **ACK:** Acknowledges receipt of data.
        - **FIN:** Indicates the end of data transmission.
        - **RST:** Resets a connection.
    - **Sequence Numbers:** Track the order of packets, ensuring data is reassembled correctly on the receiving end.
    - **Acknowledgment Numbers:** Confirm receipt of packets, facilitating reliable communication between devices.
   
## Identifying Anomalies and Issues

1. **Spotting Retransmissions, Duplicates, and Packet Loss**
    - **Retransmissions:** Occurs when a packet is lost or corrupted, prompting the sender to resend it.
        - Use the display filter `tcp.analysis.retransmission` to identify retransmitted packets.
        - High retransmission rates may indicate network congestion or hardware issues.
    - **Duplicate Packets:** Result from the same packet being received multiple times.
        - Filter for duplicates with `tcp.analysis.duplicate_ack`.
        - Excessive duplicates can point to misconfigured devices or faulty network paths.
    - **Packet Loss:** Happens when packets fail to reach their destination.
        - Detect packet loss by observing gaps in sequence numbers or using Wireshark’s built-in TCP analysis tools.
        - Consistent packet loss could suggest issues with network reliability.
5. **Detecting Unusual Traffic Patterns**
    - **Unexpected Protocols:** Look for protocols that shouldn’t be present in the network environment.
        - Apply filters like `!(tcp or udp or icmp)` to highlight unusual protocols.
    - **High Traffic Volume:** Sudden spikes in traffic may indicate problems like network loops or denial-of-service (DoS) attacks.
        - Use Wireshark’s I/O Graphs (under **Statistics > I/O Graphs**) to visualize traffic volume over time.
    - **Frequent Connection Attempts:** Repeated connection attempts to specific ports may suggest port scanning activities.
        - Filter using `tcp.flags.syn == 1 and tcp.flags.ack == 0` to see initial connection attempts.
6. **Recognizing Potential Security Threats**
    - **Suspicious IP Addresses:** Identify traffic from known malicious IP addresses.
        - Use filters like `ip.src == x.x.x.x` or `ip.dst == x.x.x.x` to track specific IPs.
        - Cross-reference IPs with threat intelligence databases.
    - **Unencrypted Sensitive Data:** Detect unencrypted transmission of sensitive information.
        - Filter for plaintext protocols like `http`, `ftp`, or `telnet`.
        - Inspect packet contents in the Packet Bytes Pane to spot exposed credentials or data.
    - **Anomalous DNS Requests:** Look for DNS queries to suspicious domains, which could indicate malware communication.
        - Use the display filter `dns` and analyze domain names for irregular patterns.

## Documenting and Reporting Findings

1. **Creating Detailed Reports of Analysis**
    - Clearly define the purpose of the analysis and what was investigated.
    - Include key details such as network topology, capture environment, and time of capture.
    - Structure reports in a logical manner, separating sections for different types of findings.
    - Use precise language to describe observations without speculation.
2. **Highlighting Key Insights and Anomalies**
    - Summarize significant findings with a focus on patterns, anomalies, and irregularities.
    - Provide context for detected anomalies, explaining their potential impact on network performance or security.
    - Compare normal and abnormal network behavior to illustrate deviations.
    - Include recommendations based on findings to guide network administrators or security teams.
3. **Using Screenshots and Annotations in Reports**
    - Capture key Wireshark screenshots to visually support findings.
    - Annotate important sections within the packet capture, such as flags, headers, or payload data.
    - Highlight relevant fields in packet details and mark timestamps for reference.
    - Ensure screenshots are high-quality and include necessary descriptions for clarity.

## Best Practices for Packet Analysis

1. **Ethical Considerations and Legal Compliance**
    - Always obtain proper authorization before capturing network traffic.
    - Be aware of privacy laws and regulations related to packet analysis.
    - Avoid capturing or storing sensitive data unless explicitly required and authorized.
    - Adhere to organizational policies and industry best practices when performing packet captures.
2. **Tips for Efficient and Effective Packet Analysis**
    - Use display and capture filters to focus on relevant traffic and reduce noise.
    - Familiarize yourself with common network protocols to interpret packet data effectively.
    - Save and document packet captures for future reference and troubleshooting.
    - Utilize Wireshark’s built-in tools, such as protocol analyzers and statistics, to speed up analysis.
    - Regularly update Wireshark and associated libraries to maintain compatibility with modern protocols.
3. **Continuous Learning and Staying Updated with Network Protocols**
    - Follow networking and cybersecurity forums, blogs, and publications to stay informed on emerging threats and technologies.
    - Participate in hands-on labs, capture-the-flag (CTF) events, and network security competitions.
    - Experiment with different packet capture scenarios to expand practical knowledge.
    - Engage in professional training courses or certifications related to network security and analysis.

# Conclusion

Thanks for reading! Hopefully you've learned something along with me. In other news, check out my [personal website](https://noahie.neocities.org). 
