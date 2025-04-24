---
title: "Don't Bother the Internet, This Is How It Works!"
datePublished: Thu Apr 24 2025 07:37:03 GMT+0000 (Coordinated Universal Time)
cuid: cm9v1uwew001h08jpc7wu0tgj
slug: dont-bother-the-internet-this-is-how-it-works
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1745476595361/27895a62-7e75-40b3-b4e4-a1e6ad444438.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1745480196174/1270cd07-9243-4c32-beb2-aff9a050c16f.png
tags: tls, internet, networking, tcp, osi-model, tcpip-model

---

# 🔎 Introduction

In simple terms, if you're familiar with computers, you can think of the internet as a massive collection of interconnected computers.

During the early stages of technological advancement, there was a global race among countries to achieve dominance. Russia took the lead by launching the first satellite, named **Sputnik**.

This development spurred the United States to act. In response, they established **ARPA** (Advanced Research Projects Agency). ARPA aimed to connect all its offices and research centers, leading to the creation of **<mark>ARPANET</mark>** — a network that initially connected four universities for the purpose of sharing information.

They used a set of rules known as **protocols** to send messages and files securely. One of these rules was **TCP** (we'll dive into this later). For now, just understand that these protocols ensured that data was shared in a structured and reliable way.

This marked the very early stages of the internet. It wasn’t global yet and was used strictly for research purposes. One major challenge at the time was navigating between multiple documents or pages — until a computer scientist named **Tim Berners-Lee** introduced several key innovations:

* **HTML** – the language used to create web pages
    
* **HTTP** – the protocol used to fetch those pages
    
* **URL** – the addressing system to locate web resources
    
* **The first browser** – originally called **World Wide Web**, later renamed **Nexus**
    

At this point, search engines didn’t exist. They were introduced later, and their arrival significantly accelerated the growth of the internet.

<mark>We'll dive into the technical details soon</mark>, but it’s worth noting that the internet is governed by certain organizations. One of the key ones is the **Internet Society (ISOC)**.

The **Internet Society**, a non-profit organization founded in 1992 (around the time the internet was becoming publicly accessible), has the mission:

> “To keep the internet open, globally connected, trustworthy, and secure — for everyone.”

# 🔎 How Does a User Reach [Google.com](http://Google.com)?

Let’s break down what happens when you type [**google.com**](http://google.com) into your browser:

1. You type [`google.com`](http://google.com) in your browser.
    
2. Your computer sends a request to Google’s server.
    
3. The server processes the request and sends back a response.
    

<details data-node-type="hn-details-summary"><summary>✅ How Does Your Computer Find Google?</summary><div data-type="detailsContent">The domain <a target="_self" rel="noopener noreferrer nofollow" href="http://google.com" style="pointer-events: none">google.com</a> is mapped to an IP address like 142.250.190.14. This is similar to finding a phone number by searching someone’s name in your contact list. This process is handled by the Domain Name System (DNS).</div></details><details data-node-type="hn-details-summary"><summary>✅ ICANN – The Root Authority</summary><div data-type="detailsContent">ICANN (Internet Corporation for Assigned Names and Numbers) manages the root of the domain system and delegates control to registrars. When someone registers a domain like <a target="_self" rel="noopener noreferrer nofollow" href="http://google.com" style="pointer-events: none">google.com</a>, they do it through a domain registrar, which updates the global DNS directory.</div></details><details data-node-type="hn-details-summary"><summary>✅ IP Addresses</summary><div data-type="detailsContent">IP addresses consist of 4 numbers ranging from 0–255. Example: 142.250.190.14</div></details>

## *🗂️ Example: Accessing Google from Your Phone (via Wi-Fi)*

Assume your phone is connected to a Wi-Fi router. Here's the simplified flow:

```text
[Your Phone] 
192.xxx.xx.23
    ↓
[Router Local IP] 
192.xxx.xx.1
    ↓ (NAT: translates local IP to public IP)
[Router Public IP] 
1xx.xx.xx.xx
    ↓
[Internet Hops]
    ↓
[Google Server] 
142.250.64.78
    ↓
(Response follows the reverse path)
```

### 📂 DHCP – Dynamic Host Configuration Protocol

When your phone connects to Wi-Fi, it doesn’t have an IP address yet.  
So it sends a **DHCP Discover** message:

> "Hello! I just joined the network. Can someone assign me an IP?"

The router (acting as the **DHCP server**) responds with something like:

> "Sure! Here’s your IP: [`192.xxx`](http://192.xxx)`.xx.23`  
> Gateway: [`192.xxx`](http://192.xxx)`.xx.1`  
> DNS: `8.8.8.8`

Now your phone knows:

* Its **own IP address**: [`192.xxx`](http://192.xxx)`.xx.23`
    
* The **gateway** (router's local IP): [`192.xxx`](http://192.xxx)`.xx.1`
    
* The **DNS server** to resolve domain names.
    

### 📂 NAT – Network Address Translation

**NAT** allows multiple devices in a local network to access the internet using a single public IP address.

Here’s what NAT does:

* **Translates** your internal/private IP (e.g., [`192.xxx`](http://192.xxx)`.xx.23`) to the **router’s public IP**
    
* **Tracks** which request came from which device
    
* **Ensures** the correct device receives the correct response
    

This is essential for home networks where many devices share one internet connection.

### 📂 Ports

Ports help identify which service or app a device is using.

* Valid range: `0 – 65535`
    
* Ports `0 – 1023` are **reserved** for well-known services
    

Common examples:

* **Port 80** → HTTP (web traffic)
    
* **Port 443** → HTTPS (secure web traffic)
    

When your browser accesses [google.com](http://google.com), it connects to **port 80** (for HTTP) or **443** (for HTTPS) on Google’s server.

### 📂 DNS: The Phonebook of the Internet

**DNS** stands for **Domain Name System**.  
It’s like a phonebook for the internet.

You type: [`google.com`](http://google.com)  
DNS translates it to: `142.250.72.14`

Computers communicate via IP addresses — DNS helps humans use readable names instead.

### 📂 Domain Structure: Read Right to Left

Let’s break down the domain: [`blog.shop.example.com`](http://blog.shop.example.com)

| Part | Name | Description |
| --- | --- | --- |
| `.com` | Top-Level Domain (TLD) | The highest level domain like `.com`, `.org`, `.net`, etc. |
| `example` | Second-Level Domain (SLD) | The name registered under the TLD (e.g., [`example.com`](http://example.com)) |
| `shop` | Subdomain | A category or section of the main domain |
| [`blog.shop`](http://blog.shop) | Nested Subdomain | A subdomain under another subdomain (optional layers) |

## 🗂️ Few Topics Revision

<details data-node-type="hn-details-summary"><summary>✅ LAN</summary><div data-type="detailsContent">A <strong>Local Area Network (LAN)</strong> is typically used in your home or office. It connects devices like your phone, laptop, printer, and smart TV within a small area, such as a room, house, or building.</div></details><details data-node-type="hn-details-summary"><summary>✅ MAN</summary><div data-type="detailsContent">A <strong>Metropolitan Area Network (MAN)</strong> connects multiple LANs across a city or campus. Often used by internet service providers (ISPs) or large organizations. It links offices, data centers, or campuses within the same metropolitan area.</div></details><details data-node-type="hn-details-summary"><summary>✅ WAN</summary><div data-type="detailsContent">The <strong>internet</strong> itself is the biggest example of a WAN (<strong>Wide Area Network) </strong>. It connects many smaller networks (LANs and MANs) across the world.</div></details><details data-node-type="hn-details-summary"><summary>✅ Topology</summary><div data-type="detailsContent">refers to the arrangement of computers or devices in a network. It defines how different devices communicate and interact with each other. Below are the Types of Topologies.</div></details><details data-node-type="hn-details-summary"><summary>✅ Bus Topology</summary><div data-type="detailsContent">All devices share a single communication line. Simple but can suffer from congestion if too many devices are added.</div></details><details data-node-type="hn-details-summary"><summary>✅ Star Topology</summary><div data-type="detailsContent">All devices connect to a central hub or switch. Easy to manage and scale but relies on the central hub.</div></details><details data-node-type="hn-details-summary"><summary>✅ Ring Topology</summary><div data-type="detailsContent">Devices are connected in a closed loop. Data travels in one direction until it reaches its destination.</div></details><details data-node-type="hn-details-summary"><summary>✅ Mesh Topology</summary><div data-type="detailsContent">Every device is connected to every other device. Provides high redundancy and fault tolerance but is expensive to implement.</div></details><details data-node-type="hn-details-summary"><summary>✅ Tree Topology</summary><div data-type="detailsContent">A combination of <strong>star</strong> and <strong>bus</strong> topologies. Hierarchical structure with multiple levels of devices.</div></details><details data-node-type="hn-details-summary"><summary>✅ Hybrid Topology</summary><div data-type="detailsContent">A mix of two or more topologies. Provides flexibility and can be customized to suit different needs.</div></details><div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text"><strong><em>Let’s first see the Network Model and it’s layers and then we will see an example of End to End , how a message you type and sent travels over internet to reach your friend.</em></strong></div>
</div>

# 🔎 Network Structure

## 🗂️ OSI Model

The **Open Systems Interconnection (OSI)** model is a conceptual framework that defines the steps through which two computers communicate over a network. It consists of **7 layers**, each with its specific responsibilities.

#### **1\. Application Layer**

* Implemented in software such as web browsers, messaging apps, etc.
    
* This is the layer closest to the user, where network services like email, web browsing, and file transfer occur.
    

#### **2\. Presentation Layer**

* Receives data from the Application Layer.
    
* Converts data into a format that the network can understand (encoding).
    
* Responsible for **translation**, **encryption**, and **compression** of data.
    
* Data is already in binary format at this layer, but this layer prepares it for transmission.
    

#### **3\. Session Layer**

* Collects data from the Presentation Layer.
    
* Responsible for establishing, maintaining, and terminating sessions between devices.
    
* Handles **authentication** and **authorization**.
    
* Manages the dialog control (keeps track of which device is sending/receiving data).
    

#### **4\. Transport Layer**

* Responsible for **end-to-end delivery** of data.
    
* Breaks data into **segments**, each with source port, destination port, and sequence numbers.
    
* Handles **flow control** to prevent the receiver from being overwhelmed.
    
* Adds a checksum to detect errors in data transmission.
    
* Key protocols: **TCP** (reliable) and **UDP** (faster but no guarantee).
    

#### **5\. Network Layer**

* Responsible for **logical addressing**, assigning source and destination **IP addresses** to each data packet.
    
* Handles **routing**, moving packets across different networks.
    
* Routers operate at this layer.
    
* Data is broken into **packets** at this stage.
    

#### **6\. Data Link Layer**

* Breaks data into **frames** for transmission.
    
* Adds the sender’s and receiver’s **MAC addresses** to ensure correct delivery on the local network.
    
* Responsible for **error detection** and **access control** to the physical medium.
    

#### **7\. Physical Layer**

* Converts data into **physical signals** (electrical signals, light pulses, or radio waves) depending on the medium (cables, fiber optics, Wi-Fi).
    
* Handles the **actual transmission** of raw bitstream over the physical medium.
    

> **Note**: The OSI model is a conceptual framework. The real-world model, which is widely used, is the **TCP/IP model**.

## 🗂️ TCP/IP Model

While the <mark>OSI model is conceptual and often used for design and learning, the </mark> **<mark>TCP/IP</mark>** <mark>model is a practical</mark>, simplified framework that powers the modern internet. It consists of **4 layers**, each serving a similar function to the corresponding layers in the OSI model.

#### **1\. Application Layer**

* Closest to the user.
    
* Handles high-level protocols, data representation, encoding, and dialog control.
    
* Key protocols: **HTTP**, **FTP**, **SMTP**, **DNS**, **Telnet**.
    
* Application resides on this Layer , where the user interacts with it. Client Server Architecture.
    
* ```plaintext
          	     request
          client < ======= > server 
          	     response
    ```
    

#### **2\. Transport Layer**

* Responsible for **end-to-end communication** and **error recovery**.
    
* Ensures complete data transfer.
    
* Key protocols: **TCP** (reliable) and **UDP** (unreliable).
    

#### **3\. Internet Layer**

* Handles **logical addressing** and **routing**.
    
* Determines the best path for data through the network.
    
* Key protocols: **IP** (IPv4/IPv6), **ICMP**, **ARP**.
    

#### **4\. Network Access Layer (also known as Link Layer)**

* Deals with the **physical transmission** of data.
    
* Includes **hardware addressing** and protocols that operate at the data link level.
    
* Key protocols: **Ethernet**, **Wi-Fi**, **ARP** (again), **Frame Relay**.
    

> The **TCP/IP model** is simpler, more efficient, and serves as the foundation for modern internet communication. The OSI model, while still important for understanding how networks work, is more detailed and used primarily in theoretical and design contexts.

# 🔎 Me📱<mark>”Hey”</mark> → Internet → 📲Friend

## ***<mark>🗂️ Part 1: Your Phone to iMessage Server.</mark>***

1. ### Wi-Fi Join and IP Assignment (DHCP Process)
    

* **Airplane Mode** = No network.
    
* **MAC Address** = `AA:BB:CC:DD:EE:FF`
    
* You turn off Airplane Mode and join a Wi-Fi network.
    

```css
Phone: "Hi, DHCP server, who am I? Please give me an IP address."
(DHCP Discover — broadcast)

Router: "Here! Take 192.168.1.10, gateway 192.168.1.1, DNS 8.8.8.8"
(DHCP Offer)

Phone: "Okay, I’ll use that!"
(DHCP Request)

Router: "Confirmed."
(DHCP Acknowledgment)

✅ Your phone now knows:

IP Address: 192.168.1.10

Gateway: 192.168.1.1

DNS: 8.8.8.8
```

2. ### DNS Resolution (Finding the iMessage Server)
    

```css
You want to send a message to: imessage.apple.com (example domain).

Your phone sends a DNS query:

Protocol: UDP

Source IP: 192.168.1.10, Source Port: Random UDP port

Destination IP: 8.8.8.8, Destination Port: 53 (DNS)

➡️ Router performs NAT and forwards the query to 8.8.8.8.

DNS server replies:
imessage.apple.com → 17.172.224.47

✅ Your phone now knows where to send the message!
```

3. ### TCP Connection Setup (3-Way Handshake)
    

```css
Before sending any data, your phone establishes a TCP connection:

SYN: Phone → Apple
"Let’s start a connection! Seq=1000"

SYN-ACK: Apple → Phone
"Okay! Seq=3000, Ack=1001"

ACK: Phone → Apple
"Got it! Ack=3001"

✅ TCP connection established.
```

4. ### TLS Handshake (Securing the Connection)
    

```css
Now, a TLS handshake occurs over the TCP connection to encrypt the message.

🔐 TLS Handshake Steps:

ClientHello (Phone → Apple):

- Supported cipher suites
- Random number
- TLS version

ServerHello (Apple → Phone):

- Chosen cipher suite
- Server random
- Digital certificate (includes Apple’s public key)

Certificate Verification:

- Phone verifies Apple’s certificate using a trusted CA.

Key Exchange:

- Phone generates a pre-master secret.
- Encrypts it using Apple’s public key.
- Sends it to Apple.

Session Key Derivation: Both Phone & Apple derive session keys using:

- Client random
- Server random
- Pre-master secret

Finished Messages (Encrypted):

- Both sides confirm TLS handshake success.

✅ Session secured — all data is now encrypted.
```

5. ### Encrypting Your Message `"hey"`
    

```css
Plain Message: "hey"
Is encrypted using the session key.

Encrypted Application Data Includes:

- TLS Header
- Encrypted Payload

"Even your router or ISP can’t read it!"
```

6. ### TCP Segment Creation
    

```css
TCP Header:

Src Port: 5050
Dst Port: 443
Seq Num: 1002
Ack Num: 3001

'Data: Encrypted "hey" message'
```

> ### **TCP Header: What’s Inside?**
> 
> In addition to port numbers (both source and destination), the TCP header contains several important fields that enable its reliability and connection management. Here’s a breakdown of what’s inside:
> 
> * **Source Port & Destination Port**: To identify the sending and receiving applications.
>     
> * **Sequence Number**: Used to track the order of the packets and ensure the data arrives in the correct sequence.
>     
> * **Acknowledgment Number**: Used for confirming receipt of data. The receiver sends back an acknowledgment number to confirm the packets it has received.
>     
> * **Flags**:
>     
>     * `SYN` (Synchronize) for establishing a connection.
>         
>     * `ACK` (Acknowledgment) for confirming receipt.
>         
>     * `FIN` (Finish) for terminating the connection.
>         
> * **Window Size**: For flow control, telling the sender how much data the receiver can handle.
>     
> * **Checksum**: For error-checking, ensuring the integrity of the data.
>     
> 
> ---
> 
> ### **What is a Retransmission Timer?**
> 
> In TCP, when a sender sends a data segment (packet), it expects an ACK from the receiver to confirm that the packet was successfully received. If the sender doesn't receive the ACK within a specified period, the retransmission timer expires, and the sender retransmits the data packet.
> 
> This mechanism ensures that data loss (due to network congestion, packet corruption, or other issues) does not lead to permanent data loss.
> 
> **How it works:**
> 
> 1. The sender sends a TCP segment and starts the retransmission timer.
>     
> 2. The sender waits for an ACK from the receiver.
>     
> 3. If the sender doesn’t receive the ACK within the timer period (also known as the Timeout Interval), the timer expires, and the sender retransmits the segment.
>     
> 4. The process is repeated until the sender gets the ACK or a maximum number of retries is reached.
>     

| Feature | **TCP (Transmission Control Protocol)** | **UDP (User Datagram Protocol)** |
| --- | --- | --- |
| **Type** | Connection-oriented | Connectionless |
| **Handshake** | 3-way handshake (SYN, SYN-ACK, ACK) | No handshake—sends data directly |
| **Reliability** | Reliable—ensures delivery and order | Unreliable—no guarantee of delivery or order |
| **Acknowledgment** | ACKs are sent for every packet received | No acknowledgment mechanism |
| **Retransmissions** | Lost packets are retransmitted automatically | No retransmission; application must handle it if needed |
| **Data Ordering** | Guarantees ordered delivery | No guarantee of order |
| **Flow Control** | Uses windowing for flow control | No flow control—can overwhelm receiver |
| **Error Checking** | Extensive—includes checksums and reassembly mechanisms | Minimal—basic checksum only |
| **Speed** | Slower due to overhead of connection, ACKs, and retransmissions | Faster due to low overhead |
| **Use Cases** | File transfer, email, web browsing (HTTP, FTP, etc.) | Video streaming, VoIP, online gaming, DNS |
| **Real-world Analogy** | Certified mail—confirmation of delivery and order | Postcards—may arrive late, out of order, or not at all |

7. ### IP Packet Creation
    

```css
IP Header:
Src IP: 192.168.1.10
Dst IP: 17.172.224.47
TTL: 64
Protocol: TCP

"Data: TCP segment"
```

8. ### MAC Frame (Ethernet/Wi-Fi)
    

```css
To send to the router, phone checks ARP table:

If unknown, it sends an ARP request:

"Who is 192.168.1.1?"

Router replies:

"That’s me! MAC: BB:CC:DD:EE:FF:11"

Ethernet Frame:

Src MAC: AA:BB:CC:DD:EE:FF
Dst MAC: BB:CC:DD:EE:FF:11

Data: IP Packet
```

9. ### What the Full Frame Looks Like
    

```css
------------------------------------------------------------------------------
[ Frame ]
│
├── [ MAC Header (src MAC, dst MAC) ]     ← Data Link Layer
│   └── [ Packet ]
│       ├── [ IP Header (src IP, dst IP) ]    ← Network Layer
│       │   └── [ Segment ]
│       │       ├── [ TCP Header (src port, dst port) ]   ← Transport Layer
│       │       │   └── [ TLS-encrypted payload ]
│       │       │       └── [ Actual data + metadata ]    ← Application Layer
-------------------------------------------------------------------------------
```

```plaintext
Fragmentation & Splitting into Packets

- If the message is too large (exceeds MTU ≈ 1500 bytes), it’s split into smaller packets.
- Each packet still carries its own headers — crucial for reassembly.


🧱 Packet 1. =  [MAC][IP][TCP][TLS part 1 (start of encrypted data)]
🧱 Packet 2. =  [MAC][IP][TCP][TLS part 2 (middle of encrypted data)]
🧱 Packet 3. =  [MAC][IP][TCP][TLS part 3 (end of encrypted data)]



✅ Every packet is complete and self-contained, ready to travel the internet independently.
```

10. ### Router NAT & Internet Journey
    

**Router performs NAT**:

* Changes source IP to public IP (e.g., `203.0.113.45`)
    
* Tracks mapping:
    

```css
192.168.1.10:5050 → 203.0.113.45:40000
```

```css
Packet Goes Out to ISP:


Src IP: 203.0.113.45
Dst IP: 17.172.224.47
```

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">Then it travels: → ISP → Internet Backbone → Apple Data Center</div>
</div>

## ***<mark>🗂️ Part 2: iMessage Server to Your Friends Phone.</mark>***

1. ### Message Storage & Routing (Apple Server)
    

When Apple receives your message:

* The message remains end-to-end encrypted.
    
* Apple temporarily stores the message in its encrypted form.
    
* Apple looks up your friend’s device tokens (your friend may own multiple Apple devices like an iPhone, iPad, or Mac).
    
* It determines the optimal delivery paths.
    
* **Device Token Example:** `ab56b4d92b40713acc5af89985d4b786`
    

2. ### Push Notification via APNs
    

To wake your friend’s iPhone, Apple uses the **Apple Push Notification service (APNs)**:

* APNs sends a notification: “Wake up, you have a new iMessage!”
    
* **Transport details:**
    
    * Persistent **TCP connection** between APNs and your friend’s iPhone.
        
    * Already established to save battery and latency.
        
    * Fully **TLS-encrypted** for security.
        

3. ### Friend’s iPhone — Network Connection Setup
    

Your friend’s phone, like yours, is:

* Connected to Wi-Fi or cellular.
    
* Assigned a **local IP**, **public IP (via NAT)**, and **MAC address**.
    
* Maintains an active **TCP connection to APNs** to avoid repeated handshakes and conserve power.
    

4. ### TLS Handshake (Initial Setup)
    

When your friend’s phone powers on and connects to APNs:

* It performs a **TLS handshake** with Apple. (already covered above while sending message)
    
* Session keys are established for secure, encrypted communication.
    
* ```css
      Apple sends the push notification:      
      
      APNs → Friend’s iPhone
      Message: “You have a new iMessage!”
    ```
    

5. ### Encrypted Message Delivery
    

Apple’s server delivers the **end-to-end encrypted message**:

* Apple **cannot read the message** because:
    
    * It only stores encrypted blobs.
        
    * Only your friend’s device holds the **private decryption keys**.
        

**Example Encrypted Payload:**

```css
TLS-encrypted packet:
  - TCP header
  - TLS header
  - Encrypted data:
      - Message metadata (e.g., sender, timestamp)
      - Message content ("hey")
```

6. ### Message Decryption on Friend’s Device
    

Your friend’s iPhone:

* Receives the encrypted data.
    
* The iMessage app **decrypts the message** using the private key stored on the device.
    
* The message appears: **"hey"**
    

7. ### Delivery Acknowledgment
    

* iMessage sends a **delivery receipt** back to Apple:
    
    * Over **TCP + TLS**
        
* Apple updates the message status.
    
* You, the sender, see: **“Delivered ✅”**
    

---

# 🔎 P2P

**P2P (Peer-to-Peer) architecture** is a network model in which each device (called a *peer*) functions both as a **client** and a **server**.

Unlike traditional **client-server** systems—where clients request resources and servers respond—P2P allows **all peers to**:

* Request data
    
* Provide data
    
* Communicate directly with other peers
    

This decentralized model enhances scalability and resilience.

## 🗂️ Example Scenario: Downloading a Text File via P2P

Let’s imagine you're downloading a file named:

```markdown
story.txt (1 MB)
```

You're using a **BitTorrent-like P2P application**.

### 📂 Step 1: File is Split into Chunks

Before the file is shared, the original uploader (called a **seeder**) splits it into small parts. For example:

```yaml
story.txt ➡️ split into 4 chunks:
- Part 1: 0–256 KB  
- Part 2: 256–512 KB  
- Part 3: 512–768 KB  
- Part 4: 768 KB–1 MB
```

Each chunk is assigned a **hash** (a unique identifier) to verify data integrity during download.

### 📂 Step 2: Chunks are Shared Across Peers

As users download pieces, they also upload the ones they have to others. Over time, the file is distributed like this:

| Peer | Chunks Owned |
| --- | --- |
| Peer A | Part 1, Part 4 |
| Peer B | Part 2 |
| Peer C | Part 3, Part 4 |
| Peer D | Part 1, Part 2, Part 3 |

Now **you** join as **Peer E**, aiming to download the full file.

### 📂 Step 3: Downloading Chunks

Your P2P app:

1. **Connects to a tracker or DHT (Distributed Hash Table)** to discover which peers have which parts.
    
2. **Downloads multiple chunks simultaneously** from different peers for speed.
    

Example download pattern:

* Part 1 from Peer D
    
* Part 2 from Peer B
    
* Part 3 from Peer C
    
* Part 4 from Peer A
    

These chunks are downloaded **independently and in parallel**, not necessarily in order.

### 📂 Step 4: Reassembling the File

Once all chunks are downloaded:

* The app verifies each part using its **hash** to ensure data integrity.
    
* Then it reassembles the parts into the original file:
    

```css
[Part 1] + [Part 2] + [Part 3] + [Part 4] ➡️ story.txt
```

Now the file is complete and ready to be opened like any normal file.

### 📂 Step 5: You Become a Seeder

After successfully downloading the full file:

* Your app begins **uploading chunks to other peers** still downloading.
    
* You become a **seeder**, contributing to the network and helping others.
    

# 🔎 Some Network Devices You Should Know

## 🗂️ Repeater

A **repeater** receives a signal, amplifies or regenerates it, and retransmits it over a network.

**Main Use**: To **extend the range** of a network where the signal gets weak or degraded over distance — commonly seen in early Ethernet or Wi-Fi setups.

| Model | Layer Name | Repeater Lives Here? |
| --- | --- | --- |
| OSI Model | Layer 1 – Physical | ✅ Yes |
| TCP/IP Model | Network Access Layer | ✅ Yes |

## 🗂️ Hub

A **hub** broadcasts incoming data to **all connected ports**, regardless of the actual destination.

Think of it like a loudspeaker: one device talks, and everyone hears — even if the message was meant for just one.

In a hub-based network, every device receives all the traffic, but:

> Your network card (NIC) is smart enough to say:  
> “Is this packet for me? No? Ignore it.”

### 📂 But... What About Sniffing?

Since all data goes through your NIC:

* You **can** use tools like **Wireshark** to sniff traffic from others.
    
* Only possible if:
    
    * The data is **unencrypted** (e.g., HTTP, not HTTPS)
        
    * You're using a **dumb hub**, not a switch
        
    * You're running **packet sniffing software**
        

| Model | Layer Name | Does Hub Work Here? |
| --- | --- | --- |
| OSI Model | Layer 1 – Physical Layer | ✅ Yes |
| TCP/IP Model | Network Access Layer | ✅ Yes |

### 📂 3 Main Types of Hubs

| Hub Type | Description | OSI Layer |
| --- | --- | --- |
| 1️⃣ Passive Hub | Just connects cables and passes signals without amplification | Layer 1 |
| 2️⃣ Active Hub | Boosts/amplifies the signal before sending it out — like a repeater + hub | Layer 1 |
| 3️⃣ Intelligent Hub | Offers monitoring/diagnostics and limited traffic management (still broadcasts) | Layer 1 |

## 🗂️ Bridge

A **bridge** connects two or more **network segments**, making them work as one — but with intelligence.

It examines **MAC addresses** and decides whether to forward or block traffic.

> **Goal**: Reduce traffic, isolate collisions, and improve LAN performance.

```plaintext
[Floor 1 Devices] ─┐
                  │
              [ Bridge ] ─── [ Router / Internet ]
                  │
[Floor 2 Devices] ─┘
```

* It forwards **external traffic** (e.g., to the internet)
    
* It **blocks internal traffic** that doesn’t need to cross segments (like a print job on Floor 2)
    

| Model | Layer Name | Works Here? |
| --- | --- | --- |
| OSI Model | Layer 2 – Data Link Layer | ✅ Yes |
| TCP/IP Model | Network Access Layer | ✅ Yes |

### 📂 Example Scenario

You're on **Floor 1**, browsing the web:

* Your PC sends a DNS/HTTP(S) request → the bridge forwards it to the router.
    
* Someone on **Floor 2** prints something → the bridge blocks it from reaching Floor 1.
    
* Result: **Less congestion**, **faster performance**.
    

### 📂 Without a Bridge?

* All traffic goes everywhere.
    
* Broadcast storms and high congestion.
    
* Slower browsing and poor performance.
    

## 🗂️ Switch

A **switch** connects multiple devices within a LAN and **forwards data intelligently** — only to the intended recipient.

It uses MAC addresses to **learn which device is connected to which port**, unlike a hub that sends to all.

```css
[PC1]──┐
[PC2]──┤
[PC3]──┤──[Switch]──[Router]──🌐 Internet
[PC4]──┘
```

| Model | Layer Name | Works Here? |
| --- | --- | --- |
| OSI Model | Layer 2 – Data Link Layer | ✅ Yes |
| TCP/IP Model | Network Access Layer | ✅ Yes |

# 🔎 Let's Talk About Protocols

Everything in networking has a **protocol** — a set of rules that devices follow to communicate.

## 🗂️ What Are Protocols?

**Protocols** are like rules in a game — both sides must follow the same rules for it to work.  
In networks, protocols define **how devices communicate**, ensuring they understand and share data correctly.

### 📂 Why Are Protocols Important?

Without protocols:

* Data would be lost or misinterpreted
    
* Devices from different manufacturers wouldn’t communicate
    
* The internet wouldn’t function
    

Protocols ensure consistency, compatibility, and reliability.

## 🗂️ Types of Protocols

### 📂 HTTP / HTTPS (Web Protocols)

#### ✅ What is HTTP?

**HTTP (Hyper Text Transfer Protocol)** is a protocol used for communication between a **client** (usually a browser) and a **web server**.  
It transfers data in **plain text**, meaning it’s not secure — anyone intercepting the request can read the data.

* **Port**: 80
    
* **Security**: ❌ No encryption
    
* **Use cases**: Non-sensitive websites or internal tools
    

#### ✅ What is HTTPS?

**HTTPS (HTTP Secure)** is the secure version of HTTP.  
It uses **SSL/TLS encryption** to protect data during transmission — especially important for:

* Banking websites
    
* Logins and authentication
    
* E-commerce
    
* Any site handling sensitive data
    
* **Port**: 443
    
* **Security**: ✅ Encrypted via SSL/TLS
    

#### ✅ HTTP Methods

These methods tell the server what action the client wants to perform:

| Method | Purpose | Example |
| --- | --- | --- |
| `GET` | Read/Retrieve data | "Get me all blog posts" |
| `POST` | Create new data | "Create a new user" |
| `PUT` | Update an entire resource | "Update the whole profile info" |
| `PATCH` | Update part of a resource | "Just update the profile picture" |
| `DELETE` | Delete a resource | "Remove this user" |

#### ✅ HTTP Status Codes

HTTP responses come with status codes that explain the result of your request.

##### **<mark>Success</mark>**

* `200 OK`: Request succeeded
    
* `201 Created`: Resource created (usually after a POST)
    
* `204 No Content`: Success, no data returned (commonly for DELETE)
    

##### **<mark>Client Errors (Issues from your side)</mark>**

* `400 Bad Request`: Syntax error or missing required data
    
* `401 Unauthorized`: Not logged in / missing credentials
    
* `403 Forbidden`: Logged in but no permission
    
* `404 Not Found`: Resource doesn’t exist
    

##### **<mark>Server Errors (Issues from the server)</mark>**

* `500 Internal Server Error`: Server malfunction
    
* `502 Bad Gateway`: Invalid response from another upstream server
    
* `503 Service Unavailable`: Server is down or overloaded
    

#### ✅ HTTP Request Basics

When making a request to a server (especially with `POST`, `PUT`, or `PATCH`), here are the main components:

##### **Headers**

Metadata sent with the request or response.

| Header | Description |
| --- | --- |
| `Content-Type` | Format of the request body (e.g., `application/json`) |
| `Authorization` | Tokens or API keys for authentication |
| `User-Agent` | Info about the browser or device making the request |

Only used with methods like `POST`, `PUT`, `PATCH`.  
Usually sent in **JSON** format or form-encoded data.

**Example:**

```json
{
  "username": "bob",
  "password": "1234"
}
```

##### **<mark>Cookies</mark>**

Small pieces of data stored in your browser and automatically sent with each request to a domain. The use cases are below.

* Session management (stay logged in)
    
* Shopping carts
    
* Analytics and tracking
    

Both HTTP and HTTPS operate at the **Application Layer**, built on top of TCP (which is in the Transport Layer).  
HTTPS adds encryption using protocols like **TLS**, but still functions within the application layer.

**<mark>TCP/IP Layer</mark>**<mark>: Application Layer</mark>

### 📂 FTP / SFTP (File Transfer Protocols)

#### FTP

* **Port**: 21
    
* **Channels**: Command + Data
    
* **Modes**: Active & Passive
    
* **Encryption**: None (plaintext)
    

#### SFTP

* **Port**: 22 (over SSH)
    
* **Connection**: Single encrypted channel
    
* **Encryption**: Full via SSH
    

**<mark>TCP/IP Layer</mark>**<mark>: Application Layer</mark>

### 📂 SMTP / IMAP / POP3 (Email Protocols)

#### ✅ SMTP (Sending)

* **Port**: 25 (or 587 with STARTTLS)
    
* **Use**: Only for sending
    

#### ✅ IMAP (Receiving)

* **Port**: 143 (or 993 secure)
    
* **Emails stay on server**, supports sync
    

#### ✅ POP3 (Receiving)

* **Port**: 110 (or 995 secure)
    
* **Downloads and deletes emails**
    

#### ✅ SMTP vs POP3 – The Basics

| Protocol | Purpose | TCP/IP Model Layer |
| --- | --- | --- |
| SMTP(Simple Mail Transfer Protocol) | Used to send emails | Application Layer |
| POP3 (Post Office Protocol v3) | Used to receive/download emails | Application Layer |

#### ✅ SMTP – Sending Email

* You send an email from an email client (e.g., Gmail, Outlook) to your email server
    
* Email servers communicate with each other
    
* **Analogy**: Like handing your letter to a postman, who then delivers it through a chain of post offices.
    

#### ✅ SMTP in Action:

1. You write an email and hit “Send”.
    
2. Your client (e.g., Gmail app) connects to Gmail’s SMTP server.
    
3. SMTP delivers the email across the internet to the recipient’s email server.
    

#### ✅ SMTP Port Numbers

| Port | Description |
| --- | --- |
| 25 | Default SMTP port (often blocked by ISPs) |
| 465 | SMTP with SSL (older secure method) |
| 587 | SMTP with TLS (modern, secure, preferred) ✅ |

#### ✅ POP3 – Receiving Email

* You retrieve/download email from a mail server to your device
    
* The email is usually deleted from the server after download (unless configured otherwise)
    
* **Analogy**: Like visiting the post office, picking up your mail, and taking it home. The post office keeps no copy.
    

#### ✅ POP3 Port Numbers

| Port | Description |
| --- | --- |
| 110 | Default POP3 (unencrypted) |
| 995 | POP3 over SSL/TLS (secure) ✅ |

#### ✅ Email Flow Scenario – Step by Step

```css
- You: you@gmail.com
- Your Friend: friend@hotmail.com

1. You Write & Send the Email

- You open Gmail and write:
- "Hey, let’s catch up this weekend!"
- To: friend@hotmail.com
- You hit SEND 💥

2. Gmail Uses SMTP to Send the Mail

- Your Gmail client talks to:
- smtp.gmail.com
- Gmail’s SMTP server prepares and forwards the message:
- From: you@gmail.com
- To: friend@hotmail.com
- Message: "Hey, let’s catch up..."

3. Gmail SMTP Contacts Hotmail Server

- Gmail uses DNS to find Hotmail’s MX record.
- It connects to:
- smtp.live.com
- Then it transfers the message using SMTP.
- Now the message is waiting on Hotmail’s mail server.

4. Friend Checks Email via POP3

- Your friend opens Outlook (or any email app) configured with POP3.
- The app connects to:
- pop-mail.outlook.com
- Using port 995 (secure), it says:
- "Any new mail for friend@hotmail.com?"

5. POP3 Server Sends the Email

- Hotmail POP3 server responds:
- "Yes! Here is a new message from you@gmail.com"
- The email gets downloaded to your friend’s device.

If using default POP3 behavior → the message is deleted from the server after download.
```

**<mark>TCP/IP Layer</mark>**<mark>: Application Layer</mark>

### 📂 DNS (Domain Name System)

* **Port**: 53
    
* **Use**: Translates domains (e.g., [google.com](http://google.com) → IP)
    
* **Queries**: A, AAAA, MX, CNAME
    
* **Protocol**: UDP (mostly), TCP for larger transfers
    

**<mark>TCP/IP Layer</mark>**<mark>: Application Layer</mark>

### 📂 TCP (Transmission Control Protocol)

* **Connection-oriented**, reliable
    
* Uses **three-way handshake** (SYN, SYN-ACK, ACK)
    
* Ensures:
    
    * Packet ordering
        
    * Retransmission of lost packets
        
    * Congestion & flow control
        

**<mark>TCP/IP Layer</mark>**<mark>: Transport Layer</mark>

### 📂 UDP (User Datagram Protocol)

* **Connectionless**, fast, lightweight
    
* No ordering, no delivery guarantee
    
* Ideal for real-time apps (games, VoIP, video)
    

**<mark>TCP/IP Layer</mark>**<mark>: Transport Layer</mark>

### 📂 IP (Internet Protocol)

* **Use**: Routing packets between networks
    
* Versions: IPv4 (32-bit), IPv6 (128-bit)
    
* Routes based on **destination IP**
    
* No delivery or ordering guarantees
    

**<mark>TCP/IP Layer</mark>**<mark>: Internet Layer</mark>

### 📂 ICMP (Internet Control Message Protocol)

* **Use**: Diagnostics & error reporting
    
* Used by **ping**, **traceroute**
    
* Doesn’t carry user data — only control messages
    

**<mark>TCP/IP Layer</mark>**<mark>: Internet Layer</mark>

### 📂 Ethernet

* **Use**: Wired LAN communication
    
* Identifies devices by **MAC address**
    
* Uses **CSMA/CD** to handle collisions
    
* MTU: ~1500 bytes
    

**<mark>TCP/IP Layer</mark>**<mark>: Network Access Layer</mark>

### 📂 Wi-Fi (IEEE 802.11)

* **Use**: Wireless LAN communication
    
* Uses **SSID**, MAC addresses, and frequencies (2.4 / 5 GHz)
    
* Uses **CSMA/CA** to avoid collisions
    
* Encryption via **WPA2/WPA3**
    

**<mark>TCP/IP Layer</mark>**<mark>: Network Access Layer</mark>

### 📂 SSL / TLS (Security Protocols)

* **Use**: Encryption (mostly HTTPS)
    
* Performs a **handshake** to exchange keys
    
* Uses digital certificates (e.g., from Let’s Encrypt)
    
* TLS 1.3 is current (SSL is deprecated)
    

**<mark>TCP/IP Layer</mark>**<mark>: Application Layer</mark>

### 📂 IP Sec (Internet Protocol Security)

* **Use**: Encrypts IP packets (often in VPNs)
    
* Modes: **Transport** & **Tunnel**
    
* Uses:
    
    * **AH** (Authentication Header)
        
    * **ESP** (Encapsulating Security Payload)
        

**<mark>TCP/IP Layer</mark>**<mark>: Internet Layer</mark>

### 📂 SSH (Secure Shell)

* **Use**: Secure remote access
    
* **Port**: 22
    
* Uses key-based/password authentication
    
* Encrypts all communication
    
* Also supports **port forwarding**, **SCP**, **SFTP**
    

**<mark>TCP/IP Layer</mark>**<mark>: Application Layer</mark>

## **Thank-you!**

  
I'm glad you made it to the end of this article. I hope you found it helpful and learned something new. If you did, a **Like** would mean a lot — it really encourages me to keep writing more!

Feel free to **comment below** if there's a topic you'd like me to cover in future posts. I'm always open to suggestions and love hearing from readers.

* [**My GitHub Repos**](https://github.com/akxat)
    
* Connect with me on [**Linkedin**](https://www.linkedin.com/in/sharma-akshat/)
    
* Start [**your own blogs**](https://hashnode.com/@AkshatSharma/joinme)