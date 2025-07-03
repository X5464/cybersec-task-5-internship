Capturing and Analyzing Network Traffic with Wireshark (macOS)

1. Safely download and install Wireshark

Go to the official Wireshark website (https://www.wireshark.org) and download the macOS installer (a signed “.dmg” file) ￼. Do not download from unknown sources. Open the downloaded disk image and drag the Wireshark app into your /Applications folder ￼. After copying, launch Wireshark. The installer may prompt you to install the ChmodBPF helper (a small service) – allow this so Wireshark can capture packets ￼. (If needed, you can also install via Homebrew:

brew install --cask wireshark

which will similarly install Wireshark and its capture helper.)

2. Choose the correct network interface

In Wireshark, click the Capture Options button (the shark-fin or gear icon). A list of available interfaces appears. Select the one that is active on your Mac. For example, if you are connected via Wi-Fi, the interface is usually named “Wi-Fi (en0)” on macOS ￼. If using Ethernet, it might be “en1” or similar. You can look at the live packet count next to each interface – the one with growing packet numbers is your active interface ￼. Once you’ve picked the correct interface, click Start to begin capturing live packets ￼.

3. Generate live network traffic

With capture running, create network activity to record. Open a web browser (e.g. Safari or Chrome) and visit a few websites (such as http://example.com) – this generates HTTP and DNS traffic as your Mac resolves names and loads pages ￼. Also open the Terminal and use commands like ping example.com to send ICMP echo requests (and DNS queries) ￼. You can browse multiple sites or let a video stream run briefly. After 30–60 seconds of activity, return to Wireshark and click the red Stop button. You should now see captured packets filling the top pane.

4. Apply protocol filters in Wireshark

Use Wireshark’s Display Filter field (at the top of the window) to focus on specific protocols. To filter by protocol, simply type its name and press Enter ￼. For example:
	•	Enter http to display only HTTP packets (web traffic) ￼.
	•	Enter dns to show only DNS query and response packets ￼.
	•	Enter icmp to see only ICMP packets (such as ping requests/replies).
	•	Enter tcp to display all TCP packets ￼.

After typing a filter, Wireshark updates the packet list in real time to show only matching packets. (To clear the filter, click the Clear button or delete the filter text.) This lets you isolate and examine one protocol at a time.

5. Identify and explain common protocols

In the capture, look at the Protocol column (or Packet Details) to see what kinds of traffic you captured. For example:
	•	HTTP (Hypertext Transfer Protocol): This is the standard protocol for web pages. It operates at the application layer. HTTP packets typically use TCP port 80 and carry requests/responses (HTML, images, etc.) between your browser and web servers ￼. HTTP is “the foundation of the World Wide Web,” defining how browsers and servers exchange data ￼.
	•	DNS (Domain Name System): DNS packets (usually UDP port 53) resolve domain names to IP addresses. Each time your browser or ping command uses a hostname (like example.com), a DNS query is sent. DNS is a hierarchical naming service; it “translates domain names to the numerical IP addresses needed” for network communication ￼.
	•	ICMP (Internet Control Message Protocol): ICMP is used for network diagnostics and error messages. The classic example is ping, which uses ICMP Echo Request and Reply messages to test reachability. ICMP “is used by network devices… to send error messages and operational information” and lets tools like ping and traceroute check connectivity ￼ ￼.
	•	TCP (Transmission Control Protocol): Many protocols (HTTP, DNS over TCP, etc.) run on TCP. TCP is a connection-oriented transport protocol that provides reliable, ordered delivery of data between endpoints ￼. In your capture, any “TCP” packets indicate the three-way handshake or data flow underlying HTTP, DNS (when using TCP), or other services. TCP ensures that data arrives intact from your Mac to the server.

(Your capture may also include link-layer frames like Ethernet, ARP, or other protocols. For example, ARP resolves local IPs to MAC addresses, but it doesn’t carry user data.)

6. Export the capture as a .pcap file

After analysis, save the captured packets. In Wireshark, go to File > Save As… (or click the save icon). In the save dialog, choose “Wireshark/tcpdump/… pcap” as the file format and give it a name (e.g. capture_task5.pcap). You can also check “Compress with gzip” to shrink the file if needed ￼. Click Save – this writes your captured data to the .pcap file. This file can be opened later in Wireshark or submitted as required.

7. Take safe screenshots and document findings

On macOS, you can capture screenshots using the built-in tools ￼. For example, press Shift+Command+4 – the pointer turns into a crosshair ￼. Drag over the area of the Wireshark window you want to capture, then release. The screenshot will save to your desktop. Important: Before using any screenshots in reports, blur or redact any sensitive information. Hide personal IP addresses or MAC addresses if present (MAC addresses are tied to your hardware but generally only reveal manufacturer, not personal info ￼). Also crop out your local hostname or any visible email/username. Give screenshot files generic names (e.g. screenshot1_interface.png, screenshot2_filter_http.png) without real addresses. In your documentation, describe findings clearly but avoid publishing any internal IPs or private data.

⸻


Tools Used
	•	Wireshark: For live packet capture and analysis.
	•	Web Browser: (e.g. Safari or Chrome) to generate HTTP/DNS traffic by visiting websites.
	•	Terminal (macOS): Used for networking commands like ping to generate ICMP traffic.

Steps Performed
	1.	Installed Wireshark on macOS: Downloaded the official Wireshark macOS package from wireshark.org and installed it.
	2.	Selected the network interface: Opened Wireshark’s Capture Options and chose the active interface (e.g. “Wi-Fi (en0)” for wireless).
	3.	Generated live traffic: Started the capture, then browsed to websites and used ping in Terminal. This produced HTTP, DNS, and ICMP packets.
	4.	Applied protocol filters: In Wireshark’s filter bar, used filters like http, dns, and icmp to isolate those packets.
	5.	Identified protocols: Examined packet details to identify HTTP, DNS, ICMP, and TCP traffic (see below for descriptions).
	6.	Exported the capture: Saved the captured packets to a file named capture_task5.pcap (checked “compress” option for smaller size).
	7.	Documented findings: Took screenshots of filtered results and noted the key observations (see protocol list and outcomes).

Protocols Identified
	•	HTTP (Hypertext Transfer Protocol): Web traffic between client and server (used port 80 by default). HTTP follows a request/response model where browsers fetch HTML and other resources. It is the core protocol of the World Wide Web.
	•	DNS (Domain Name System): Name-resolution traffic. DNS packets translate domain names (like example.com) into IP addresses. Each DNS query/response pair is visible as “DNS” in Wireshark.
	•	ICMP (Internet Control Message Protocol): Used by the ping tool. ICMP Echo Request and Echo Reply packets check whether a host is reachable. In the capture, pinging a server produced these ICMP packets.
	•	TCP (Transmission Control Protocol): The transport protocol underlying HTTP (and sometimes DNS). TCP provides reliable, ordered data delivery. TCP handshake packets and TCP segments carrying HTTP data were visible.
(Other protocols like Ethernet II (link-layer frames) and ARP (address resolution) also appeared; these handle local network addressing but carry no user data.)

.pcap Export Info
	•	The capture was saved in the standard .pcap format (compatible with Wireshark and tcpdump).
	•	The file was named capture_task5.pcap. (We chose gzip compression in the save dialog for a smaller file size ￼.)
	•	This .pcap file contains all captured packets and can be opened later for further analysis or evidence.



Key Learning Outcomes
	•	Learned how to install and configure Wireshark on macOS (including granting capture permissions).
	•	Practiced capturing live network traffic and intentionally generating packets using browsing and ping.
	•	Used Wireshark display filters to zero in on specific protocols (HTTP, DNS, ICMP, TCP).
	•	Gained a basic understanding of the captured protocols: HTTP for web data, DNS for name lookups, ICMP for network diagnostics, and TCP for reliable transport.
	•	Learned how to export the capture data to a .pcap file for sharing or further analysis.
	•	Understood the importance of data privacy: screenshots were sanitized to remove personal IPs/MACs and any sensitive content.
