How to Use Wireshark for Network Traffic Analysis
This guide walks you through getting started with Wireshark, a powerful tool for analyzing network traffic.

Step 1: Install Wireshark
Install Wireshark on your system:

Linux:

bash
sudo apt install wireshark
Windows or macOS: Download it from the Wireshark website.

Step 2: Open Wireshark and Capture Traffic
Launch Wireshark.

Select a network interface (e.g., eth0 for Ethernet or wlan0 for Wi-Fi).

Click Start to begin capturing traffic.

Step 3: Filter Traffic
To focus on specific packets, use Wireshark’s filter bar:

Filter by Protocol: For HTTP traffic, enter:

http
Filter by IP Address: To capture packets from a specific IP:

ip.addr == 192.168.1.1
Step 4: Analyze Captured Packets
Click on any packet to view its details, including headers and payload. Wireshark displays data in three panes:

Packet List: All captured packets.

Packet Details: Layer-by-layer breakdown.

Hex Dump: Raw data in hexadecimal format.

Conclusion
Wireshark is a go-to tool for troubleshooting network issues and understanding traffic patterns. Start exploring its features to sharpen your network analysis skills!