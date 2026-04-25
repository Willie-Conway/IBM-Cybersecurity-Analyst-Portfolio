# Securing Network Infrastructure

**Estimated time needed: 10 minutes**

---

## Introduction

Let's review the placement of basic network components to ensure security.

---

## Local Area Network (LAN)

A **Local Area Network (LAN)** , in a network diagram, is usually depicted as a cluster of devices, such as computers, printers, and servers, which are interconnected. The LAN is typically located at the **core** of the network diagram.

![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/lan.png>)

---

## Modem

The **modem** typically sits at the **network's edge** since it is the gateway between the local network and the internet. It is usually connected directly to the internet service provider's line (like a cable or DSL line).

> From the modem, a line is drawn to a router, which then connects to other devices in the network, like computers, printers, and switches. This setup allows all devices on the local network to access the internet through the modem.

![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/modem.png>)

---

## Router

**Routers** typically occupy a **central role**, connecting distinct networks. They are often depicted as nodes between the network's internal segments (such as LANs) and external networks (like the Internet).

Where multiple routers are involved in more complex networks, they are usually shown in the diagram forming a path between:

- The network's **edge** (where it interfaces with external networks)
- Its **core** (where the most critical, high-capacity parts of the network are located)

> These routers facilitate data flow, directing traffic based on the most efficient route to ensure seamless network communication.


![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/router.png>)

---

## Switch

A **switch** is usually placed at the **heart of the network infrastructure**. It is a controller connecting devices like computers, printers, and servers within a LAN.

- The switch manages traffic flow in this central role, effectively facilitating communication among connected devices
- It often connects to a router, which links the internal network to external networks such as the Internet
- The positioning of the switch ensures efficient data transfer within the network, promoting optimal performance and response time

> In a network diagram involving two routers and two LANs, each router is typically positioned as a central node within its respective LAN, facilitating intra-network communication and connecting the two LANs, enabling them to share data and resources efficiently.


![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/switch.png>)

---

## Firewall

A **firewall** is strategically positioned at the **front line of a network**, acting as a security control point between:

- The **internal network** (protected)
- The **external network** (unprotected, such as the Internet)

### Placement

The firewall is typically placed **immediately after the router** to filter incoming and outgoing traffic based on predefined security rules.

> The placement of the firewall is **critical** as it ensures that all traffic entering or leaving the network passes through it, adding a crucial layer of security.


![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/firewall.png>)



### Function

Its job is to scrutinize all data packets, permitting or denying traffic based on the network's security policies, effectively protecting the network from potential threats.

---

## Demilitarized Zone (DMZ)

A **DMZ** in a network diagram is typically placed **between the internal protected network (LAN) and an external network** (most frequently the Internet). It acts as an additional protective layer, hosting services that communicate with external networks, thus isolating them from the internal, more secure network.

### Placement

Its graphical representation sits **between the internal network router and the external-facing router**, creating a buffer zone.

> This architecture reduces the risk of an outside security threat reaching the core components of the internal network.


![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/dmz.png>)

### Systems Typically Hosted in the DMZ

| System                 | Purpose                                                   |
| ---------------------- | --------------------------------------------------------- |
| **Web Server**   | Delivers web pages to users who request them via browsers |
| **Email Server** | Manages incoming and outgoing mail                        |
| **DNS Server**   | Translates domain names into IP addresses                 |
| **FTP Server**   | Facilitates file transfers                                |
| **VPN Server**   | Provides remote network access                            |

> By isolating these servers in the DMZ, organizations seek to limit potential damage from external threats, as these are the systems that primarily interact with the internet and are thus more exposed.

---

## Intrusion Detection System (IDS)

An **IDS** in a network diagram is often situated at **critical points** where it can monitor and analyze traffic to and from all devices on the network.

### Placement

Typically, the IDS is positioned **behind the firewall before the network switch** to examine internal traffic for any anomalies or patterns that indicate a possible intrusion.

> Multiple IDS may be used and placed at various entry and exit points in more extensive networks to maximize coverage and protection.


![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/ids.png>)

### Function

The IDS enhances a network's security by providing an **additional layer of detection** beyond the firewall and DMZ, potentially identifying and alerting to threats that other security measures may have missed.

---

## Wireless Router

A **wireless router** is typically situated at a **strategic point** in a network diagram. This device serves as both a **router** and a **wireless access point**.

### Functions

- Connects wired networks to wireless devices
- Connects the internal network to external networks like the internet
- Extends network access to devices that may not be physically wired into the network
- Enables wireless devices to communicate and share data with other devices on the network
  
![alt text](<../Labs/Analyze recent security threat reports using X-Force Threat Exchange/Screenshots/wireless_router.png>)


> Its position in the diagram reflects its critical role in managing and facilitating both wired and wireless communications within the network.
>

