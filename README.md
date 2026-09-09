*This project has been created as part of the 42 curriculum by jose-car.*

# NetPractice

## Description

NetPractice is an introduction to the fundamentals of computer networking.

Instead of writing code, the project consists of solving **10 levels** in a web-based
training interface. Each level shows a small network diagram — hosts, switches, routers
and sometimes the Internet — that does **not** work as it should. One or more objectives
are stated at the top of the screen (for example: *"host A must be able to reach host B"*),
and the goal is to fill in the editable fields (IP addresses, subnet masks, default
gateways and routing table entries) so that every objective is met.

The difficulty grows level after level: the first ones only require choosing a valid host
address inside a given subnet, while the last ones involve designing several subnets,
splitting an address range with the right mask, and writing routing entries so that
packets can travel from one network to another through multiple routers.

The purpose of the project is to gain a practical, hands-on understanding of TCP/IP
addressing: how an IP address and a subnet mask define a network, which addresses are
usable, why a default gateway is needed, and how routers forward traffic between
different networks.

The networks used here are **simulated** — they are not real networks, and the addresses
and topologies shown are fictitious.

## Instructions

### Requirements

* A web browser
* `python3` (used to serve the pages locally)
* A POSIX shell (`bash`)

A local web server is required: due to browser security restrictions, opening the HTML
files directly from the filesystem does not work correctly.

### Running the training interface

1. Download the archive attached to the project page on the intranet
   (`net_practice.<version>.tgz`) and extract it in any folder of your choice:

   ```bash
   tar -xzf net_practice.1.9.tgz
   cd net_practice
   ```

2. Run the launcher script from that folder:

   ```bash
   ./run.sh
   ```

   The script starts a local web server on a free port and opens the page in your default
   web browser.

3. If `run.sh` does not work on your machine, start the server manually and open the URL
   yourself:

   ```bash
   python3 -m http.server 49242
   ```

   Then navigate to <http://localhost:49242> (any other free port number works too).

Press `Ctrl-C` in the terminal to shut the server down.

### Using the interface

The welcome page offers two tabs:

* **Training** — enter your **intranet login** and press *Start!*. The login is mandatory:
  it is used to generate the configuration that belongs to you, and the correction system
  relies on it to check your submitted files.
* **Evaluation** — generates a random configuration with three levels taken from levels 6
  to 10, to be solved in 15 minutes. This is the mode used during the defense.

For each level:

* Modify the **unshaded (editable) fields** until the network configuration is correct.
* Press **[Check again]** to verify your configuration.
* Read the **logs at the bottom of the page**: they explain why a configuration is
  rejected (missing gateway, invalid IP address, unreachable network, etc.).
* Once every objective is satisfied, a button appears to move on to the next level.

### Exporting your configurations

Once a level is solved, press the **[Get my config]** button. It downloads a file named
`levelN.json` containing your configuration for that level.

> **Do this before moving on to the next level** — otherwise you will have to solve it
> again to export it.

### Submission

Submit your work in your Git repository as usual: only what is inside the repository is
evaluated during the defense.

* The **10 exported configuration files** — one per level — must be placed **at the root
  of the repository**.
* They must keep the names produced by the export button:
  `level1.json`, `level2.json`, `level3.json`, `level4.json`, `level5.json`,
  `level6.json`, `level7.json`, `level8.json`, `level9.json`, `level10.json`.
* This `README.md` must also be at the root of the repository.
* Double-check the file names before pushing — a wrong name means the file is not
  evaluated.
* Make sure you entered **your intranet login** in the interface before exporting: files
  generated without it are not valid.

Expected repository layout:

```
.
├── README.md
├── level1.json
├── level2.json
├── level3.json
├── level4.json
├── level5.json
├── level6.json
├── level7.json
├── level8.json
├── level9.json
└── level10.json
```

During the defense you are asked to solve **three random levels** (from levels 6 to 10)
within a limited amount of time, using the *Evaluation* tab. No external tools are
allowed; only a simple calculator such as `bc` is tolerated.

## Resources

### Networking concepts studied

The following notions are the ones actually needed to complete the levels:

* **OSI model and TCP/IP model** — the layers involved here are mainly the link layer
  (switches), the network layer (IP addressing, routers) and, indirectly, the transport
  layer.
* **TCP/IP addressing (IPv4)** — the 32-bit address, its dotted-decimal notation, the
  split between network part and host part, and the distinction between private and
  public address ranges.
* **Subnet masks and CIDR notation** — how a mask such as `255.255.255.0` (`/24`)
  determines which bits identify the network, how to compute the **network address**, the
  **broadcast address** and the **range of usable host addresses**, and how to size a
  subnet for a given number of hosts (subnetting / VLSM).
* **Default gateway** — why a host needs one to reach any address outside its own subnet,
  and why the gateway must belong to the same subnet as the host's interface.
* **Routers** — devices with several interfaces, each one in a different network; they
  forward packets between those networks.
* **Routing tables** — destination network / mask and next hop, and the meaning of the
  default route (`0.0.0.0/0`).
* **Switches** — layer 2 devices: they interconnect hosts inside a single network and
  have no IP configuration of their own.
* **Address conflicts and common mistakes** — overlapping subnets, duplicated addresses,
  using a network or broadcast address as a host address, mismatched masks between two
  ends of a link.

### References

* The official 42 subject PDF (`en.subject.pdf`), available on the project page of the intranet.
* RFC 791 — *Internet Protocol*: <https://datatracker.ietf.org/doc/html/rfc791>
* RFC 1918 — *Address Allocation for Private Internets*:
  <https://datatracker.ietf.org/doc/html/rfc1918>
* RFC 4632 — *Classless Inter-Domain Routing (CIDR)*:
  <https://datatracker.ietf.org/doc/html/rfc4632>
* Cloudflare Learning Center — *What is a subnet?*:
  <https://www.cloudflare.com/learning/network-layer/what-is-a-subnet/>
* Cisco — *IP Addressing and Subnetting for New Users*:
  <https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13788-3.html>
* Practical exercises: <https://subnettingpractice.com/> and
  <https://www.subnet-calculator.com/> (to check your reasoning **while training only** —
  external tools are not allowed during the defense).
* *Computer Networking: A Top-Down Approach* — Kurose & Ross, chapters on the network
  layer.

### Use of AI

AI (a conversational assistant) was used on this project for two tasks:

* **Writing this `README.md`** — structuring the document, drafting the sections and
  collecting the list of references.
* **Clarifying networking theory** — asking for explanations about subnet masks, how to
  compute network and broadcast addresses, and the role of the default gateway and of
  routing tables, in order to better understand the concepts behind the levels.

The **10 levels were solved manually**, by reasoning about each topology directly in the
training interface; no AI was used to generate or verify the answers, and every
configuration submitted here is understood and can be explained.
