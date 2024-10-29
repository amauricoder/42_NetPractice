# 42_NetPractice

This project involves configuring small networks. The document provides a concise explanation of how each exercise was solved.

## Table of contents
- [How to Use This Document](#how-to-use-this-document)
- [Exercise 1](#exercise-1)
- [Exercise 2](#exercise-2)
- [Exercise 3](#exercise-3)
- [Exercise 4](#exercise-4)
- [Exercise 5](#exercise-5)
- [Exercise 6](#exercise-6)
- [Exercise 7](#exercise-7)
- [Exercise 8](#exercise-8)
- [Exercise 9](#exercise-9)
- [Exercise 10](#exercise-10)
- [License](#license)


## How to Use This Document

To fully understand the explanations, please refer to the resources listed below. These materials provide essential background knowledge in subnetting, network concepts, and configuration techniques.

### Recommended Resources

1. **[You Suck at Subnetting - Playlist](https://www.youtube.com/watch?v=5WfiTHiU4x8&list=PLIhvC56v63IKrRHh3gvZZBAGvsvOhwrRF)**  
   Created by [NetworkChuck](https://www.youtube.com/@NetworkChuck)  
   This playlist offers a hands-on, beginner-friendly approach to subnetting concepts.

2. **[Redes - Playlist (Portuguese)](https://www.youtube.com/watch?v=dp9ynjJamoI&list=PLuf64C8sPVT_nObvAFU5W-SiE04ST-PlL&pp=iAQB)**  
   Created by [Paulo Kretcheu](https://www.youtube.com/@kretcheu2001)  
   This playlist covers networking fundamentals in Portuguese, making it a great resource for Portuguese speakers.

3. **[A Computer Networking Zine](https://jvns.ca/networking-zine.pdf)**  
   By [Julia Evans](https://jvns.ca/)  
   This zine provides a fun and visual approach to learning networking concepts, perfect for beginners and visual learners.

4. **[Comprehensive Repository of Networking Concepts and Resources](https://github.com/zelhajou/42cursus-net_practice)**  
   Created by [Zakaria Elhajoui](https://github.com/zelhajou)  
   This repository includes an extensive collection of networking concepts and additional resources, making it an excellent reference for network practice.

---

Thank you to all the creators for contributing to the community and sharing knowledge.


## Exercise 1

![Exercise 1](images/1.png)

## Goal 1 : host my PC needs to communicate with host my little brother's computer

### Network Information:
- **Hosts A and B** are on the same network.
- The subnet masks are pre-filled and locked.

### Subnet Mask Details:
- **Subnet Mask (Decimal):** `255.255.255.0`
- **Subnet Mask (Binary):** `11111111.11111111.11111111.00000000`
- **CIDR Notation:** `/24`

### Explanation:
- The first **24 bits** (3 bytes) represent the **network portion**.
- The last **8 bits** (1 byte) represent the **host portion**.

Since both hosts are on the same network, there is no need to change the subnet mask.

### IP Address Range:
- **Usable IP Range:** `104.96.23.1` to `104.96.23.254`
- **Exception:** `104.96.23.12` is already assigned to **Client B1**.

### Important Notes:
- The first address in the range, `104.96.23.0`, is reserved as the **network address**.
- The last address in the range, `104.96.23.255`, is reserved as the **broadcast address**.

---

## Goal 2 : host my Mac needs to communicate with host my little sister's computer

### Network Information:
- **Hosts C and D** are on the same network.
- The subnet masks are pre-filled and locked.

### Subnet Mask Details:
- **Subnet Mask (Decimal):** `255.255.0.0`
- **Subnet Mask (Binary):** `11111111.11111111.00000000.00000000`
- **CIDR Notation:** `/16`

### Explanation:
- The first **16 bits** (2 bytes) represent the **network portion**.
- The last **8 bits** (2 bytes) represent the **host portion**.

Now, the subnet mask is 255.255.0.0 - In this case, the first 2 octects(2 bytes) will represent the network and the other 2 will represent the host.
Since both hosts are on the same network, there is no need to change the subnet mask.
Because the have the last 2 bits for the hosts, the range for hosts will be bigger.

### IP Address Range:
- **Usable IP Range:** `211.191.1.0` to `211.191.255.254`
- **Exception:** `211.191.31.75` is already assigned to **Client C1**.
- Here we are already having in consideration the network and broadcast.

---

## Exercise 2

![Exercise 2](images/2.png)

## Goal 1 : host Computer B needs to communicate with host Computer A

### Network Information:
- Host B and host A are on the same network
- Subnet Mask of host A is filled and locked.

### Subnet Mask Details:
- **Subnet Mask (Decimal):** `255.255.255.224`
- **Subnet Mask (Binary):** `11111111.11111111.11111111.11100000`
- **CIDR Notation:** `/27`

### Explanation:
- The first **27 bits** represent the **network portion**.
- The last **5 bits** represent the **host portion**.
- This allows for 32 IP addresses per subnet (since 2^5 = 32).

- The subnet mask of the host A is filled and locked.
- The ip of host B is filled and locked with ip **192.168.28.222 (11000000.10101000.00011100.11011110)**
Since hosts B and A are on the same network, the subnet mask will be the name for both.
Since we know that we can change only the last 5 bits for the hosts and this subnet mask allows 32 hosts,
we can calculate the range as:

| **Network Address** | **Broadcast Address** | **Usable IP Range**                |
|---------------------|-----------------------|------------------------------------|
| 192.168.28.0        | 192.168.28.31         | 192.168.28.1 - 192.168.28.30       |
| 192.168.28.32       | 192.168.28.63         | 192.168.28.33 - 192.168.28.62      |
| 192.168.28.64       | 192.168.28.95         | 192.168.28.65 - 192.168.28.94      |
| 192.168.28.96       | 192.168.28.127        | 192.168.28.97 - 192.168.28.126     |
| 192.168.28.128      | 192.168.28.159        | 192.168.28.129 - 192.168.28.158    |
| 192.168.28.160      | 192.168.28.191        | 192.168.28.161 - 192.168.28.190    |
| **192.168.28.192**  | **192.168.28.223**    | **192.168.28.193 - 192.168.28.222**|

### IP Address Range:
- **Usable IP Range:** `192.168.28.193` to `192.168.28.221`
- **Network address**: `192.168.28.192`
- **Broadcast address:** `192.168.28.223`
- **Exception:** `192.168.28.222` is already assigned to **Host B**.

## Goal 2 : host Computer D needs to communicate with host Computer C

### Network Information:
- Host D and host C are on the same Network
- SubnetMask are already filled on both. They are the same, but in different representations.

### Subnet Mask Details:
- **Subnet Mask (Decimal):** - 255.255.255.252.
- **Subnet Mask (Binary):** - `11111111.11111111.11111111.11111100`
- **CIDR Notation:** - /30

### Explanation:
- The first **30 bits** represents the network. The last **2 bits** represents the hosts.
- This allows for 4 IP addresses per subnet (since 2^2 = 4).
- Since the IP address 127.0.0.1 is reserved. It is known as the loopback address, and the mask that is a Class C mask, we will work with the 192.168.28.x ips.

### IP Address Range:

| **Network Address** | **Broadcast Address** | **Usable IP Range**                |
|---------------------|-----------------------|------------------------------------|
| **192.168.28.0**    | **192.168.28.3**      | **192.168.28.1 - 192.168.28.2**    |
| 192.168.28.4        | 192.168.28.7          | 192.168.28.33 - 192.168.28.62      |
| 192.168.28.8        | 192.168.28.11         | 192.168.28.65 - 192.168.28.94      |
| and there goes      | and there goes        | and there goes                     |
| 192.168.28.252      | 192.168.28.255        | 192.168.28.253 - 192.168.28.254    |

### IP Address Range:
- **Usable IP Range:** `192.168.28.1` to `192.168.28.2`
- **Network address**: `192.168.28.0`
- **Broadcast address:** `192.168.28.3`

---

## Exercise 3
![Exercise 3](images/3.png)

This exercise introduces us to the usage of a switch. 
This device links multiple hostsof the same network together.

### Network Information:
- Host A, host B and Host C are on the same network
- The Mask of Host C is filled and locked.
- The Host A ip is filled and locked.

With this information, we know that all the masks will be the same 
and we are also able to calculate the range of the ips.

### Subnet Mask Details:
- **Subnet Mask (Decimal):** - `255.255.255.128`
- **Subnet Mask (Binary):** - `11111111.11111111.11111111.10000000`
- **CIDR Notation:** - /25

### Explanation:
- The first **25 bits** represents the network. The last **7 bits** represents the hosts.
- This allows for 128 IP addresses per subnet (since 2^7 = 128).

## IP Range
- **Ip filled and locked** - `104.198.253.125`
- **Binary Representation** - `01101000.11000110.11111001.01111101`


### IP Address Range:

| **Network Address** | **Broadcast Address** | **Usable IP Range**                  |
|---------------------|-----------------------|--------------------------------------|
| **104.198.253.0**   | **104.198.253.127**   | **104.198.253.1 - 104.198.253.126**  |

### IP Address Range:
- **Usable IP Range:** `104.198.253.1` to `104.198.253.126`
- **Network address**: `104.198.253.0`
- **Broadcast address:** `104.198.253.127`

We need to fill all three ips inside this range, without repeating and the exercise is solved.

## Exercise 4
![Exercise 4](images/4.png)

This exercise introduces the router.
This device is used to link multiple networks together, it does so with the use of multiple interfaces.

### Network Information:
- Masks are not filled on Host A and Host B and they are on the same network, so we can chose. I will chose something easy. 255.255.255.0 -> /24 in CIDR notation.
- Host A have an IP filled and locked (**79.55.118.132**).
- Interfaces R3 and R2 have all the informations locked.
- Interface R1 have submask and ip free to chose.

Since we can chose the mask, i will chose and easy one that doesnt recquire any calculations.
for the mask /24, we know that the range will be 79.55.118.1 to 79.55.118.254(having in consideration that the first and the last are reserved).
The IP address of Host B and Interface R1 must have the same network address as the IP address of Interface A1 and the same submask.

Fill all three with the same Mask and in the IP range described above and the exercise is solved.
We don't touch on Interface R2 and R3 because none of our communications have to reach that side of the router.

---

## Exercise 5

![Exercise 5](images/5.png)

This exercise introduces the concept of **routes** in networking.

What is a Route?
   A **route** is a set of instructions used by routers to determine how to send packets from one network to another. When data needs to travel across networks, it follows these routes to reach its intended destination.

Components of a Route:
   A route consists of two key fields:

1. Destination
- The **destination** is the address of the endpoint where the data is intended to go. It can refer to a specific device (such as a computer or server) or a broader network.
- **Example:** If you're sending data to a website, the destination would be the IP address of that website.
The destination default is equivalent to 0.0.0.0 /0, this will forward the packets to the first applicable network address it finds. For instance, if the destination address is 123.4.5.6/24, the packets will be directed to the network 123.4.5.0.

2. Next Hop
- The **next hop** specifies the next router (or internet or device) that should receive the packets on their way to the destination.
- This field is crucial for routing as it determines the immediate path the packets will take.
- **Example:** If the destination is on a different network, the packet may first be sent to a local router (the next hop), which then forwards it to the appropriate network.


## Network information
- interfaces A1 and B1 ips and masks have open field to change the values.
- Host A routes have destination and next hop open fields to change the values.
- Host B routes have destination filled as default and lock and next hop field open to change the value.
- Interface R1 and R2 have locked ips and masks.

## Goal 1 : host Machine A needs to communicate with host The Mighty Router

To make the host Machine A to communicate with the Mighty Router, we need to check in which interface of the router we are in touch. In this case, is the interface R1.

Interface R1 have the Ip and submask fields filled and locked.
The mask is 255.255.255.128 -> /25 in CIDR notation.
The ip is 45.227.104.126.

With this informations we know that Machine A needs to have the same mask as interface R1 and the IP needs to be inside the range of R1 ips.

We also can know that the number of hosts on the network is 128. Because 2^7 = 128.
Then, the range is 45.227.104.1 - 45.227.104.126 (Having in consideration the hosts and broadcast)

Host A route
We can define the destination as default, because there is only 1 route through which it can send its packets.
The next hop address must be the IP address of the next router's interface on the packets' way.
The next interface is Interface R1, with the IP address of 54.117.30.126. Note that the next interface is not Interface A1, since this is the sender's own interface.

Doing this, we will solve this goal.

---

## Goal 2 : host Machine B needs to communicate with host The Mighty Router

We will use the same logic as the exercise before.
Interface R2 Has IP and Mask filled and locked.
The mask is 255.255.192.0 -> /18 in CIDR notation.
The IP is 170.71.188.254.

With this informations we know that Machine B needs to have the same mask as interface R2 and the IP needs to be inside the range of R2 ips.

We also can know that the number of hosts on the network is 128. Because 2^6 = 64.
Then, the range is 170.71.188.193 - 170.71.188.254 (Having in consideration the hosts and broadcast).

Host B route
The destination is already filled with default.
The next hop address must be the IP address of the next router's interface on the packets' way.
The next interface is Interface R2, with the IP address of 170.71.188.254. Note that the next interface is not Interface B1, since this is the sender's own interface.

Doing this, we will solve this goal.

---

Goal 3 : host Machine A needs to communicate with host Machine B 
Solving the 2 first goals will allow the communications between Machine A and Machine B.

--

## Exercise 6

![Exercise 6](images/6.png)

This exercise introduces internet.
The internet operates similarly to a router, directing data between devices and networks. However, certain IP addresses are reserved for private use and cannot be used on the public internet. Here are the key ranges of reserved IP addresses:

      192.168.0.0 - 192.168.255.255: This range includes 65,536 IP addresses and is commonly used in home networks.

      172.16.0.0 - 172.31.255.255: This range provides 1,048,576 IP addresses and is often utilized by medium-sized networks.

      10.0.0.0 - 10.255.255.255: This range offers 16,777,216 IP addresses and is frequently employed in larger networks.

If a device's interface is connected to the internet, it **cannot** use these private IP addresses. Instead, it must use a public IP address to communicate over the internet.

## Network information
### internet
- destination -> changeble.
- next hop -> 163.172.250.12

### interface R2
- ip -> 163.172.250.12
- submask -> 255.255.255.240 -> CIDR /28

### router R
- destination -> changeble
- next hop -> 163.172.250.1

### interface R1
- ip -> Changeble
- submask -> 255.255.255.128 -> CIDR /25

### interface A1
- ip -> 112.156.244.227
- mask -> changeble

### Host A route
- destination -> changeble
- next hop -> changeble

Next hop of internet is already locked and filled, and matches it ip from interface R2.
Then we need to configurate the destination of the internet, that in this case we need to send packages to host A.
So, internet destination must match with the network of address of interface A1.
A1 mask is changeble, than we can fill this with some easy calculation mask. 255.255.255.0 -> /24 -> This will give us a range of 255.

Calculate internet address of a client:
To calculate this, we need to transform the Interface A1 ip and mask to binary.

`ip 112.156.244.227 -> 01110000.10011100.11110100.11100011`

`mask 255.255.255.0 -> 11111111.11111111.11111111.00000000`

Apply the Subnet Mask to the IP Address

To find the **network address**, apply the subnet mask to the IP address using a bitwise **AND** operation.

    1 AND 1 = 1
    1 AND 0 = 0
    0 AND 1 = 0
    0 AND 0 = 0

| **IP Address**        | `01110000.10011100.11110100.11100011` |
|-----------------------|--------------------------------------|
| **Subnet Mask**        | `11111111.11111111.11111111.00000000` |
| **Network Address**    | `01110000.10011100.11110100.00000000` |

#### 3. Convert the Result to Decimal (Network Address)

Convert the binary result back to decimal:

- `01110000` -> 112
- `10011100` -> 156
- `11110100` -> 244
- `00000000` -> 0

So, the **network address** (internet address of the client) is: **112.156.244.0**.

#### 4. Possible Host Addresses

Since we are using a `/24` subnet mask (255.255.255.0), there are 8 bits left for the host portion, allowing for a range of host addresses from **112.156.244.1** to **112.156.244.254**. 
- The first address `112.156.244.0` is the **network address**.
- The last address `112.156.244.255` is the **broadcast address**.

Now, we need to finish configuring the routes.
All the destinations (except for internet) will be the default.
Host A next hop will be the next interface ip (R1).

## Exercise 7

![Exercise 7](images/7.png)

This level introduces us to the concept of overlaps.
Network overlap occurs when two or more IP address ranges (or subnets) share common addresses. This means that devices in different networks could have IP addresses that fall within the same range, leading to confusion for routers on how to properly route traffic. Essentially, an overlap happens when networks aren't correctly separated, causing ambiguity in IP assignments and routing.
The IP address range of one network should not mix or share any addresses with the range of another network. These networks are kept apart by routers, which help manage and direct traffic between them. If the address ranges overlap, the router won't be able to clearly distinguish which network to send the data to.

## Network information
- 3 seperate networks
- Host A to Router R1
- Router R1 to Router R2
- Router R2 to Host C

- Interface R11 is alread filled with IP 93.198.14.1, because of this, we can't fill freely chose interface A1 ip.
Now, imagine that we give a 255.255.255.0 /024 mas to A1 ip. Lets see the range:

### Subnet Mask Details:
- **Subnet Mask (Decimal):** - 255.255.255.0
- **Subnet Mask (Binary):** - `11111111.11111111.11111111.00000000`
- **CIDR Notation:** - /30
- **Hosts** - 255 (w/ host and broadcast)

| **Network Address** | **Broadcast Address** | **Usable IP Range**                |
|---------------------|-----------------------|------------------------------------|
| 93.198.14.0         | 93.198.14.255         | 93.198.14.1 - 93.198.14.254        |

The IP of interface R12 is **93.198.14.254** and is filled and locked.
So, because of this, we can't use a mask of /24, because it will overlap the range of interface R12.
They would be both in the range of 93.198.14.0 - 93.198.14.255.
Since we need IP addresses for 3 different networks, it's useful to divide the last part of the address into 4 or more smaller address groups. We achieve this by applying a subnet mask of /26 or greater. 
For example, a /28 mask will create 16 smaller groups of addresses, and from these, we will use 3 specific ranges.

### Subnet Mask Details:
- **Subnet Mask (Decimal):** - 255.255.255.0
- **Subnet Mask (Binary):** - `11111111.11111111.11111111.11110000`
- **CIDR Notation:** - /28
- **Hosts** - 16 (w/ host and broadcast)

      93.198.14.1 - 93.198.14.14    (Host A to Router R1)
      93.198.14.65 - 93.198.14.78   (Router R2 to Host C)
      93.198.14.241 - 93.198.14.254 (Router R1 to Router R2)

Useful link
https://www.calculator.net/ip-subnet-calculator.html?cclass=any&csubnet=28&cip=93.198.14.2&ctype=ipv4&printit=0&x=97&y=13

## Exercise 8

![Exercise 8](images/8.png)

## Network information
- Cliente D and Client C needs to communicate between each other and to the internet.
- We have the destiny of the internet filled and locked with ip 131.79.51.0 mask /26

With this information, we can know that all networks must have 131.79.51.x with the range of 62 hosts(excluding network and broadcast)
Then, we know that the internet will communicate with networks with the range of 131.79.51.0 to 131.79.51.63;
But, we need to be careful for not occuring overlaps between the networks.
- Interface D1 has the mask filled and locked 255.255.255.240 /28 , this told us that the networks can have 14 hosts(excluding network and broadcast).

Knowing all this information, we know that the mask is manipulated and the network is splitted in 4.
All the ips are between the range and we need to put any network in a range:

|split| **Network Address** | **Broadcast Address** | **Usable IP Range**                |
|------|---------------------|-----------------------|------------------------------------|
|Host D to router| 131.79.51.0         | 131.79.51.15          | 131.79.51.1 - 131.79.51.14         |
|HOST C to router| 131.79.51.16        | 131.79.51.31          | 131.79.51.17 - 131.79.51.30        |
|router to router| 131.79.51.32        | 131.79.51.63          | 131.79.51.33 - 131.79.51.62        |
|not used| 131.79.51.64        | 131.79.51.128         | 131.79.51.65 - 131.79.51.127       |

- interface R12 ip is filled and locked. With this information we have the next hop of internet.

Now all that we have to do is fill the networks with valid ips from the equivalent range.
All the routes will be default(except for one) and the next hop will be the next interface, just like the other exercises.
- the route from R1 needs to have a destination defined to the specific network that we want to send the packages, that is 131.79.51.0/24.

## Exercise 9

![Exercise 9](images/9.png)

## Network information
Internet initially does not send packages to any specific network.
The networks does not share a common addres range.
For this reason, this exercise is very easy.

The easiest way is to solve it goal by goal.
#### Goal 1 : host meson needs to communicate with host ion
- All the hosts needs to have the same subnet mask. We have one field locked and filled, then we share this
subnet mask between all the hosts.
- All the destinations can be set to default.
- Then, we can choose a reasonable ip to this network and just change the host number.

#### Goal 2 : host cation needs to communicate with host gluon
- between gluon and the router, there is a mask filled and locked. We can share this to the other host on the network.
- On gluon, we have algo the next hop filled and locked, then we know the ip that we need to have on the next interface. With this information, we can algo calculate the network range of the other host.
- The destination on gluon can be setted to default
- The R2, we need to put the next hop that is the next interface. For this, we can also chose an IP.
- between cation and the router, we basically can define anything. Then you can chose something easy that won't 
require any calculations.

#### Goal 3 : host meson needs to communicate with host Internet
- Just put the ip that you choose initially and put it as destination on internet.
There is no need to calculate this, just put the ip open to all (ip.0/24). But if you want to
calculate the network, you can do it by doing an AND bitwise operation.

#### Goal 4 : host meson needs to communicate with host gluon
- Meson network is already configured.
- Then, we need to configure the path between meson to gluon.
- Between interface R13 and R21, we have a submask filled and locked. We know that they need to have the same subnet mask, then we share between them. Doing this, we can chose the ip. We know that the range will be
very short, because this is a mask .252. Then, we can chose and easy ip based on this information and our knowledge.

#### Goal 5 : host ion needs to communicate with host cation
- Configure the router R1 next hop with the next interface and the destination with the network address of the cation network. 

#### Goal 6 : host cation needs to communicate with host Internet
- Configure the internet next hop with the next interface and the destination with the network address of the cation network. 

## Exercise 10

![Exercise 10](images/10.png)

# Network Configuration Explanation

At this level, we have 4 distinct network connections:

1. **Router R1 to Switch S1**
2. **Router R1 to Router R2**
3. **Router R2 to Client H4**
4. **Router R2 to Client H3**

## Step 1: Ensuring Internet Access to All Hosts
The internet needs to reach all hosts, so its destination IP range should encompass all networks in the setup.

Interfaces R11 and R13 already have assigned IPs, differing only in the last byte: Interface R11 ends in `.1`, while R13 ends in `.254`. To include this full IP range, we use a `/24` subnet mask for the internet destination, covering `134.97.142.0` to `134.97.142.255`.

## Step 2: Choosing IP Ranges for Each Network
When assigning IP addresses, two criteria are essential:

1. The IP address must fall within the internet’s destination range.
2. The IP ranges for each network should not overlap.

Given the existing IP assignments (grayed out), here’s a breakdown of the ranges covered by each network:

- **Router R1 to Switch S1:** Range `134.97.142.0 - 134.97.142.127` (using a `/25` mask)
- **Router R2 to Client H4:** Range `134.97.142.128 - 134.97.142.191` (using a `/26` mask)
- **Router R1 to Router R2:** Range `134.97.142.252 - 134.97.142.255` (using a `/30` mask)
- **Router R2 to Client H3:** Currently unassigned (needs a specific mask)

For the "Router R2 to Client H3" connection, we have the remaining IP range `134.97.142.192 - 134.97.142.251`. Any mask allowing two IPs within this range can be applied for Interface R22 and Interface R31.

## License
[View License](LICENSE)