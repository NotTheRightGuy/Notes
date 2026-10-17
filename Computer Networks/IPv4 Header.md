---
tags:
  - GATE/CS
  - GATE/ComputerNetworks
  - InternetProtocol
  - PacketSwitching
aliases:
  - IPv4 Header Format
  - IP Packet Header
  - Internet Protocol v4 Header
date_created: 2026-08-31
difficulty: ⭐⭐⭐
last_revised: 2026-08-31
pyq_frequency: High
---

## Syllabus Position

Subject: [[Computer Networks]]
Parent Topic: [[Network Layer]]
Sibling Topics: [[Classful Addressing]], [[Classless Addressing]], [[Subnet Masking]], [[Supernetting]]
Leads To: [[IPv6]], [[NAT]], [[ICMP]], [[Routing Algorithms]]

GATE Syllabus Line: "IPv4: Datagram, fragmentation, and reassembly, addressing, subnetting, CIDR, NAT."

Exam Weight Note: Appears frequently as 1-mark MCQs on field sizes and flag meanings, and as 2-mark NAT/MCQ on fragmentation offsets, identification fields, and header length calculations.

---

## The Problem This Solves

When data travels across the Internet, it passes through many intermediate routers. Each router needs to know where the packet came from, where it's going, how long it has been alive, and whether it is part of a larger fragmented message. Without a standardized header at the network layer, routers would have no idea how to forward packets or handle errors.

Think of it like a shipping label on a package: it must contain the sender's address, recipient's address, weight limits, and handling instructions — all in a fixed format so every courier in the chain can read it instantly.

**Core Idea:** The IPv4 header is a 20-byte (minimum) fixed-format header that every IP datagram carries, giving routers the metadata needed to forward, fragment, and manage packets across the Internet.

---

## Formal Theory

### Overview

The IPv4 header is defined in RFC 791. It sits between the Data Link Layer frame and the Transport Layer segment. Every IPv4 datagram begins with this header, which is a minimum of 20 bytes and can extend up to 60 bytes with options.

![[Screenshot 2026-09-02 at 3.45.14 PM.png]]

### Header Structure (20 Bytes Minimum)

The header is organized into 32-bit (4-byte) words. GATE expects you to know every field by position, size, and purpose.


### Field-by-Field Breakdown

### Version (4 bits)

Specifies the IP version. For IPv4, this is always `4` (binary `0100`). Routers use this field to determine which header format to parse. If the version is not 4, the packet is rejected.

GATE angle: Questions sometimes ask "what is the decimal value of the version field" — the answer is always 4.

### IHL — Internet Header Length (4 bits)

Specifies the length of the header in **32-bit words** (4-byte units). The minimum value is 5 (meaning 5 × 4 = 20 bytes, the fixed header with no options). The maximum value is 15 (15 × 4 = 60 bytes, with maximum options).

**Key formula:**

$$\text{Header Size (bytes)} = \text{IHL} \times 4$$

GATE frequently tests: "If IHL = 8, what is the header size?" Answer: 8 × 4 = 32 bytes.

### DSCP — Differentiated Services Code Point (6 bits)

Originally called the **Type of Service (ToS)** field. Used for Quality of Service (QoS) routing. The first 6 bits define the DSCP value, which tells routers how to prioritize the packet (e.g., low-latency for VoIP, best-effort for email).

### ECN — Explicit Congestion Notification (2 bits)

The last 2 bits of the ToS byte. Allows end-to-end congestion notification without dropping packets. Routers set ECN bits to signal congestion; the receiver echoes this to the sender.

GATE note: ECN is a recent addition and rarely tested, but know it exists as part of the ToS byte.

### Total Length (16 bits)

The total length of the entire IP datagram (header + payload) in bytes.

**Range:**

$$\text{Total Length} \in [20, 65535] \text{ bytes}$$

- Minimum: 20 bytes (header only, no data)
- Maximum: $2^{16} - 1 = 65535$ bytes

**Payload length** is derived as:

$$\text{Payload Length} = \text{Total Length} - \text{Header Length} = \text{Total Length} - (\text{IHL} \times 4)$$

GATE trap: Students confuse Total Length with Header Length. Total Length includes both header and data.

### Identification (16 bits)

A unique identifier assigned by the sender to every datagram. When a datagram is fragmented, all fragments carry the **same Identification value**, allowing the receiver to reassemble them correctly.

- Initial value: typically incremented for each datagram sent
- Used in conjunction with Fragment Offset and MF flag for reassembly

### Flags (3 bits)

Controls fragmentation behavior:

| Bit | Name | Meaning |
|-----|------|---------|
| 0 | Reserved | Must be 0 |
| 1 | DF (Don't Fragment) | If 1, the datagram must not be fragmented. If fragmentation is needed, the router discards the packet and sends an ICMP error. |
| 2 | MF (More Fragments) | If 1, this fragment is not the last; more fragments follow. If 0, this is the last fragment (or no fragmentation occurred). |

**Bit pattern for common scenarios:**

- No fragmentation: `010` (DF=1, MF=0)
- Middle fragment: `001` (DF=0, MF=1)
- Last fragment: `000` (DF=0, MF=0)

GATE frequently tests: "A packet arrives with flags = `001`. What does this mean?" Answer: It is an intermediate fragment; more fragments are coming.

### Fragment Offset (13 bits)

Specifies the position of this fragment's data relative to the original datagram's data, measured in **8-byte units** (64-bit blocks).

**Key formula:**

$$\text{Byte Offset} = \text{Fragment Offset} \times 8$$

- First fragment: Offset = 0
- Subsequent fragments: Offset = (cumulative data bytes before this fragment) / 8

GATE critical point: The offset is in 8-byte units, NOT byte units. A fragment offset of 100 means byte 800 of the original datagram.

### Time to Live — TTL (8 bits)

Limits the datagram's lifetime to prevent infinite looping. Each router that processes the packet **decrements TTL by at least 1**. When TTL reaches 0, the router discards the packet and sends an ICMP "Time Exceeded" message to the sender.

- Initial TTL: set by the sender (commonly 64, 128, or 255)
- Maximum hop count: 255 (if initial TTL = 255)

GATE question pattern: "A packet with TTL = 3 passes through routers. How many routers can it traverse before being discarded?" Answer: 3 routers (TTL decremented to 0 at the 3rd router).

### Protocol (8 bits)

Identifies the protocol of the encapsulated payload in the data portion of the datagram. This tells the receiver which transport-layer protocol to hand the data to.

| Protocol Number | Protocol |
|-----------------|----------|
| 1 | [[ICMP]] |
| 2 | IGMP |
| 6 | [[TCP]] |
| 17 | [[UDP]] |
| 89 | OSPF |

GATE tests: "If the Protocol field = 17, what transport protocol is used?" Answer: UDP.

### Header Checksum (16 bits)

Used for error detection in the header only (not the payload). The checksum is computed using the **1's complement sum** of all 16-bit words in the header.

**Algorithm:**

1. Set the checksum field to 0.
2. Divide the header into 16-bit words.
3. Compute the 1's complement sum.
4. Take the 1's complement of the result.
5. Place this value in the Header Checksum field.

Since TTL changes at every router, the checksum must be **recomputed at each hop**.

GATE note: The checksum protects only the header. If the data is corrupted, it is not detected by this field — transport-layer checksums handle that.

### Source Address (32 bits)

The IPv4 address of the original sender of the datagram. This is **never changed** during routing (unless NAT is involved).

### Destination Address (32 bits)

The IPv4 address of the final destination. This is also **never changed** during standard routing.

Note: In source routing (rarely used), the destination can be modified hop by hop.

### Options (variable, 0–40 bytes)

Optional fields that extend the header beyond 20 bytes. When present, the IHL value increases accordingly. Common options include:

- **Record Route**: Records the IP addresses of routers the packet traverses
- **Strict Source Routing**: The sender specifies the exact route
- **Loose Source Routing**: The sender specifies some hops, but others can be inserted
- **Timestamp**: Records when the packet passes through each router

Options are padded to ensure the header ends on a 32-bit boundary.

GATE critical: If IHL = 7, options occupy $(7 - 5) \times 4 = 8$ bytes.

### How GATE Tests This Topic

GATE loves to test:
1. Calculating header size from IHL
2. Determining payload length from Total Length and IHL
3. Interpreting Flags and Fragment Offset for reassembly
4. Understanding TTL behavior across routers
5. Mapping Protocol numbers to transport protocols
6. Calculating the number of fragments from a given MTU

---

## Diagrams and Visuals

### IPv4 Header Layout (Color-Coded)

```
Byte:  0          1          2          3
      +----------+----------+----------+----------+
  0   | Version  |    IHL   |    DSCP / ECN       |
      | (4 bits) | (4 bits) |     (8 bits)         |
      +----------+----------+----------+----------+
  4   |            Total Length (16 bits)           |
      +----------+----------+----------+----------+
  8   |       Identification (16 bits)  |Frag Flags|
      +----------+----------+----------+----------+
 12   |  Fragment Offset (13 bits) + Flags (3 bits)|
      +----------+----------+----------+----------+
 16   |    TTL (8 bits)  |  Protocol   | Checksum  |
      +----------+----------+----------+----------+
 20   |              Source Address (32 bits)       |
      +----------+----------+----------+----------+
 24   |           Destination Address (32 bits)     |
      +----------+----------+----------+----------+
 28   |          Options (if IHL > 5) ...           |
      +----------+----------+----------+----------+
```

### Fragmentation Visual Example

**Original datagram:** 4000 bytes data + 20 bytes header = 4020 bytes total.

**MTU = 1500 bytes** (Ethernet). Maximum payload per fragment = 1500 - 20 = 1480 bytes.

**Fragmentation calculation:**

- Max data per fragment: 1480 bytes
- Fragment 1: 1480 bytes data (Offset = 0, MF = 1)
- Fragment 2: 1480 bytes data (Offset = 1480/8 = 185, MF = 1)
- Fragment 3: 1040 bytes data (Offset = 2960/8 = 370, MF = 0)

```
Original: [4020 bytes]
         ├── Header (20) ──┤── Data (4000) ──────────────────────────┤

Fragment 1: [1500 bytes]
           ├── Header (20) ──┤── Data (1480) ──┤
           Offset=0, MF=1, ID=X

Fragment 2: [1500 bytes]
           ├── Header (20) ──┤── Data (1480) ──┤
           Offset=185, MF=1, ID=X

Fragment 3: [1060 bytes]
           ├── Header (20) ──┤── Data (1040) ─┤
           Offset=370, MF=0, ID=X
```

### Reassembly Process

```
Receiver collects fragments with same Identification (X):

Fragment 1: Offset=0,    MF=1 → bytes 0–1479
Fragment 2: Offset=185,  MF=1 → bytes 1480–2959
Fragment 3: Offset=370,  MF=0 → bytes 2960–3999

Reassembled: [Header from Fragment 1] + [Data from all 3 fragments]
Total data: 1480 + 1480 + 1040 = 4000 bytes ✓
```

---

## Complexity Analysis

This section is adapted for protocol concepts rather than algorithms.

### Header Processing Complexity

| Operation | Time Complexity | Notes |
|-----------|----------------|-------|
| Header parsing | $O(1)$ | Fixed-size fields, no iteration |
| Checksum computation | $O(h)$ where $h$ = header length in words | Sum of 16-bit words |
| Fragment reassembly | $O(f)$ where $f$ = number of fragments | Must sort by offset |
| Option parsing | $O(k)$ where $k$ = number of options | Variable-length options |

### Packet Size Constraints

| Parameter | Value | Formula |
|-----------|-------|---------|
| Min header | 20 bytes | 5 × 4 (IHL = 5) |
| Max header | 60 bytes | 15 × 4 (IHL = 15) |
| Min datagram | 20 bytes | Header only |
| Max datagram | 65535 bytes | $2^{16} - 1$ |
| Min fragment data | 8 bytes | Fragment offset granularity |
| Max fragment data | 65515 bytes | 65535 - 20 |

---

## Worked Example

### Example: Fragmentation with MTU = 500 bytes

**Scenario:** A 2000-byte datagram (1980 bytes data + 20 bytes header) needs to traverse a link with MTU = 500 bytes.

**Step 1: Determine max data per fragment**

$$\text{Max data per fragment} = \text{MTU} - \text{Header} = 500 - 20 = 480 \text{ bytes}$$

**Step 2: Calculate number of fragments**

$$\text{Number of fragments} = \left\lceil \frac{1980}{480} \right\rceil = \lceil 4.125 \rceil = 5 \text{ fragments}$$

**Step 3: Compute each fragment**

| Fragment | Data (bytes) | Offset (÷8) | MF | Total Size |
|----------|-------------|-------------|-----|------------|
| 1 | 480 | 0 | 1 | 500 |
| 2 | 480 | 60 | 1 | 500 |
| 3 | 480 | 120 | 1 | 500 |
| 4 | 480 | 180 | 1 | 500 |
| 5 | 60 | 240 | 0 | 80 |

**Verification:**

- Total data: $480 \times 4 + 60 = 1980$ bytes ✓
- Last fragment MF = 0 ✓
- All fragments have same Identification value ✓

**What would change if the data were 1920 bytes instead?**

Then $\lceil 1920/480 \rceil = 4$ fragments exactly (480 × 4 = 1920), and the last fragment would also have 480 bytes of data with MF = 0.

---

## Intuition Anchors

**The Analogy (deepened):**

Imagine mailing a 500-page book through a courier service that only accepts packages of 100 pages or fewer. You must split the book into 5 packages, each labeled with:
- The book's title (Identification) — so the recipient knows all packages belong together
- The page range inside (Fragment Offset) — so they can reassemble in order
- A "more packages coming" sticker (MF flag) — so they don't start reading prematurely
- A stamp saying "do not split further" (DF flag) if needed

**The Mental Model:**

When you see an IPv4 header question, picture a conveyor belt at a sorting facility. Each field is a label on the package: the version tag says "this is an IPv4 package," the TTL stamp gets punched at each station, the protocol sticker says "this contains a TCP letter," and the checksum is the security seal that gets re-verified at every stop.

**The One-Line Recall:**

IPv4 header is 20 bytes minimum, 60 bytes max; IHL measures header in 4-byte words; Fragment Offset is in 8-byte units; TTL prevents loops; Protocol identifies the payload protocol.

**The #1 Trap:**

Students assume Fragment Offset is measured in bytes. It is measured in **8-byte units**. A fragment offset of 100 corresponds to byte 800, not byte 100. This is the single most common GATE mistake on IPv4 headers.

---

## GATE Questions

---

**Question 1 — PYQ GATE 2019 — 1-mark MCQ**

> An IP datagram of size 1000 bytes arrives at a router. The router has to forward this packet on a link whose MTU is 100 bytes. The number of fragments that the IP packet will be divided into is:

- (A) 10
- (B) 11
- (C) 12
- (D) 13

<details>
<summary>Solution</summary>

**Answer: (C) 12**

**Reasoning:**

- Total datagram size: 1000 bytes
- Header: 20 bytes (standard, no options)
- Data: 1000 - 20 = 980 bytes
- MTU: 100 bytes
- Max data per fragment: 100 - 20 = 80 bytes
- Number of fragments: $\lceil 980 / 80 \rceil = \lceil 12.25 \rceil = 13$

Wait — let me recalculate: $980 / 80 = 12.25$, so $\lceil 12.25 \rceil = 13$.

**Answer: (D) 13**

**What this question is really testing:**

Whether you subtract the header from the data portion and divide by (MTU − header), then apply the ceiling function.

**Trap to avoid:**

Forgetting to subtract the 20-byte header from the MTU, or dividing the total datagram by MTU directly.

</details>

---

**Question 2 — GATE-style — 2-mark MCQ**

> A router receives an IP packet with Total Length = 4000 bytes, IHL = 5, and flags = 010 (DF=1, MF=0). The packet arrives on a link with MTU = 1500 bytes. What happens?

- (A) The router fragments the packet and forwards all fragments
- (B) The router discards the packet and sends an ICMP "Destination Unreachable" message
- (C) The router discards the packet and sends an ICMP "Time Exceeded" message
- (D) The router forwards the packet without fragmentation

<details>
<summary>Solution</summary>

**Answer: (B)**

**Reasoning:**

- Total Length = 4000 bytes, IHL = 5 → Header = 20 bytes, Data = 3980 bytes
- MTU = 1500 → Max data per fragment = 1480 bytes
- Since 3980 > 1480, fragmentation is required
- However, the DF (Don't Fragment) flag is set (flags = 010)
- When DF = 1 and fragmentation is needed, the router **discards the packet** and sends ICMP Type 3 (Destination Unreachable), Code 4 (Fragmentation Needed)

**What this question is really testing:**

The interaction between the DF flag and MTU constraints. DF=1 means "if you can't fit it, don't fragment — just drop it."

**Trap to avoid:**

Confusing ICMP "Time Exceeded" (Type 11) with ICMP "Destination Unreachable" (Type 3). Time Exceeded is for TTL = 0, not for fragmentation failure.

</details>

---

**Question 3 — GATE-style — 2-mark NAT**

> An IPv4 packet has IHL = 7. What is the size of the options field in bytes?

- (A) 0
- (B) 8
- (C) 12
- (D) 28

<details>
<summary>Solution</summary>

**Answer: (B) 8**

**Reasoning:**

- IHL = 7 means header length = 7 × 4 = 28 bytes
- Fixed header (without options) = 20 bytes (IHL = 5)
- Options size = 28 - 20 = 8 bytes

**What this question is really testing:**

Direct application of the IHL formula: Header = IHL × 4, Options = Header − 20.

**Trap to avoid:**

Thinking IHL is in bytes rather than 32-bit words, or forgetting that the base header is 20 bytes.

</details>

---

**Pattern Recognition:**

- When GATE gives IHL, immediately compute Header = IHL × 4 and Options = Header − 20.
- When GATE asks about fragmentation, always: (a) subtract header from data, (b) subtract header from MTU, (c) apply ceiling, (d) check for DF flag.
- When GATE asks about Fragment Offset, always multiply by 8 to get the byte position.
- When GATE shows flags as 3-bit binary, decode: bit 1 = DF, bit 2 = MF.

---

## Edge Cases and Failure Modes

- [ ] **IHL < 5:** Invalid. The minimum header is 20 bytes (IHL = 5). A packet with IHL = 4 is malformed and should be dropped.
- [ ] **Total Length < 20:** Invalid. A datagram must be at least 20 bytes (header only). Packets smaller than this are malformed.
- [ ] **Fragment Offset not 8-byte aligned:** The offset must always be a multiple of 8. If a fragment arrives with a non-aligned offset, it is invalid.
- [ ] **Last fragment MF=0 but data does not fill expected range:** Receiver waits for timeout before declaring reassembly complete. This introduces delay but prevents errors.
- [ ] **DF=1 but MTU < packet size:** Packet is dropped with ICMP error. Common in PMTUD (Path MTU Discovery) failures.
- [ ] **Duplicate Identification from different senders:** Receiver uses (Source, Destination, Identification, Protocol) tuple to disambiguate. Fragments from different sources with the same ID are not confused.
- [ ] **Options present but IHL still 5:** Invalid. If options are present, IHL must reflect the extended header length.
- [ ] **Header Checksum fails at receiver:** Packet is silently discarded. No ICMP error is sent (unlike TTL expiry).

---

## Comparisons

| Feature | [[IPv4 Header]] | [[IPv6 Header]] | [[TCP Header]] |
|---------|----------------|-----------------|----------------|
| Min Size | 20 bytes | 40 bytes | 20 bytes |
| Max Size | 60 bytes | 40 bytes (fixed) | 60 bytes |
| Fragmentation | Routers can fragment | Only sender fragments | N/A (segment, not packet) |
| Checksum | Header only | None | Header + pseudo-header + data |
| Address Size | 32 bits | 128 bits | N/A (uses IP addresses) |
| Fields | 13 + options | 8 (simplified) | 10 + options |
| TTL Equivalent | TTL (8 bits) | Hop Limit (8 bits) | N/A |
| GATE Preference | Most tested | Increasingly tested | Tested with TCP |

The most common GATE question comparing these is: "Which field exists in IPv4 but not IPv6?" The answer is **Header Checksum** — IPv6 removed it because link-layer and transport-layer checksums are deemed sufficient.

---

## Connections Web

**Must know before this topic:**
- [[Classful Addressing]] — how IP addresses are structured (needed to understand Source/Destination fields)
- [[Subnet Masking]] — how subnet masks interact with IP addresses in routing
- [[Delay in Computer Networks]] — understanding propagation and processing delays at routers

**Topics that build on this:**
- [[IPv6]] — the successor protocol with a simplified header
- [[ICMP]] — uses Protocol field = 1 and operates over IP
- [[NAT]] — modifies Source/Destination addresses in the header
- [[TCP]] and [[UDP]] — transport protocols identified by the Protocol field
- [[Go-Back-N Protocol]] and [[Selective Repeat Protocol]] — fragmentation is conceptually similar to ARQ segmentation

**GATE subject cross-links:**
- [[Computer Networks]] > [[Network Layer]] > IPv4 Header
- [[Computer Architecture and Organisation]] > memory alignment relates to 32-bit word alignment in header

**Cross-subject connections:**
- [[Hamming Code]] — error detection concepts parallel Header Checksum computation
- [[CRC Analysis, Characteristics of Generator Function]] — another error detection method used at Data Link Layer

**Standard references:**
- RFC 791 — Internet Protocol (original specification)
- [[Kurose & Ross]] Chapter 4 — Network Layer
- [[Tanenbaum & Wetherall]] Chapter 5 — Network Layer

---

## Quick Revision Sheet

**Definition (1 sentence):** The IPv4 header is a 20–60 byte metadata field prepended to every IP datagram, containing addressing, fragmentation, and routing information.

**Core Idea / Analogy (1 sentence):** It is the shipping label on every Internet packet — routers read it to know where to send the packet next and how to handle it.

**Key Field Sizes:**

| Field | Size | Key Detail |
|-------|------|------------|
| Version | 4 bits | Always 4 |
| IHL | 4 bits | Header size in 4-byte words (min=5, max=15) |
| Total Length | 16 bits | Entire datagram in bytes (max 65535) |
| Identification | 16 bits | Same for all fragments of one datagram |
| Flags | 3 bits | Reserved(0), DF(1), MF(2) |
| Fragment Offset | 13 bits | In 8-byte units |
| TTL | 8 bits | Decremented by each router |
| Protocol | 8 bits | 6=TCP, 17=UDP, 1=ICMP |
| Header Checksum | 16 bits | Recomputed at each hop |
| Source Address | 32 bits | Never changed |
| Destination Address | 32 bits | Never changed |

**The #1 Trap:**
Fragment Offset is in 8-byte units, not bytes. Offset of 100 = byte 800.

**When to use this over alternatives:**
IPv4 header is used for all IPv32 networks. IPv6 header is used in modern networks that have exhausted IPv4 addresses.

**Mnemonic for Fragment Offset:** "Frag-Offset-Eight" — remember it's in 8-byte chunks.

---

## Revision Checklist

- [ ] I can state the minimum and maximum header sizes without looking (20 and 60 bytes).
- [ ] I can calculate header size from any IHL value.
- [ ] I can determine the number of fragments for any datagram/MTU combination.
- [ ] I can decode the 3-bit Flags field and explain DF and MF.
- [ ] I can convert Fragment Offset to byte position and back.
- [ ] I know which Protocol numbers correspond to TCP, UDP, and ICMP.
- [ ] I understand why Header Checksum must be recomputed at every hop.
- [ ] I can trace a fragmentation and reassembly scenario by hand.
- [ ] I have linked this note correctly in my Obsidian vault.
