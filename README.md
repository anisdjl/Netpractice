*This project has been created as part of the 42 curriculum by adjelili.*

# NetPractice

## Description

NetPractice is a practical networking project from the 42 curriculum. The goal is to configure small-scale networks by solving 10 progressive levels, each presenting a non-functioning network diagram that must be fixed by adjusting IP addresses, subnet masks, and routing tables.

Through this project, you learn how devices communicate over a network, how routers direct traffic between subnets, and how to think systematically about network configuration and debugging.

## Instructions

### Running the Training Interface

1. Download the project files from the 42 project page.
2. Extract the files into a folder of your choice.
3. Run the training interface:
   ```bash
   bash run.sh
   ```
   This will start a local web server and open the interface in your browser automatically.

4. If `run.sh` does not work, start the server manually:
   ```bash
   python3 -m http.server 49242
   ```
   Then navigate to `http://localhost:49242` in your browser.

### Using the Interface

- Enter your 42 intranet login in the **Training** tab to load your personal configuration.
- Use the **Evaluation** tab to generate a random configuration for practice or peer-evaluation.
- Modify the unshaded (white) fields until the network is correctly configured.
- Click **Check again** to verify your configuration.
- Click **Get my config** to export and download your configuration file for each level.

### Exporting and Submitting

- After successfully completing each level, export the configuration using the **Get my config** button.
- **10 configuration files** (one per level) must be placed at the root of your Git repository.
- Make sure your 42 login is entered in the interface before exporting — Moulinette uses it to identify your configuration.
- During the defense, you will have to complete 3 random levels under a time limit, without access to external tools (a basic calculator like `bc` is tolerated).

## Key Networking Concepts

### OSI Model

The OSI (Open Systems Interconnection) model is a conceptual framework that divides network communication into 7 layers, each with a specific role:

| Layer | Name | Role |
|-------|------|------|
| 7 | Application | User-facing protocols (HTTP, FTP, DNS) |
| 6 | Presentation | Data formatting and encryption |
| 5 | Session | Managing connections between applications |
| 4 | Transport | End-to-end communication, error control (TCP, UDP) |
| 3 | Network | IP addressing and routing between networks |
| 2 | Data Link | Communication within the same network (MAC addresses) |
| 1 | Physical | Raw transmission of bits over a medium |

In NetPractice, we work primarily at **Layer 3** (IP addresses, routing) and **Layer 2** (switches).

### Switch

A switch is a Layer 2 device that connects multiple devices within the same local network (LAN). It forwards frames based on MAC addresses and does not perform routing — all devices connected to a switch share the same network. A switch does not need an IP address to function.

### Router

A router is a Layer 3 device that connects multiple different networks together. It forwards packets based on their destination IP address and a **routing table**, which lists known networks and the next hop to reach them. Each router interface belongs to a different network. When no specific route matches, the router uses the **default route** (`0.0.0.0/0`) to forward the packet to a gateway.

### TCP/IP

TCP/IP is the suite of protocols that powers the internet. It is composed of two main protocols:

- **IP (Internet Protocol)**: handles addressing and routing of packets across networks. Each device is identified by an IP address.
- **TCP (Transmission Control Protocol)**: handles reliable, ordered delivery of data between two endpoints. It ensures packets are received correctly and in order.

In NetPractice, we focus on the **IP layer** — configuring addresses and routes so that packets can travel from source to destination and back.

### IP Addresses and Subnet Masks

An IPv4 address is a 32-bit number written as four decimal octets, e.g. `192.168.1.1`. It has two parts:

- **Network part**: identifies which network the device belongs to
- **Host part**: identifies the specific device within that network

The **subnet mask** defines where the boundary between these two parts lies. For example, with a mask of `/24` (`255.255.255.0`), the first 24 bits are the network and the last 8 bits are the host.

For any subnet, given an IP and a mask:
- **Network address** = first IP of the range (not assignable)
- **Broadcast address** = last IP of the range (not assignable)
- **Usable IPs** = everything in between

Example with `192.168.1.0/24`:
- Network: `192.168.1.0`
- Broadcast: `192.168.1.255`
- Usable: `192.168.1.1` to `192.168.1.254`

The larger the prefix (e.g. `/30` vs `/24`), the smaller the subnet and the fewer usable addresses. A `/30` gives exactly 2 usable IPs, which is ideal for point-to-point links between two routers.

## Resources

### References

- [Hack The Box — Introduction to Networking](https://academy.hackthebox.com/module/details/34) — comprehensive networking module covering OSI model, IP addressing, subnetting, and routing
- [Wikipedia — OSI Model](https://en.wikipedia.org/wiki/OSI_model) — full overview of the 7-layer model
- [Wikipedia — Subnetwork](https://en.wikipedia.org/wiki/Subnetwork) — subnetting explained
- [Wikipedia — Routing Table](https://en.wikipedia.org/wiki/Routing_table) — how routing tables work
- [lpaube/NetPractice — Guide in French](https://github.com/lpaube/NetPractice/blob/main/README.fr.md) — level-by-level explanations of NetPractice concepts
- [yomazini/42cursus-Netpractice](https://github.com/yomazini/42cursus-Netpractice) — visual walkthrough of all 10 levels
- [codequoi.com — IPv4, Routing and Subnet Masks](https://www.codequoi.com/adresses-ipv4-routage-et-masques-de-sous-reseau/) — detailed French article on subnetting
- [YouTube — NetPractice: An Intro to IP Addresses and Subnets](https://www.youtube.com/watch?v=HQUw0CfQWAM) — video walkthrough of NetPractice concepts
- [YouTube — Adressage IP: exercices et solutions](https://www.youtube.com/watch?v=vaC_xZpOE8U) — subnetting exercises in French

### Use of AI

An AI assistant was used to help understand all the networking concepts covered in this project, including subnet masks, IP addressing, routing tables, gateway reachability, and how to debug network configurations systematically.
