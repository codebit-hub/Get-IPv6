# Get-IPv6

A practical IPv6 subnetting cheat sheet.

The purpose of this project is to understand how IPv6 addressing and subnetting work, especially the parts that are different from IPv4 subnetting.

The main goal is to have a quick reference that can be used when manually calculating IPv6 subnets, prefix lengths, hexadecimal increments, and hierarchical subnet structures.

---

## Objective

The main objectives of this project are:

* Understand the structure of an IPv6 address.
* Understand IPv6 prefix lengths.
* Understand the relationship between:

  * Routing Prefix
  * Subnet ID
  * Interface ID
* Learn how IPv6 subnetting differs from IPv4 subnetting.
* Learn how to calculate the number of subnet bits required.
* Learn how to calculate the hexadecimal increment between consecutive subnets.
* Learn how to perform IPv6 subnetting manually without a subnet calculator.
* Learn how to divide the 16-bit Subnet ID hierarchically.
* Build a compact reference that can be used when solving IPv6 networking exercises.

---

## Subnetting Cheat Sheet

| **Bit**     |  **16** | **15** | **14** | **13** | **12** | **11** | **10** |  **9** |  **8** |  **7** |  **6** |  **5** |  **4** |  **3** |  **2** |  **1** |  **0** |
| ----------- | ------: | -----: | -----: | -----: | -----: | -----: | -----: | -----: | -----: | -----: | -----: | -----: | -----: | -----: | -----: | -----: | -----: |
| **Decimal** |   65536 |  32768 |  16384 |   8192 |   4096 |   2048 |   1024 |    512 |    256 |    128 |     64 |     32 |     16 |      8 |      4 |      2 |      1 |
| **Hex**     | `10000` | `8000` | `4000` | `2000` | `1000` |  `800` |  `400` |  `200` |  `100` |   `80` |   `40` |   `20` |   `10` |    `8` |    `4` |    `2` |    `1` |
| **CIDR**    |     `-` | `/113` | `/114` | `/115` | `/116` | `/117` | `/118` | `/119` | `/120` | `/121` | `/122` | `/123` | `/124` | `/125` | `/126` | `/127` | `/128` |
| **CIDR**    |     `-` |  `/97` |  `/98` |  `/99` | `/100` | `/101` | `/102` | `/103` | `/104` | `/105` | `/106` | `/107` | `/108` | `/109` | `/110` | `/111` | `/112` |
| **CIDR**    |     `-` |  `/81` |  `/82` |  `/83` |  `/84` |  `/85` |  `/86` |  `/87` |  `/88` |  `/89` |  `/90` |  `/91` |  `/92` |  `/93` |  `/94` |  `/95` |  `/96` |
| **CIDR**    |     `-` |  `/65` |  `/66` |  `/67` |  `/68` |  `/69` |  `/70` |  `/71` |  `/72` |  `/73` |  `/74` |  `/75` |  `/76` |  `/77` |  `/78` |  `/79` |  `/80` |
| **CIDR**    |     `-` |  `/49` |  `/50` |  `/51` |  `/52` |  `/53` |  `/54` |  `/55` |  `/56` |  `/57` |  `/58` |  `/59` |  `/60` |  `/61` |  `/62` |  `/63` |  `/64` |
| **CIDR**    |     `-` |  `/33` |  `/34` |  `/35` |  `/36` |  `/37` |  `/38` |  `/39` |  `/40` |  `/41` |  `/42` |  `/43` |  `/44` |  `/45` |  `/46` |  `/47` |  `/48` |
| **CIDR**    |     `-` |  `/17` |  `/18` |  `/19` |  `/20` |  `/21` |  `/22` |  `/23` |  `/24` |  `/25` |  `/26` |  `/27` |  `/28` |  `/29` |  `/30` |  `/31` |  `/32` |
| **CIDR**    |     `-` |   `/1` |   `/2` |   `/3` |   `/4` |   `/5` |   `/6` |   `/7` |   `/8` |   `/9` |  `/10` |  `/11` |  `/12` |  `/13` |  `/14` |  `/15` |  `/16` |

Important links:
1. https://www.youtube.com/@itfreetraining/search?query=ipv6
2. https://www.youtube.com/watch?v=UIGVPvxnCtk
3. https://www.youtube.com/watch?v=KSiZ751-Zs8&pp=0gcJCRsMAYcqIYzv

---

## Important IPv6 Prefixes

| Prefix           | Meaning                       |
| ---------------- | ----------------------------- |
| `::/128`         | Unspecified                   |
| `::1/128`        | Loopback                      |
| `2000::/3`       | Global Unicast                |
| `2001:db8::/32`  | Documentation                 |
| `fc00::/7`       | Unique Local                  |
| `fd00::/8`       | Locally assigned Unique Local |
| `fe80::/10`      | Link-Local                    |
| `ff00::/8`       | Multicast                     |
| `2002::/16`      | 6to4                          |
| `2001:0000::/32` | Teredo                        |

For learning and documentation, the following prefix is particularly useful:

```text
2001:db8::/32
```

It is reserved for documentation and examples.

---

## Quick Recognition Table

When looking at the beginning of an IPv6 address:

```text
2000::/3       → Global Unicast
fd00::/8       → Unique Local
fe80::/10      → Link-Local
ff00::/8       → Multicast
::1            → Loopback
::             → Unspecified
2001:db8::     → Documentation/example
```

---

# 1. IPv6 Address Basics

An IPv6 address is **128 bits** long.

It consists of:

* 8 groups
* Each group contains 16 bits
* Each group is written as 4 hexadecimal digits

Therefore:

```text
8 × 16 = 128 bits
```

Example:

```text
2001:0db8:0000:0000:0000:0000:0000:0001
```

Each hexadecimal digit represents **4 bits**:

```text
1 hexadecimal digit = 4 bits
1 hextet = 4 hexadecimal digits = 16 bits
8 hextets = 128 bits
```

---

# 2. Hexadecimal Cheat Sheet

IPv6 subnetting becomes much easier when hexadecimal values are understood in binary.

## Hexadecimal to Binary

- Count 2^:  3210
- Bit value:     8421

| Hex | Binary | Decimal |
| --: | :----: | ------: |
|   0 | `0000` |       0 |
|   1 | `0001` |       1 |
|   2 | `0010` |       2 |
|   3 | `0011` |       3 |
|   4 | `0100` |       4 |
|   5 | `0101` |       5 |
|   6 | `0110` |       6 |
|   7 | `0111` |       7 |
|   8 | `1000` |       8 |
|   9 | `1001` |       9 |
|   A | `1010` |      10 |
|   B | `1011` |      11 |
|   C | `1100` |      12 |
|   D | `1101` |      13 |
|   E | `1110` |      14 |
|   F | `1111` |      15 |

The most important relationship to remember:

```text
1 hexadecimal digit = 4 bits
```

For example:

```text
C = 1100
A = 1010
9 = 1001
```

Therefore:

```text
CA9 = 1100 1010 1001
```

---

# 3. IPv6 Address Abbreviation

An IPv6 address can be written in several equivalent forms.

Full form:

```text
F00D:CAFE:0000:0000:0000:0000:0000:0001
```

Leading zeros in each hextet can be removed:

```text
F00D:CAFE:0:0:0:0:0:1
```

A consecutive sequence of zero hextets can be replaced with `::`:

```text
F00D:CAFE::1
```

The `::` abbreviation can be used **only once** in an address.

Correct:

```text
FF:0:0:0:1:0:0:1
FF::1:0:0:1
FF:0:0:0:1::1
```

Incorrect:

```text
FF::1::1
```

The reason is that `::` represents an unspecified number of zero hextets, so using it twice would make the address ambiguous.

According to RFC 5952, when multiple sequences of zero hextets are possible, the **longest sequence** should be compressed.

---

# 4. IPv6 Address Structure

For a typical IPv6 global unicast network, the 128 bits can be viewed as:

```text
|<----------- 64 bits ----------->|<----------- 64 bits ----------->|
|         Network Prefix          |          Interface ID           |
```

A commonly used structure is:

```text
|<------ 48 bits ------>|<-- 16 bits -->|<------ 64 bits ------>|
|    Routing Prefix     |   Subnet ID   |     Interface ID      |
```

Therefore:

```text
Routing Prefix + Subnet ID = Network Prefix
```

or:

```text
Network Prefix = Prefix
```

A typical `/64` network therefore looks like:

```text
2001:db8:cad:1234::/64
```

where:

```text
2001:db8:cad       = Routing Prefix
1234               = Subnet ID
remaining 64 bits  = Interface ID
```

This **48 + 16 + 64** model is the most useful model for manual IPv6 subnetting exercises.

> Note: Actual allocations can use different prefix lengths. The 48-bit routing prefix and 16-bit Subnet ID model is a common organizational model and is the model used throughout this cheat sheet.

---

# 5. Why IPv6 Subnetting Looks Different from IPv4

In IPv4, subnetting often means borrowing bits from the host portion:

```text
Network | Subnet | Hosts
```

IPv6 has an enormous address space, so subnetting is normally approached differently.

A common allocation is:

```text
/48 → organization
/64 → individual LAN
```

This leaves:

```text
64 - 48 = 16 bits
```

for subnetting.

Those 16 bits can provide:

```text
2^16 = 65,536 subnets
```

while still leaving the final 64 bits for Interface IDs.

This is why IPv6 subnetting is often less about calculating individual host addresses and more about **allocating the 16-bit Subnet ID**.

---

# 6. The 16-Bit Subnet ID

Suppose an ISP delegates:

```text
2001:db8:cad::/48
```

The first 48 bits are already fixed.

The next 16 bits are available for subnetting:

```text
2001:db8:cad:0000::/64
              ^^^^
              Subnet ID
```

The Subnet ID is one complete 16-bit hextet.

Therefore it can contain:

```text
0000
0001
0002
...
FFFF
```

Number of possible values:

```text
2^16 = 65,536
```

So:

```text
2001:db8:cad:0000::/64
2001:db8:cad:0001::/64
2001:db8:cad:0002::/64
...
2001:db8:cad:ffff::/64
```

represent 65,536 possible `/64` subnets.

---

# 7. The Most Important Subnetting Formula

When dividing the 16-bit Subnet ID hierarchically, divide its bits into three categories:

```text
f = fixed / already allocated bits
s = subnet bits allocated at the current level
r = remaining / unallocated bits
```

The total is always:

```text
f + s + r = 16
```

This is one of the most useful formulas for manual IPv6 subnetting.

---

# 8. How Many Bits Do I Need?

The number of subnet combinations is:

```text
Number of subnets = 2^s
```

Therefore:

| Required subnets | Bits required |
| ---------------: | ------------: |
|                2 |             1 |
|                4 |             2 |
|                8 |             3 |
|               16 |             4 |
|               32 |             5 |
|               64 |             6 |
|              128 |             7 |
|              256 |             8 |
|              512 |             9 |
|             1024 |            10 |
|             2048 |            11 |
|             4096 |            12 |
|             8192 |            13 |
|            16384 |            14 |
|            32768 |            15 |
|            65536 |            16 |

The general rule is:

```text
s = ceil(log2(required subnets))
```

For example, if 10 subnets are required:

```text
2^3 = 8     not enough
2^4 = 16    enough
```

Therefore:

```text
s = 4 bits
```

---

# 9. Prefix Length Cheat Sheet

The 16-bit Subnet ID starts immediately after `/48`.

Therefore:

```text
48 + subnet bits = new prefix length
```

| Subnet bits | Prefix |
| ----------: | -----: |
|           0 |  `/48` |
|           1 |  `/49` |
|           2 |  `/50` |
|           3 |  `/51` |
|           4 |  `/52` |
|           5 |  `/53` |
|           6 |  `/54` |
|           7 |  `/55` |
|           8 |  `/56` |
|           9 |  `/57` |
|          10 |  `/58` |
|          11 |  `/59` |
|          12 |  `/60` |
|          13 |  `/61` |
|          14 |  `/62` |
|          15 |  `/63` |
|          16 |  `/64` |

Remember:

```text
New prefix = original prefix + number of allocated subnet bits
```

For example:

```text
/48 + 5 bits = /53
```

---

# 10. Hexadecimal Increment

This is the key calculation for manually finding the next IPv6 subnet.

The 16-bit Subnet ID contains 16 bits.

If:

```text
f = fixed bits
s = bits allocated to the current subnet level
r = remaining bits
```

then:

```text
r = 16 - f - s
```

The increment between consecutive subnet IDs is:

```text
I = 2^r
```

Convert the result to hexadecimal.

Therefore:

```text
Increment = 2^(16 - f - s)
```

This tells you what value to add to the Subnet ID to get the next subnet.

---

# 11. Quick Hexadecimal Increment Table

For the common case where the entire 16-bit Subnet ID is being divided at once:

| Subnet bits | Prefix | Number of subnets | Increment |
| ----------: | -----: | ----------------: | --------: |
|           1 |  `/49` |                 2 |    `8000` |
|           2 |  `/50` |                 4 |    `4000` |
|           3 |  `/51` |                 8 |    `2000` |
|           4 |  `/52` |                16 |    `1000` |
|           5 |  `/53` |                32 |    `0800` |
|           6 |  `/54` |                64 |    `0400` |
|           7 |  `/55` |               128 |    `0200` |
|           8 |  `/56` |               256 |    `0100` |
|           9 |  `/57` |               512 |    `0080` |
|          10 |  `/58` |              1024 |    `0040` |
|          11 |  `/59` |              2048 |    `0020` |
|          12 |  `/60` |              4096 |    `0010` |
|          13 |  `/61` |              8192 |    `0008` |
|          14 |  `/62` |             16384 |    `0004` |
|          15 |  `/63` |             32768 |    `0002` |
|          16 |  `/64` |             65536 |    `0001` |

This table is the IPv6 equivalent of the familiar IPv4 subnetting increment table.

---

# 12. Example: 8 Subnets

Given:

```text
2001:db8:cad::/48
```

We need:

```text
8 subnets
```

Find the number of bits:

```text
2^3 = 8
```

Therefore:

```text
s = 3
```

The new prefix is:

```text
48 + 3 = /51
```

Remaining bits:

```text
r = 16 - 0 - 3
r = 13
```

Increment:

```text
I = 2^13
I = 8192 decimal
I = 2000 hexadecimal
```

Therefore the subnet IDs increase by:

```text
2000
```

The resulting networks are:

```text
2001:db8:cad:0000::/51
2001:db8:cad:2000::/51
2001:db8:cad:4000::/51
2001:db8:cad:6000::/51
2001:db8:cad:8000::/51
2001:db8:cad:a000::/51
2001:db8:cad:c000::/51
2001:db8:cad:e000::/51
```

The important pattern is:

```text
0000
2000
4000
6000
8000
A000
C000
E000
```

---

# 13. Example: 4 Subnets

Given:

```text
2001:db8:cad::/48
```

Required:

```text
4 subnets
```

Required bits:

```text
2^2 = 4
```

Therefore:

```text
s = 2
```

New prefix:

```text
48 + 2 = /50
```

Remaining bits:

```text
r = 16 - 2
r = 14
```

Increment:

```text
I = 2^14
I = 16384 decimal
I = 4000 hexadecimal
```

Therefore:

```text
2001:db8:cad:0000::/50
2001:db8:cad:4000::/50
2001:db8:cad:8000::/50
2001:db8:cad:c000::/50
```

The Subnet ID pattern is:

```text
0000
4000
8000
C000
```

---

# 14. General Manual Subnetting Procedure

When solving an IPv6 subnetting problem manually, use this sequence.

### Step 1 — Identify the starting prefix

Example:

```text
2001:db8:cad::/48
```

### Step 2 — Identify the available Subnet ID bits

For a `/48` allocation with `/64` LANs:

```text
64 - 48 = 16 bits
```

### Step 3 — Determine how many subnets are required

For example:

```text
10 subnets
```

### Step 4 — Determine the number of bits required

Find the smallest power of two that is sufficient:

```text
2^3 = 8       insufficient
2^4 = 16      sufficient
```

Therefore:

```text
s = 4
```

### Step 5 — Calculate the new prefix

```text
48 + 4 = /52
```

### Step 6 — Calculate remaining bits

```text
r = 16 - f - s
```

For a first-level division:

```text
f = 0
s = 4

r = 16 - 0 - 4
r = 12
```

### Step 7 — Calculate the increment

```text
I = 2^12
I = 4096 decimal
I = 1000 hexadecimal
```

### Step 8 — Generate the subnet IDs

```text
0000
1000
2000
3000
...
F000
```

---

# 15. Hierarchical Subnetting

IPv6 subnetting becomes particularly useful when a company wants to create a hierarchy.

For example:

```text
Organization
    |
    +-- Countries
          |
          +-- States
                |
                +-- Offices
```

The 16-bit Subnet ID can be divided into sections.

For example:

```text
| Country | State | Office | Remaining |
```

The important rule is:

```text
f + s + r = 16
```

At every level, previously allocated bits become **fixed bits**.

---

# 16. Hierarchical Subnetting Example

Given:

```text
2001:db8:cad::/48
```

We need:

```text
4 countries
60 states per country
10 offices per state
```

We have:

```text
16 subnet bits available
```

---

## Level 1 — Countries

We need:

```text
4 countries
```

Therefore:

```text
2^2 = 4
```

Allocate:

```text
s = 2
```

At this point:

```text
f = 0
s = 2
r = 14
```

New prefix:

```text
/48 + 2 = /50
```

Increment:

```text
I = 2^14
I = 16384
I = 4000 hex
```

The country networks are:

```text
2001:db8:cad:0000::/50    Country 1
2001:db8:cad:4000::/50    Country 2
2001:db8:cad:8000::/50    Country 3
2001:db8:cad:c000::/50    Country 4
```

---

# 17. Level 2 — States

We need:

```text
60 states
```

Find the required number of bits:

```text
2^5 = 32       insufficient
2^6 = 64       sufficient
```

Therefore:

```text
s = 6
```

The first 2 bits are already fixed by the country allocation:

```text
f = 2
```

Remaining bits:

```text
r = 16 - 2 - 6
r = 8
```

The state prefix becomes:

```text
48 + 2 + 6 = /56
```

Increment:

```text
I = 2^8
I = 256 decimal
I = 0100 hex
```

For Country 1:

```text
2001:db8:cad:0000::/50     Country 1

2001:db8:cad:0100::/56     State 1
2001:db8:cad:0200::/56     State 2
2001:db8:cad:0300::/56     State 3
...
2001:db8:cad:3f00::/56     State 64
```

The same structure repeats inside every country:

```text
Country 1 → 0000–3F00
Country 2 → 4000–7F00
Country 3 → 8000–BF00
Country 4 → C000–FF00
```

---

# 18. Level 3 — Offices

We need:

```text
10 offices
```

Find the required bits:

```text
2^3 = 8       insufficient
2^4 = 16      sufficient
```

Therefore:

```text
s = 4
```

Previously allocated:

```text
f = 2 + 6
f = 8
```

Remaining:

```text
r = 16 - 8 - 4
r = 4
```

The office prefix becomes:

```text
48 + 8 + 4 = /60
```

Increment:

```text
I = 2^4
I = 16 decimal
I = 0010 hex
```

For the first state:

```text
2001:db8:cad:0100::/56    State 1

2001:db8:cad:0110::/60    Office 1
2001:db8:cad:0120::/60    Office 2
2001:db8:cad:0130::/60    Office 3
...
2001:db8:cad:01F0::/60    Office 16
```

The allocation has now used:

```text
2 + 6 + 4 = 12 bits
```

Therefore:

```text
16 - 12 = 4 bits remaining
```

Those remaining bits could be used for another level of hierarchy.

---

# 19. Hierarchical Subnetting Summary

The previous example can be summarized as:

```text
Original allocation:

2001:db8:cad::/48
        |
        | 16 bits available
        v
+-------+-------+--------+----------+
|Country| State | Office | Remaining|
| 2 bit | 6 bit| 4 bit  |  4 bit   |
+-------+-------+--------+----------+
```

Prefix lengths:

```text
Country:
48 + 2 = /50

State:
48 + 2 + 6 = /56

Office:
48 + 2 + 6 + 4 = /60
```

The general rule is:

```text
New prefix = original prefix + all subnet bits allocated so far
```

---

# 20. The Most Useful Mental Model

When looking at a `/48` allocation, imagine:

```text
2001:db8:cad:XXXX::/48
              ^^^^
              16-bit Subnet ID
```

The entire problem is about deciding how to divide:

```text
XXXX
```

into useful groups of bits.

For example:

```text
2 bits:
XX00 0000 0000 0000
```

or:

```text
2 + 6 + 4 + 4 = 16

| CC | SSSSSS | OOOO | RRRR |
```

where:

```text
C = Country
S = State
O = Office
R = Remaining
```

This is often much easier to understand than thinking about all 128 bits simultaneously.

---

# 21. IPv6 Prefix Length vs. Subnet ID

Remember that the prefix length counts **all bits from the beginning of the IPv6 address**.

For example:

```text
2001:db8:cad:4000::/50
```

means:

```text
48 bits = original routing prefix
 2 bits = subnet bits

48 + 2 = 50
```

The remaining 14 bits of the Subnet ID are still available within that `/50` network.

Similarly:

```text
2001:db8:cad:0100::/56
```

means:

```text
48 bits = original routing prefix
 8 bits = allocated subnet bits

48 + 8 = 56
```

---

# 22. `/64` — The Common IPv6 LAN Prefix

A typical IPv6 LAN uses a `/64`.

For example:

```text
2001:db8:cad:1234::/64
```

The structure is:

```text
|<------------- 64 bits ------------->|<------------- 64 bits ------------->|
|             Network Prefix           |           Interface ID              |
```

The Interface ID contains 64 bits:

```text
2^64
```

possible values.

Unlike IPv4, IPv6 subnetting normally does **not** involve taking arbitrary bits away from the 64-bit Interface ID simply to create ordinary LAN subnets.

Instead, the subnetting is normally performed before the `/64` boundary.

---

# 23. IPv6 Address Scopes

IPv6 addresses contain information about their intended scope.

| Prefix      | Purpose             |
| ----------- | ------------------- |
| `::/128`    | Unspecified address |
| `::1/128`   | Loopback            |
| `2000::/3`  | Global Unicast      |
| `fc00::/7`  | Unique Local        |
| `fe80::/10` | Link-Local          |
| `ff00::/8`  | Multicast           |

### Global Unicast

```text
2000::/3
```

Globally routable IPv6 addresses.

### Unique Local

```text
fc00::/7
```

Private IPv6 addressing.

In practice, locally generated Unique Local addresses commonly use:

```text
fd00::/8
```

### Link-Local

```text
fe80::/10
```

Used for communication on the local link.

Link-local addresses are not routed between links.

### Loopback

```text
::1/128
```

Equivalent in purpose to:

```text
127.0.0.1
```

in IPv4.

### Unspecified

```text
::/128
```

Equivalent in purpose to:

```text
0.0.0.0
```

in IPv4.

---

# 24. IPv6 Communication Types

IPv6 supports:

### Unicast

One sender → one receiver.

```text
Host A → Host B
```

### Multicast

One sender → multiple members of a multicast group.

```text
Host A → multicast group
```

Examples:

```text
ff02::1    All Nodes
ff02::2    All Routers
```

### Anycast

One sender → the nearest/appropriate node using the same anycast address.

### Broadcast

IPv6 does **not** use broadcast.

Functions that would traditionally require broadcast are generally implemented using multicast.

---

# 25. Common IPv6 Multicast Addresses

| Address     | Purpose                         |
| ----------- | ------------------------------- |
| `ff02::1`   | All nodes on the local link     |
| `ff02::2`   | All routers on the local link   |
| `ff02::fb`  | mDNS                            |
| `ff02::1:2` | DHCPv6 servers and relay agents |
| `ff02::101` | NTP servers                     |

A useful address to remember when learning IPv6:

```text
ff02::1
```

This represents all IPv6 nodes on the local link.

---

# 26. IPv6 Address Assignment

IPv6 addresses can be assigned using:

### Static

The address is manually configured.

### SLAAC

**Stateless Address Autoconfiguration**

The host can configure its own IPv6 address based on information advertised by the router.

### DHCPv6

**Dynamic Host Configuration Protocol for IPv6**

A DHCPv6 server can provide configuration information to hosts.

SLAAC and DHCPv6 can also be used together depending on the network configuration.

---

# 27. IPv6 and ICMPv6

Internet Control Message Protocol (ICMP)
ICMPv6 is an important part of IPv6 operation.

It is used for:

* Error reporting
* Diagnostics
* Neighbor Discovery
* Router Discovery
* Ping

Common ICMPv6 types:

|  Type | Purpose                 |
| ----: | ----------------------- |
|   `1` | Destination Unreachable |
|   `3` | Time Exceeded           |
| `128` | Echo Request            |
| `129` | Echo Reply              |
| `133` | Router Solicitation     |
| `134` | Router Advertisement    |
| `135` | Neighbor Solicitation   |
| `136` | Neighbor Advertisement  |

Ping:

```text
128 → Echo Request
129 → Echo Reply
```

Router discovery:

```text
133 → Router Solicitation
134 → Router Advertisement
```

Neighbor discovery:

```text
135 → Neighbor Solicitation
136 → Neighbor Advertisement
```

---

# 28. Useful IPv6 Linux Commands

Display IPv6 addresses:

```bash
ip addr | grep inet6
```

Display all interface information:

```bash
ip addr
```

Ping an IPv6 host:

```bash
ping -6 www.example.com
```

Example:

```bash
ping -6 www.ibm.com
```

---

# 29. IPv6 Addresses in URLs

Because IPv6 addresses already use `:` characters, an IPv6 address inside a URL must be enclosed in square brackets.

Without a port:

```text
http://[2001:db8::1]
```

With a port:

```text
http://[2001:db8::1]:8000
```

The brackets separate the IPv6 address from the port number.

---

# 30. Practical IPv6 Subnetting Cheat Sheet

When you need to subnet an IPv6 `/48`, use this condensed procedure.

```text
1. Start with the /48 prefix.

2. You normally have 16 bits available
   for the Subnet ID before the /64 boundary.

3. Determine how many subnets are required.

4. Find the smallest s where:

       2^s >= required subnets

5. New prefix:

       /48 + s

6. Calculate remaining bits:

       r = 16 - f - s

7. Calculate subnet increment:

       I = 2^r

8. Convert I to hexadecimal.

9. Add the increment to the Subnet ID
   to obtain the next subnet.

10. For hierarchical subnetting, previously
    allocated bits become fixed:

       f + s + r = 16
```

---

# 31. One-Page Subnetting Table

### Starting from `/48`

| Required subnets | Bits | Prefix | Increment |
| ---------------: | ---: | -----: | --------: |
|                2 |    1 |  `/49` |    `8000` |
|                4 |    2 |  `/50` |    `4000` |
|                8 |    3 |  `/51` |    `2000` |
|               16 |    4 |  `/52` |    `1000` |
|               32 |    5 |  `/53` |    `0800` |
|               64 |    6 |  `/54` |    `0400` |
|              128 |    7 |  `/55` |    `0200` |
|              256 |    8 |  `/56` |    `0100` |
|              512 |    9 |  `/57` |    `0080` |
|             1024 |   10 |  `/58` |    `0040` |
|             2048 |   11 |  `/59` |    `0020` |
|             4096 |   12 |  `/60` |    `0010` |
|             8192 |   13 |  `/61` |    `0008` |
|            16384 |   14 |  `/62` |    `0004` |
|            32768 |   15 |  `/63` |    `0002` |
|            65536 |   16 |  `/64` |    `0001` |

---

# 32. IPv6 Subnetting Formula Card

Keep these formulas together:

```text
Number of subnets:

    2^s


Required subnet bits:

    s = ceil(log2(required subnets))


Available Subnet ID bits:

    16 bits       (typical /48 → /64 model)


New prefix:

    original prefix + allocated subnet bits


Remaining bits:

    r = 16 - f - s


Subnet increment:

    I = 2^r


Total:

    f + s + r = 16
```

The most important one for manual calculations is:

```text
              16-bit Subnet ID
        +-------------------------+
        | fixed | subnet | remain |
        +-------------------------+
           f       s        r

             f + s + r = 16
```

---

# 33. Worked Example — Complete Hierarchy

Given:

```text
2001:db8:cad::/48
```

Requirements:

```text
4 countries
60 states per country
10 offices per state
```

### Country

```text
4 networks
2 bits
/50
increment = 4000
```

```text
2001:db8:cad:0000::/50
2001:db8:cad:4000::/50
2001:db8:cad:8000::/50
2001:db8:cad:c000::/50
```

### State

```text
60 networks
6 additional bits
/56
increment = 0100
```

Example inside Country 1:

```text
2001:db8:cad:0100::/56
2001:db8:cad:0200::/56
2001:db8:cad:0300::/56
...
2001:db8:cad:3f00::/56
```

### Office

```text
10 networks
4 additional bits
/60
increment = 0010
```

Example inside State 1:

```text
2001:db8:cad:0110::/60
2001:db8:cad:0120::/60
2001:db8:cad:0130::/60
...
2001:db8:cad:01f0::/60
```

The complete bit allocation is:

```text
Country = 2 bits
State   = 6 bits
Office  = 4 bits
Unused  = 4 bits

2 + 6 + 4 + 4 = 16
```

---

# 34. IPv6 vs. IPv4 Subnetting — Mental Comparison

A useful way to connect IPv6 subnetting to what was learned in NetPractice is:

### IPv4

Usually think:

```text
Network | Subnet | Host
```

You borrow host bits to create smaller networks.

### IPv6

For a typical `/48` allocation, think:

```text
Routing Prefix | Subnet ID | Interface ID
     48 bits       16 bits       64 bits
```

You normally divide the **16-bit Subnet ID** into logical subnet levels.

For example:

```text
| Country | State | Office | Remaining |
|   2     |   6   |   4    |     4     |
```

The Interface ID is then left as the 64-bit host/interface portion of the final `/64` network.

# 37. Final Mental Model

If you remember only one thing about IPv6 subnetting, remember this:

```text
IPv6 = 128 bits

Typical allocation:

|<------ 48 ------>|<-- 16 -->|<------ 64 ------>|
| Routing Prefix   | Subnet ID |  Interface ID    |
```

The subnetting problem is usually:

```text
How should I divide these 16 bits?
```

For every subnetting level:

```text
f = fixed bits
s = new subnet bits
r = remaining bits

f + s + r = 16
```

The number of networks created by `s` bits is:

```text
2^s
```

The increment between subnet IDs is:

```text
2^r
```

converted to hexadecimal.

So the complete process is:

```text
Required networks
       ↓
Determine subnet bits
       ↓
Calculate prefix length
       ↓
Calculate remaining bits
       ↓
Calculate hexadecimal increment
       ↓
Generate subnet IDs
       ↓
Repeat for the next hierarchy level
```

This is the core of manual IPv6 subnetting.

---
## Protocols

| Number | Protocol  | Purpose                                                                                                 |
| ------ | --------- | ------------------------------------------------------------------------------------------------------- |
| 6      | TCP       | Stateful - Confirms if packets have arrived. Important for use cases with validation.                   |
| 17     | UDP       | Stateless - Does not confirm if packets have arrived. Good for streaming applications, VoIP calls, etc. |
| 58     | IPv6-ICMP | Information, Error reporting, diagnostics based use cases.                                              |

## Methods to Assign IPv6 Addresses

**Static** - Fixed Address,  
**SLAAC** - Stateless Address Auto-Configuration (Address generated by Host),  
**DHCPv6** - Dynamic Host Configuration Protocol (Address assigned by a central DHCP server).

## Scopes and Special Addresses

When working in the world of IPv6, our addresses can vary depending on our scope (i.e. what part of a network):  
**GLOBAL** - Everything (i.e. the whole internet),  
**UNIQUE LOCAL** - Everything in our LAN (behind the internet gateway),  
**LINK LOCAL** - Everything within the same collision domain that will not be routed (i.e. attached to the same switch).

| Range     | Purpose                          |
| --------- | -------------------------------- |
| ::1/128   | Loopback Address (localhost)     |
| ::/128    | Unspecified Address              |
| 2000::/3  | GLOBAL Unicast (Internet)        |
| fc00::/7  | Unique-Local (LAN)               |
| fe80::/10 | Link-Local Unicast (Same switch) |

You should always use the smallest possible scope for communication.  
A host can have **multiple** addresses in different scopes, even on the same interface.

## Subnetting

<img src=address_format.png width=600>

As in IPv4, IPv6 includes support for network segmentation via Subnetting. In the image below, the first 64 bits are designated as the `Network` portion, while the last 64 bits are for `Host` identification. Within the network portion, the first 48 bits are the `Routing Prefix` - aka the Network Address. The next and final 16 bits of the network notion is the `Subnet ID` or subnet address.

**Network+Subnet = Prefix**

The following address:

`2003:1000:1000:1600:1234::1` formatted fully as `2003:1000:1000:1600:1234:0000:0000:0001`, consists of the following segments:

- `2003:1000:1000:1600` - Prefix (Combined of Routing Prefix and Subnet ID)
- `2003:1000:1000` - Routing Prefix / Network Address
- `1600` - Subnet ID / Subnet

If my ISP provider **delegated** a portion of the prefix to me (e.g. `2003:1000:1000:1600/56`), then I could use the subnets `1600` through to `16FF` for my own purposes (Which would give me 256 available subnets).

## IPv6 Addresses in URIs/URLs

Because IPv6 address notation uses colons to isolate hextets, it is necessary to encase the address in square brackets in URIs. For example `http://[2a00:1450:4001:82a::2004]`. If you wish to specify a port, you can do so as normal using a colon following the closing square bracket: `http://[2a00:1450:4001:82a::2004]:80`.

## Multicast

Communication from one node to another is called **Unicast**. Communication from one node to many is called **Multicast**.

The following IPv6 multicast addresses may be used in in the link-local scope:

| Range     | Purpose                                |
| --------- | -------------------------------------- |
| ff02::1   | All Nodes within the network segment   |
| ff02::2   | All Routers within the network segment |
| ff02::fb  | mDNSv6                                 |
| ff02::1:2 | All DHCP Servers and Agents            |
| ff02::101 | All NTP Servers                        |

A full list is maintained by [IANA](https://www.iana.org/assignments/ipv6-multicast-addresses/ipv6-multicast-addresses.xhtml)

You can actually ping these addresses, e.g. `ping ff02::1`

## ICMP Message Types

ICMP does not use ports in order to communicate, but rather **types**. Critical/important types have numbers ranging from 1-127, while informational types have the numbers 128 and above. Each **type** can have subtypes or rather **codes** that can be used for further specifications.  

Here are some frequently used IPv6 ICMP types:

| Type | Code | Purpose                        |
| ---- | ---- | ------------------------------ |
| 0    |      | Reserved                       |
| 1    |      | Destination Unreachable        |
| 1    | 0    | No Route to Destination        |
| 1    | 2    | Beyond Scope of Source Address |
| 3    |      | Time Exceeded                  |
| 3    | 0    | Hop Limit Exceeded in Transit  |

| Type | Code | Purpose                   |
| ---- | ---- | ------------------------- |
| 128  | 0    | Echo Request ("ping")     |
| 129  | 0    | Echo Reply                |
| 133  | 0    | Router Solicitation       |
| 134  | 0    | Router Advertisement      |
| 135  | 0    | Neighbo(u)r Solicitation  |
| 136  | 0    | Neighbo(u)r Advertisement |

A full list is maintained by [IANA](https://www.iana.org/assignments/icmpv6-parameters/icmpv6-parameters.xhtml)

## DHCPv6

IPv6 addresses can be distributed using the IPv6 version of the **Dynamic Host Configuration Protocol (DHCPv6)**. If a host wishes to obtain an IPv6 address via DHCPv6, it sends out a **DHCP Solicitation** from UDP port 546 to port 547 on the DHCP multicast address `ff02::1:2`. The DHCP server then replies to the client (from UDP port 547 to UDP port 546) with **DHCP Advertisement**. This handshake can be completed by the client sending out a **DHCP Request** and the server responding with a **DHCP Reply**

The DHCPv6 protocol is explained in more detail in this [Wikipedia Article](https://en.wikipedia.org/wiki/DHCPv6)

## DHCPv6 vs. SLAAC

Depending on how the router and the client are set up, the client can (and will) use both mechanisms (i.e. SLAAC and DHCP) to acquire IPv6 address allocations. The following table highlights the possible configuration combinations:

<img src=dhcp_slaac.jpg>

## Using WireShark

To gain a greater understanding of IPv6's functionality, you can use the packet sniffing tool WireShark to trace the message flow. Here are some WS filters for IPv6 ICMP, DHCPv6 and Router Solicitation and Advertisements:

Show ping and ping reply: `icmpv6 and (icmpv6.type==128) or (icmpv6.type==129)` <br>
Router solicit and advertise: `icmpv6 and (icmpv6.type==133) or (icmpv6.type==134)` <br>
Show DHCPv6 traffic: `dhcpv6` <br>
Router Solicit/Advertise and DHCPv6: `dhcpv6 or (icmpv6 and (icmpv6.type==134) or (icmpv6.type==133))` <br>

### Unicast vs. Multicast vs. Broadcast vs. Anycast

Within IPv6, there are a range of message options. All of these message types have a single host transmitting the message and all delivery is handled by the switch or router:

- **Unicast** is a message sent from a host to one receiver (One to One),
- **Broadcast** is a message sent from a host to all other hosts on the same broadcast domain (One to All),
- **Multicast** is a message sent from a host to all subscribers of a Multicast group (One to Specific),
- **Anycast** is a message sent from a host to the fastest / nearest subscriber of a specific address (One to Specific - Fastest Receiver / Nearest Node will receive).
 
---

# References

## Videos

The following videos were used as learning material and additional explanations of IPv6 addressing and subnetting:

1. [IPv6 Subnetting](https://www.youtube.com/watch?v=fOaw65eaLV8)
2. [IPv6 Address Types](https://www.youtube.com/watch?v=HCTl3UJ9FlE)
3. [Subnetting IPv6 Addresses](https://www.youtube.com/watch?v=UIGVPvxnCtk)
4. [Manual IPv6 Subnetting](https://www.youtube.com/watch?v=KSiZ751-Zs8&pp=0gcJCRsMAYcqIYzv)
5. [ITFreeTraining — IPv6 videos](https://www.youtube.com/@itfreetraining/search?query=ipv6)

## Additional References

* [IANA IPv6 Multicast Address Assignments](https://www.iana.org/assignments/ipv6-multicast-addresses/ipv6-multicast-addresses.xhtml)
* [IANA ICMPv6 Parameters](https://www.iana.org/assignments/icmpv6-parameters/icmpv6-parameters.xhtml)
* [IPv6 Subnet Calculator](http://www.subnetonline.com/pages/subnetcalculators/ipv6-subnet-calculator.php)
* [GestioIP IPv4/IPv6 Subnet Calculator](http://www.gestioip.net/cgi-bin/subnet_calculator.cgi)

---

# Useful RFCs

For deeper reference:

* **RFC 4291** — IPv6 Addressing Architecture
* **RFC 5952** — A Recommendation for IPv6 Address Text Representation
* **RFC 4193** — Unique Local IPv6 Unicast Addresses
* **RFC 4862** — IPv6 Stateless Address Autoconfiguration
* **RFC 8200** — Internet Protocol, Version 6 (IPv6) Specification
---