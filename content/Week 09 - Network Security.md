---
title: Week 09 - Network Security
date: 2025-12-14
tags:
  - network-defense
  - architecture
  - firewalls
  - IDS
aliases:
  - DMZ
  - Packet Filtering
  - IPS
summary: Architectural defenses including DMZs, Firewalls, and Intrusion Detection Systems.
---
## Key Terms
|Term|Definition|Exam Context/Example|
|:--|:--|:--|
|**Firewall**|A mechanism for maintaining control over the traffic that flows into and out of a network.|Firewalls are typically placed on the border between an internal network and the Internet, or internally to protect sensitive network traffic. They can allow or disallow traffic based on factors like the protocol being used.|
|**Packet Filtering**|One of the oldest and simplest firewall technologies that examines the contents of each packet individually.|Filtering decisions are based on the source and destination IP addresses, port number, and the protocol used. Because packets are examined individually and out of context, attacks can potentially slip through this type of firewall.|
|**Stateful Packet Inspection (Stateful Firewall)**|A firewall technology that keeps track of traffic over a given connection, defined by source/destination IPs, ports, and existing traffic, using a state table.|This type of firewall will only allow traffic through that is part of a new or already established connection. Most stateful firewalls can also function as packet filtering firewalls.|
|**Deep Packet Inspection**|Firewalls that add intelligence by analyzing the actual content of the flowing traffic.|These firewalls can reassemble the contents of the traffic to see what will be delivered to the application, allowing them to filter out attacks and undesirable content based on contents rather than just structure. This process is slower and introduces delay.|
|**Proxy Servers**|A specialized variant of a firewall that provides security and performance features, generally for a particular application (e.g., mail or Web browsing).|Proxy servers serve as a choke point to filter traffic for attacks or malware. They provide a layer of security for devices behind them by acting as a single source for requests, and are used widely in businesses to filter spam and objectionable content.|
|**DMZ (Demilitarized Zone)**|A network design feature combined with a protective device (like a firewall) used for systems that must be exposed to external networks, such as mail servers or Web servers.|A DMZ places a layer of protection between the exposed system and the Internet, and another layer between the system and the rest of the internal network.|
|**Network Segmentation**|The division of a network into multiple smaller networks, each acting as its own small network, called a subnet.|Proper segmentation helps reduce the impact of attacks, localize technical network issues, and prevent unauthorized traffic from reaching sensitive portions of the network.|
|**Choke Points**|Certain points in the network through which traffic is funneled for inspection, filtering, and control.|Examples include routers moving traffic between subnets, or firewalls/proxies controlling traffic. Choke points pose a risk because if they fail, the network is compromised.|
|**IDSes (Intrusion Detection Systems)**|Devices or software that monitor networks, hosts, or applications for unauthorized activity.|Network-based IDSes (NIDSes) are typically attached to the network to monitor traffic and are often placed behind a filtering device, like a firewall, to reduce the traffic they need to inspect.|
|**Signature-based Detection**|An IDS method that maintains a database of attack signatures and compares incoming traffic against those signatures.|This method works well for known attacks, similar to antivirus systems, but fails when encountering new attacks or those specifically constructed to avoid existing signatures.|
|**Anomaly-based Detection**|An IDS method that establishes a baseline of normal network traffic and activity, measuring the present state against that baseline.|This method is effective for detecting new attacks, but may result in a larger number of false positives if legitimate activity causes unusual traffic patterns that deviate from the baseline.|
|**Defense in Depth**|The concept of implementing multiple layers of security appropriate for the value of the assets being secured.|Combining functions, such as firewalls and IDSes, into one correlated capability is an example of starting a defense in depth security program.|
|**Virtual Private Networks (VPNs)**|An encrypted connection, often referred to as a tunnel, between two points used for sending sensitive traffic over unsecure networks.|VPNs allow remote workers to connect securely to internal organizational resources or can be used by the public to protect or anonymize traffic from ISPs or others on untrusted connections.|
|**Rogue Access Points**|Wireless access points attached to a network without authorization.|These devices can bypass existing border security measures and may invalidate carefully planned network security by creating an insecure back door.|
|**WPA2 (Wi-Fi Protected Access version 2)**|The most current and strongest encryption protocol used for 802.11 wireless devices.|WPA2, along with WEP and WPA, are the three major categories of encryption used to protect the confidentiality of traffic flowing over wireless networks.|
|**SSH (Secure Shell)**|A secure protocol based on RSA public key encryption used to secure communications.|SSH is the secure equivalent of Telnet and can be used for terminal access, file transfers (SFTP), securing remote desktop traffic, and communicating over a VPN.|
|**MDM (Mobile Device Management)**|An external solution that enables central management of mobile devices.|MDM solutions enforce policies by regulating access to enterprise resources, mandating security patches and password changes, and allowing devices to be remotely wiped or disabled if they become noncompliant or are stolen.|
|**BYOD (Bring Your Own Device)**|An organization’s strategy and policies regarding the use of personal versus corporate devices.|This approach is popular due to leveraging equipment the organization did not pay for. A permissive BYOD policy carries risks, but a strict policy involving MDM can enforce security measures on personal devices.|
|**Port Scanners**|Tools used to search for hosts on a network, identify the operating systems those hosts are running, and detect the versions of services running on any open ports.|Security professionals use tools like Nmap (Network Mapper) to discover the networks and systems present in their environment.|
|**Packet Sniffers (Network or Protocol Analyzer)**|A tool that intercepts traffic on a network, amounting to listening for any traffic that the network interface of a device can see.|Tools like Wireshark and Tcpdump are used for troubleshooting and security analysis. Sniffers can be used to glean sensitive data (like login credentials) if insecure protocols are used.|
|**Honeypots**|A tool configured to deliberately display vulnerabilities or attractive materials (e.g., an outdated operating system or a tempting network share) to detect, monitor, and study attackers.|Honeypots provide an early warning system for a corporation or serve as a research method for understanding attacker techniques.|
|**IPsec (Internet Protocol Security)**|A solution that encapsulates the original IP packet into a secure packet, used to provide confidentiality, authentication, and integrity.|IPsec is commonly used in site-to-site VPN scenarios, working purely at the network layer. It has mechanisms to prevent packet modification using hashing and anti-replay protection via sequence numbers.|
|**DNS Spoofing**|An attack where an unauthorized party replies to a DNS request before the legitimate DNS resolver, providing the client with false information.|DNS Security Extensions (DNSSEC) attempt to solve this by requiring recursive resolvers and higher-level servers to sign records using public-key cryptography, which clients can then verify.|
|**Zero-day Attacks**|New or unpublished attacks or vulnerabilities that are unknown to security tools and, therefore, can take systems by surprise when they surface.|Security assessments and penetration testing are typically only capable of finding known issues.|
|**Telnet**|An older, purely text-based protocol for remote access that transmits what the user types and receives the text output of the remote computer.|Telnet is completely unsecure and sends sensitive information like passwords unencrypted over the wire; it has largely been replaced by secure protocols like SSH.|

--- 
# Firewalls: Types & Rule Logic
## Comparison of Firewalls
A comparison of Stateless Packet Filtering firewalls and Stateful Inspection firewalls reveals significant differences in their operation, security capabilities, and limitations.

|Feature|Stateless Packet Filtering Firewall|Stateful Packet Inspection Firewall|
|:--|:--|:--|
|**Operation Principle**|Examines the contents of each packet individually and makes a determination based on simple factors.|Watches the traffic over a given connection and keeps track of its state.|
|**Information Used for Filtering**|Source/destination IP addresses, port number, and the protocol being used.|Source/destination IP addresses, ports being used, and already existing network traffic, using a state table.|
|**Context Awareness**|Filters an individual packet "out of context".|Able to keep track of the traffic at a granular level based on the connection state.|
|**Security Risk**|Attacks can potentially slip through because each packet is examined individually and not in concert with the rest of the traffic.|Only allows traffic that is part of a new or already established connection.|

---
**Remote Access Hierarchy (Least to Most Secure)**

1. **Least Secure:** Unencrypted protocols (Telnet, HTTP).
    
2. **Weak:** Graphical access with weak/legacy auth (Legacy VNC).
    
3. **Better:** RDP (Remote Desktop Protocol) _if_ Tunneled through VPN.
    
4. **Best:** **SSH (Secure Shell)**. Strong encryption, certificate-based auth, and can tunnel other traffic (X11 forwarding).
### The Difference: Stateful Inspection and the State Table

**Stateful packet inspection firewalls** (stateful firewalls) operate on the same general principle as packet filtering firewalls but are able to keep track of traffic at a granular level.

A stateful firewall uses a **state table** to track the connection state of traffic. A connection is generally defined by the source and destination IP addresses, the ports being used, and the existing network traffic. For example, this type of firewall can identify and track the traffic related to a specific user-initiated connection, such as one to a Web site, and knows when that connection has been closed, indicating that further traffic should not legitimately be present.

This method is **more secure than simple packet filtering** because, while a simple packet filtering firewall examines an individual packet out of context, a stateful firewall only allows traffic through that is part of a new or already established connection. By tracking the state of connections, stateful firewalls prevent attacks that might otherwise slip through a simple packet filter because those filters examine packets individually without regard for the surrounding traffic context.

---

### The Limitations: What a Packet Filtering Firewall Cannot See

Packet filtering firewalls are limited to examining information readily available in the network stack headers, specifically the source and destination IP addresses, port number, and the protocol being used.

A significant limitation is that they **cannot see the actual content of the traffic**, often referred to as application-layer data or payload. Filtering high-level protocols built on top of UDP or TCP is complex for simple firewalls.

If a firewall needs to filter content based on what will be delivered to the application (such as filtering out viruses or undesirable content), it requires a more advanced technology called **Deep Packet Inspection**. Deep packet inspection firewalls reassemble the contents of the traffic to inspect the actual payload, enabling them to filter attacks and undesirable content based on the contents, rather than just the structure, of the network traffic. This capability is necessary because viruses and worms usually transit inside high-level protocols, especially those involving file exchange, making them complex to filter without looking at the payload.

Comparing these types of firewalls is like comparing a mail inspector who only checks the envelope for correct addresses and stamps (packet filtering) with one who keeps a list of all active conversations and only accepts replies relevant to existing letters (stateful inspection). Neither, however, opens the letter to read the actual message inside (which requires deep packet inspection).

## Hypothetical Firewall Rules for a Web Server
A set of hypothetical firewall rules for a web server, based on the provided sources (particularly the rule example in the slides), is presented below. This server is configured to handle standard web traffic (HTTP and HTTPS) and some essential network functions (DNS).

|Rule No.|Source IP|Dest IP|Protocol|Port|Action|Purpose|
|:--|:--|:--|:--|:--|:--|:--|
|**01**|`0.0.0.0/0`|`0.0.0.0/0`|Any|Any|**DROP**|Block packets with invalid states (e.g., malformed packets).|
|**02**|`0.0.0.0/0`|`0.0.0.0/0`|Any|Any|**ACCEPT**|Allow all traffic that is part of an already established connection (State: ESTABLISHED).|
|**03**|`127.0.0.0/8`|`0.0.0.0/0`|Any|Any|**ACCEPT**|Allow all traffic originating from the local loopback interface.|
|**04**|`0.0.0.0/0`|`127.0.0.0/8`|Any|Any|**ACCEPT**|Allow all traffic destined for the local loopback interface.|
|**05**|`58.242.82.5/32`|`0.0.0.0/0`|Any|Any|**DROP**|Explicitly block a known malicious IP address (or range).|
|**06**|`0.0.0.0/0`|`0.0.0.0/0`|ICMP|Any|**RATE LIMIT ACCEPT**|Limit the rate of ICMP traffic to prevent attacks, while allowing necessary communication.|
|**07**|`0.0.0.0/0`|`0.0.0.0/0`|TCP|80 (HTTP)|**ACCEPT**|Allow new incoming connections for standard web traffic (State: NEW).|
|**08**|`0.0.0.0/0`|`0.0.0.0/0`|TCP|443 (HTTPS)|**ACCEPT**|Allow new incoming connections for secure web traffic (State: NEW).|
|**09**|`0.0.0.0/0`|`0.0.0.0/0`|UDP|53 (DNS)|**ACCEPT**|Allow UDP traffic on port 53 for Domain Name System (DNS) queries.|
|**10**|`0.0.0.0/0`|`0.0.0.0/0`|Any|Any|**DROP**|**Default Deny/Implicit Deny:** Reject all other unsolicited traffic.|

_(Note: The `0.0.0.0/0` entries denote any IP address or network range, and `Any` denotes any protocol or port not specified.)_

---

### Best Practice: Default Deny (Implicit Deny)

The fundamental concept behind the final rule in the list (Rule 10) is **Default Deny**, also known as Implicit Deny.

- **Definition:** When building a firewall, the common configuration standard is to operate on a "**reject everything except what I allow**" basis. This means that after all specific allowance and blocking rules have been evaluated, there must be a final rule that explicitly rejects all traffic that did not match any preceding rule.
- **Importance:** This practice ensures that if a new or unexpected type of traffic appears that was not covered by the explicit `ACCEPT` rules, it is automatically blocked, maintaining security.

### Why the Order of Rules is Critical

The order in which firewall rules are defined is critical because firewalls typically process rules sequentially, from top to bottom.

1. **First Match Wins:** The firewall considers rules one by one, taking the **first one that matches the traffic** as the final answer. Once a match is found and an action (like `ACCEPT`, `REJECT`, or `DROP`) is executed, the firewall stops processing that packet against subsequent rules.
2. **Efficiency and Performance:** Rules intended to make the firewall more efficient, such as Rule 02 which accepts traffic for already established connections (Stateful Inspection), are placed near the beginning. This allows the firewall to quickly process valid, ongoing traffic without needing to evaluate it against the entire list of rules every time.
3. **Security Precedence:** Specific blocking rules, such as those targeting known bad IP addresses (Rule 05) or invalid traffic (Rule 01), must be placed _before_ any general `ACCEPT` rules that might otherwise permit the malicious traffic to pass.
4. **Implicit Deny Placement:** The final **Default Deny** rule (Rule 10) must be placed at the very end of the list to ensure that only traffic that failed to match any specifically accepted rule is caught and blocked. If the `DROP` or `REJECT` all rule were placed higher, it could block all subsequent legitimate traffic.


# Network Architecture: The DMZ

### Architecture of a Demilitarized Zone (DMZ)

A **Demilitarized Zone (DMZ)** is fundamentally a combination of a network design feature and a protective device, such as a firewall, used to increase network security by properly segmenting the network. The DMZ creates a layer of protection for systems that must be exposed to external networks, such as the Internet, while simultaneously protecting the internal network.

#### Placement: Firewalls, Internet, DMZ, and Internal LAN

In a network utilizing a DMZ, the firewalls are placed to create two distinct protective layers:

1. **External Firewall:** This firewall is situated between the **Internet** and the **DMZ**. This is the first line of defence and controls traffic flowing from the untrusted external network into the DMZ.
2. **Internal Firewall:** This firewall is situated between the **DMZ** and the **Internal Network (LAN)**. This layer controls communication between the exposed systems in the DMZ and the private, trusted systems on the LAN.

This design essentially places the DMZ network segment between two distinct layers of protection, typically firewalls, as shown in the source's illustration.

#### Service Location

The placement of servers depends on whether they need to be accessible from the external network (Internet) or if they only serve internal users.

|Location|Example Servers/Systems|Rationale|
|:--|:--|:--|
|**DMZ (Exposed Network Segment)**|Web servers, Mail servers, Proxy servers, Software as a service applications|These systems must be exposed to external networks (like the Internet) in order to function and serve customers or external clients. Traffic to these servers can be restricted only to the necessary ports, such as HTTP (port 80), HTTPS (port 443), or SMTP (port 25).|
|**Internal LAN (Private Network Segment)**|Database servers, Employee workstations, sensitive internal systems|These systems hold sensitive data or are used by internal personnel and must be shielded from direct access or exposure to the Internet.|

#### The '为什么' (Why): Protection via Segmentation

The primary purpose of the DMZ architecture is to prevent attackers who compromise an externally facing system from moving freely into the internal network. If a hacker successfully compromises the **Web Server** located in the **DMZ**, the architecture protects the **Database in the LAN** in the following way:

1. **Isolation:** The DMZ is a segmented network, meaning the Web Server is isolated from the sensitive internal LAN. Network segmentation prevents unauthorized network traffic or attacks from reaching portions of the network that should not be accessed.
2. **Internal Firewall Barrier:** The compromised Web Server is still on the _outside_ of the **Internal Firewall**. This firewall acts as a second, strong defensive barrier.
3. **Strict Filtering:** The Internal Firewall can be configured with highly restrictive rules that only allow necessary, controlled communication between the DMZ and the LAN. For example, the firewall might only allow the Web Server to communicate with the Database Server on a specific port for database requests, blocking all other protocols and traffic destined for the LAN.

If the hacker attempts to use the compromised Web Server as a jumping-off point to attack the Internal LAN, the Internal Firewall should deny the traffic, mitigating the attack and containing the intrusion within the DMZ segment. This layered approach is an example of security in network design.


# Intrusion Detection & Prevention (IDS/IPS)

## Contrast: Detection vs. Prevention

**Intrusion Detection System (IDS):** An IDS is a device or software that **monitors** networks, hosts, or applications for unauthorized activity. The goal of an IDS is to find and deal with malicious users. They constantly search for traces of possible intrusion by analysing network traffic itself, looking for unusual and abnormal traffic patterns, or even by partially reading packet content. They can detect known issues using signature-based detection or detect new issues by measuring current traffic against a baseline of normal activity (anomaly-based detection).

**Intrusion Prevention System (IPS):** The sources **do not contain information** regarding the definition, function, or contrast of an Intrusion Prevention System (IPS).

### Active vs. Passive Role

Based on the documented role of an IDS, it primarily operates in a **passive** or monitoring capacity:

- **Alerting/Passive Role (IDS):** An IDS monitors the traffic going by. Once an IDS detects a sign of intrusion (such as abnormal network traffic patterns or specific signatures), it takes appropriate action, which is usually carried out **through the firewall**. This indicates that the IDS is typically a _detection_ and _alerting_ tool rather than one that sits directly in the traffic flow to proactively block packets itself.
    
- **Blocking/Inline Role (IPS):** The sources **do not describe** a security system that sits 'inline' with the traffic to actively block packets, nor do they use the term 'span port' (mirror port).
    

### Placement of NIDS Sensors

A **Network Intrusion Detection System (NIDS)** needs to be placed carefully in a location on the network where it can monitor the traffic going by.

The ideal placement for an NIDS sensor is **behind another filtering device, such as a firewall**. Placing the NIDS behind a firewall helps to eliminate some of the obviously spurious (false) traffic, which in turn decreases the amount of traffic the NIDS needs to inspect. If the NIDS had to examine a large amount of traffic on a typical network, it would generally be limited to performing only a relatively cursory inspection, meaning it may miss some attacks.

Combining functions, such as firewalls and IDSes, into one correlated capability is a common strategy in a defence in depth security program.


## Explanation of Detection Methods

|Method|Definition|How it Works|
|:--|:--|:--|
|**Signature-Based Detection**|This method works similarly to most antivirus systems.|It maintains a database of signatures that might signal a particular type of attack and compares incoming network traffic against these known signatures.|
|**Anomaly-Based Detection (Heuristic)**|This method focuses on deviations from normal activity patterns.|It typically establishes a **baseline** of the normal traffic and activity taking place on the network and measures the present state of traffic against this baseline to detect patterns that are normally absent.|

### Pros and Cons (Zero-Day Attacks and False Positives)

The primary differences in their effectiveness and drawbacks are:

**Catching New (Zero-Day) Attacks:**

- **Anomaly-Based Detection** is better at catching new attacks. This method works well when looking to detect **new or unpublished attacks** (commonly known as **zero-day attacks**).
- **Signature-Based Detection** works well for known attacks but fails when encountering an attack that is **new** or has been specifically constructed not to match existing attack signatures. A large drawback is that if the system does not have a signature for an attack, it may miss it entirely.

**Prone to High False Positives:**

- **Anomaly-Based Detection** is prone to a larger number of **false positives** than signature-based detection.
- If the traffic on the network changes from the original baseline established, or if legitimate activity causes unusual traffic patterns or spikes in traffic, the Anomaly-Based IDS may incorrectly see this as an attack.

Many organizations now implement a single IDS that uses both signature-based and anomaly-based methods, which allows for greater flexibility in detecting attacks, though it may operate a bit more slowly and cause a lag in detection.


# Exam Style Questions


---

## 5 Potential 'Short Answer' Exam Questions

### Question 1: Firewall Filtering Comparison

Contrast **Stateful Packet Inspection firewalls** with simple **Packet Filtering firewalls** regarding the context they use when making filtering decisions. Why is stateful inspection generally more secure?

**Answer:** **Packet filtering** is one of the oldest and simplest firewall technologies and looks at the contents of each packet individually and out of context. The filtering determination is based on simple factors like source/destination IP addresses, port number, and protocol being used. **Stateful packet inspection firewalls** (stateful firewalls) are able to keep track of the traffic at a granular level and watch the traffic over a given connection. They use a **state table** to track the connection state, defined by source/destination IP addresses, ports, and existing network traffic. This is generally more secure because it only allows traffic through that is part of a new or already established connection, preventing attacks that might slip through a packet filter since those examine packets individually.

### Question 2: IDS Detection Methods

Explain the difference between **Anomaly-Based Detection** and **Signature-Based Detection** in an Intrusion Detection System (IDS), and identify which method is better suited for detecting **zero-day attacks**.

**Answer:** **Signature-based detection** maintains a database of attack signatures and compares incoming traffic to those signatures, working similarly to antivirus systems. **Anomaly-based detection** works by taking a baseline of normal network traffic and activity and measuring the present state against that baseline to detect unusual patterns. **Anomaly-based detection** is better suited for detecting **zero-day attacks** (new or unpublished attacks or vulnerabilities) because it detects deviations from the established norm, rather than relying on a known signature.

### Question 3: DMZ Architecture and Protection

When utilizing a Demilitarized Zone (DMZ), where are the two separate firewalls typically placed, and what is the function of the second (internal) layer of protection?

**Answer:** The DMZ architecture involves placing two layers of protection around systems exposed to external networks. One layer (the external firewall) is placed between the **Internet** and the **DMZ**. The second layer (the internal firewall) is placed between the **DMZ** and the **rest of the network**. The function of this second layer is to protect the devices on the internal network by restricting traffic, ensuring, for example, that only necessary ports (like IMAP or SMTP) pass through to reach servers within the DMZ.

### Question 4: VPN Goals and IPsec Mechanism

Name three security goals that Virtual Private Networks (VPNs) are designed to achieve, and explain how the IPsec VPN solution functions specifically at the network layer.

**Answer:** The security goals of a VPN are **Confidentiality**, **Authentication**, **Integrity**, and anti-replay. **IPsec (Internet Protocol Security)** is a solution that works entirely at the **network layer level**. It encapsulates the original IP packet into a secure IPsec packet, which is then transported over the unsecure network. IPsec uses hashing to authenticate the packet and prevent modification, and it uses a sequence number mechanism to provide anti-replay protection.

### Question 5: Port Scanners vs. Packet Sniffers

Distinguish between the purpose of a **Port Scanner** and a **Packet Sniffer** (Network Analyzer) in network security assessments, naming a specific example tool for each type found in the sources.

**Answer:** A **Port Scanner** searches for hosts on a network, identifies the operating systems they are running, and detects the versions of services running on any open ports. They are useful for discovering the networks and systems present in an environment. An example tool is **Nmap** (Network Mapper). A **Packet Sniffer** (or network analyzer) intercepts traffic on a network, which involves listening for any traffic that the network interface can see. Sniffers are used for troubleshooting and security analysis and can glean sensitive data if insecure protocols are used. An example tool is **Wireshark** or **Tcpdump**.

---

## 2 Potential 'Scenario-based' Long-Form Questions

### Scenario Question 1: Securing Remote Access and Tunneling

An employee working remotely needs secure access to corporate resources over an untrusted, public wireless network provided by a hotel.

**A. Recommended Security Measure:** What is the specific technology the employee should use to secure their connection and establish an encrypted "tunnel" to the internal network? Define this technology's primary purpose for remote workers. **B. Protocol Choice:** If the employee requires text-based terminal access to a remote server, they should avoid using the insecure **Telnet** protocol. What modern, secure protocol based on public key cryptography should they use instead, and what is a specific, non-terminal feature this secure protocol supports?. **C. Filtering Workaround:** If a firewall on the employee's network blocks their access because it filters their needed application protocol, describe one workaround solution for passing the data, using a technique mentioned in the sources.

**Answer:** **A. Recommended Security Measure:** The employee should use a **Virtual Private Network (VPN)**. A VPN connection, often referred to as a tunnel, is an encrypted connection between two points. For remote workers, VPNs allow them to connect to the internal resources of an organization, enabling the connected device to act as though it were connected directly to the organization’s internal network, allowing greater secure access.

**B. Protocol Choice:** They should use **Secure Shell (SSH)** instead of Telnet. SSH is a secure protocol based on RSA public key encryption. A specific, non-terminal feature that SSH supports is **file transfers** (using Secure File Transfer Protocol or SFTP).

**C. Filtering Workaround:** If a firewall is filtering a required protocol, one solution is to **embed the data in another protocol**. This has been done many times with protocols like HTTP to pass data through firewalls that otherwise would filter the traffic.

### Scenario Question 2: Managing Mobile Devices and Identifying Threats

A large corporation implements a **Bring Your Own Device (BYOD)** policy allowing personal smartphones to access basic corporate resources. Management is concerned about the risk this introduces, particularly the possibility of unauthorized hardware being attached to the network.

**A. MDM Implementation:** What external solution should the corporation implement to centrally manage these personal mobile devices, and name two specific security policies it allows the organization to enforce (even on personal devices)?. **B. Rogue Hardware Detection:** The security team is worried about unauthorized **rogue access points** being installed, which could bypass border security. What specific action should the team take to find such devices, and what Linux-based tool is mentioned as being well-known for detecting wireless access points?. **C. Insider Threat Monitoring:** To provide an early warning system for malicious activity, the security team decides to set up a tempting, vulnerable system named "top secret company docs" on the internal network. What is this security tool called, and how does its use assist in detecting or studying insider threats?.

**Answer:** **A. MDM Implementation:** The corporation should implement a **Mobile Device Management (MDM)** solution. MDM solutions enable central management and typically utilize an agent on the mobile device to enforce a specific configuration. Two specific security policies MDM solutions allow organizations to enforce are **mandating security patches/updates** and **forcing regular password changes**. MDM can also remotely wipe or disable a device if it becomes noncompliant or is stolen.

**B. Rogue Hardware Detection:** The simple solution for finding unauthorized wireless devices is to **carefully document the legitimate devices and regularly scan for additional devices**. The Linux-based tool mentioned for detecting wireless access points, even when attempts have been made to conceal them, is **Kismet**.

**C. Insider Threat Monitoring:** This security tool is called a **Honeypot**. A honeypot is configured to deliberately display vulnerabilities or attractive materials to serve as bait for an attacker. By catching the attacker, the organization can monitor their activities without their knowledge, providing an early warning system or serving as a method for researching the attackers' tools and methods. Honeynets (multiple honeypots) can be used internally to a network specifically to detect insider threats.