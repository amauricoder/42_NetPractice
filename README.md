# 42_NetPractice
his document is a System Administration related exercise.

## How to Calculate the Range in a Network

To calculate the **range** of a network (i.e., the range of valid IP addresses), you need two main pieces of information: the **IP address** and the **subnet mask**. Let’s use the example you provided, with the IP `104.99.23.240` and the subnet mask `255.255.255.0`.

### Steps to Calculate the Network Range:

#### 1. **Identify the Network and Host Portions:**
   The subnet mask `255.255.255.0` (or `/24` in CIDR notation) indicates that the first **24 bits** of the IP are for the **network**, and the last **8 bits** are for the **hosts**.

   - **IP in decimal**: `104.99.23.240`
   - **Subnet mask in decimal**: `255.255.255.0`
   - **IP in binary**: `01101000.01100011.00010111.11110000`
   - **Mask in binary**: `11111111.11111111.11111111.00000000`

   The subnet mask `255.255.255.0` means that the first three octets (`104.99.23`) represent the **network**, and the last octet (`240`) represents the **hosts**.

#### 2. **Find the Network Address:**
   The **network address** is obtained by performing a bitwise AND operation between the IP address and the subnet mask.

   - **IP in binary**: `01101000.01100011.00010111.11110000`
   - **Mask in binary**: `11111111.11111111.11111111.00000000`

   Performing the AND operation:

- 01101000.01100011.00010111.11110000 (IP)
- AND
- 11111111.11111111.11111111.00000000 (Máscara)
- 01101000.01100011.00010111.00000000 (Resultado: 104.99.23.0)


Therefore, the **network address** is `104.99.23.0`.

#### 3. **Find the Broadcast Address:**
The **broadcast address** is the last address in the network and is obtained by setting all the **host bits** to 1.

- For a `/24` mask, the first 24 bits are for the network and the last 8 bits are for hosts.
- The host portion in the broadcast address will be `11111111` (in binary), which is `255` in decimal.

Therefore, the **broadcast address** is:
- **Broadcast address**: `104.99.23.255`.

#### 4. **Calculate the Usable IP Range:**
The range of valid IP addresses (hosts) goes from the first IP **after the network address** to the last IP **before the broadcast address**.

- **First usable IP**: `104.99.23.1` (the next address after `104.99.23.0`).
- **Last usable IP**: `104.99.23.254` (the address before the broadcast `104.99.23.255`).

### Summary of Results:

- **Network address**: `104.99.23.0`
- **Broadcast address**: `104.99.23.255`
- **Usable IP range**: from `104.99.23.1` to `104.99.23.254`

Thus, with the IP `104.99.23.240` and the subnet mask `255.255.255.0`, the range of usable IPs goes from `104.99.23.1` to `104.99.23.254`.


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
- Interface R1 and R2 have locked ips and masks.

## Goal 1 : host Machine A needs to communicate with host The Mighty Router

---

## Goal 2 : host Machine B needs to communicate with host The Mighty Router

---

Goal 3 : host Machine A needs to communicate with host Machine B 

--


