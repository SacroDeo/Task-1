# Task-1
## **NMAP SCAN:**

![nmap1.png](attachment:46b785d5-fa01-46da-8a55-06912c601be5:nmap1.png)

The output provides the following information:

- The scan was run on September 22, 2025.
- **Three hosts** were found to be active on the network.
- For each active host, Nmap shows:
    - Whether the host is up.
    - The latency (how long it took to get a response).
    - The **ports** found on the host, including whether they are **open** or **closed**.
    - The **services** running on those ports (e.g., DNS on port 53).
- The entire scan of **256 IP addresses** was completed in 6.65 seconds.

In short, the image is a **network scan report** that shows which devices were active on a network and what services they were running.

### The Command: `nmap -sS <IP_Address>/24 -oN Commands/nmapResults.txt`

The command breaks down as follows:

- `nmap`: This is the command to launch the Nmap tool.
- `sS`: This is the **scan type** option, specifically a **TCP SYN scan** (also known as a "Stealth Scan"). It's called stealthy because it doesn't complete the full three-way TCP handshake, which can make it less likely to be logged by a firewall.
- `<IP_Address>/24`: This specifies the **target** of the scan. The `/24` is a **CIDR notation** that tells Nmap to scan an entire subnet of 256 IP addresses (from `<IP_Address>` up to `<IP_Address>` + 255).
- `oN Commands/nmapResults.txt`: This is the **output** option.
    - `oN` means "output to normal format."
    - `Commands/nmapResults.txt` is the file path where the scan results will be saved.
    

*I have used Wireshark to capture packets for analysis and i have attached the .pcap file in the repo kindly please go through that.*

## Research On the Open ports and there Services:

I’ve Done the Nmap scan, and here’s what I found. 

Out of 256 devices, I spotted three active ones. One has port 53 open, which I know is usually for DNS (turning website names into IP addresses). The other two either blocked or closed all ports, so they’re not running any services.

### What’s Running on Port 53?

I figured out that port 53 typically runs DNS services like BIND, dnsmasq (common in home routers or virtual setups like VMware), or Microsoft DNS. It’s probably helping with name resolution on my network.

### Possible Risks

Since I’ve got port 53 open, here are some risks I need to watch out for:

- **Big Traffic Attacks**: Hackers could trick it into sending huge amounts of data to someone else.
- **Fake Websites**: They might mess with DNS to redirect me to bad sites.
- **Software Bugs**: If my DNS software isn’t updated, it could be vulnerable.
- **Sneaky Data Theft**: Attackers could hide data in DNS requests to steal info.
- **Open Door Issues**: If anyone can use it, it might get abused or flagged.
- **Network Trouble**: Even internally, malware could use it to spread.

### Quick Fixes

- I’m going to set up a firewall to limit who can access it.
- I’ll also make sure the DNS software is updated, turn off extra features if I don’t need them, and keep an eye on weird traffic on port 53.
- Since this is just my home or lab setup, the risks are lower, but I’ll still lock it down!
