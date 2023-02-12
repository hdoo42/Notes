 Protocols (RFC 1700)

| level |  value | disc|
| --- | --- | --- | 
| IPPROTO_IP          |    0               | dummy for IP 
| IPPROTO_HOPOPTS 	  |    0               | IP6 hop-by-hop options 
| IPPROTO_ICMP        |    1               | control message protocol 
| IPPROTO_IGMP        |    2               | group mgmt protocol 
| IPPROTO_GGP         |    3               | gateway^2 (deprecated) 
| IPPROTO_IPV4        |    4               | IPv4 encapsulation 
| IPPROTO_IPIP        |    IPPROTO_IPV4    | for compatibility 
| IPPROTO_TCP         |    6               | tcp 
| IPPROTO_ST          |    7               | Stream protocol II 
| IPPROTO_EGP         |    8               | exterior gateway protocol 
| IPPROTO_PIGP        |    9               | private interior gateway 
| IPPROTO_RCCMON      |    10              | BBN RCC Monitoring 
| IPPROTO_NVPII       |    11              | network voice protocol
| IPPROTO_PUP         |    12              | pup 
| IPPROTO_ARGUS       |    13              | Argus 
| IPPROTO_EMCON       |    14              | EMCON 
| IPPROTO_XNET        |    15              | Cross Net Debugger 
| IPPROTO_CHAOS       |    16              | Chaos
| IPPROTO_UDP         |    17              | user datagram protocol 
| IPPROTO_MUX         |    18              | Multiplexing 
| IPPROTO_MEAS        |    19              | DCN Measurement Subsystems 
| IPPROTO_HMP         |    20              | Host Monitoring 
| IPPROTO_PRM         |    21              | Packet Radio Measurement 
| IPPROTO_IDP         |    22              | xns idp 
| IPPROTO_TRUNK1      |    23              | Trunk-1 
| IPPROTO_TRUNK2      |    24              | Trunk-2 
| IPPROTO_LEAF1       |    25              | Leaf-1 
| IPPROTO_LEAF2       |    26              | Leaf-2 
| IPPROTO_RDP         |    27              | Reliable Data 
| IPPROTO_IRTP        |    28              | Reliable Transaction 
| IPPROTO_TP          |    29              | tp-4 w/ class negotiation 
| IPPROTO_BLT         |    30              | Bulk Data Transfer 
| IPPROTO_NSP         |    31              | Network Services 
| IPPROTO_INP         |    32              | Merit Internodal 
| IPPROTO_SEP         |    33              | Sequential Exchange 
| IPPROTO_3PC         |    34              | Third Party Connect 
| IPPROTO_IDPR        |    35              | InterDomain Policy Routing 
| IPPROTO_XTP         |    36              | XTP 
| IPPROTO_DDP         |    37              | Datagram Delivery 
| IPPROTO_CMTP        |    38              | Control Message Transport 
| IPPROTO_TPXX        |    39              | TP++ Transport 
| IPPROTO_IL          |    40              | IL transport protocol 
| IPPROTO_IPV4        |    41              | IP6 header 
| IPPROTO_SDRP        |    42              | Source Demand Routing 
| IPPROTO_ROUTING 	  |    43              | IP6 routing header 
| IPPROTO_FRAGMENT    |    44              | IP6 fragmentation header 
| IPPROTO_IDRP        |    45              | InterDomain Routing
| IPPROTO_RSVP        |    46              | resource reservation 
| IPPROTO_GRE         |    47              | General Routing Encap. 
| IPPROTO_MHRP        |    48              | Mobile Host Routing 
| IPPROTO_BHA         |    49              | BHA 
| IPPROTO_ESP         |    50              | IP6 Encap Sec. Payload 
| IPPROTO_AH          |    51              | IP6 Auth Header 
| IPPROTO_INLSP       |    52              | Integ. Net Layer Security 
| IPPROTO_SWIPE       |    53              | IP with encryption 
| IPPROTO_NHRP        |    54              | Next Hop Resolution 
|| 55-57| Unassigned |
| IPPROTO_ICMPV6      |    58              | ICMP6 
| IPPROTO_NONE        |    59              | IP6 no next header 
| IPPROTO_DSTOPTS     |    60              | IP6 destination option 
| IPPROTO_AHIP        |    61              | any host internal protocol 
| IPPROTO_CFTP        |    62              | CFTP 
| IPPROTO_HELLO       |    63              | "hello" routing protocol 
| IPPROTO_SATEXPAK    |    64              | SATNET/Backroom EXPAK 
| IPPROTO_KRYPTOLAN   |    65              | Kryptolan 
| IPPROTO_RVD         |    66              | Remote Virtual Disk 
| IPPROTO_IPPC        |    67              | Pluribus Packet Core 
| IPPROTO_ADFS        |    68              | Any distributed FS 
| IPPROTO_SATMON      |    69              | Satnet Monitoring 
| IPPROTO_VISA        |    70              | VISA Protocol 
| IPPROTO_IPCV        |    71              | Packet Core Utility 
| IPPROTO_CPNX        |    72              | Comp. Prot. Net. Executive 
| IPPROTO_CPHB        |    73              | Comp. Prot. HeartBeat 
| IPPROTO_WSN         |    74              | Wang Span Network 
| IPPROTO_PVP         |    75              | Packet Video Protocol 
| IPPROTO_BRSATMON    |    76              | BackRoom SATNET Monitoring 
| IPPROTO_ND          |    77              | Sun net disk proto (temp.) 
| IPPROTO_WBMON       |    78              | WIDEBAND Monitoring 
| IPPROTO_WBEXPAK     |    79              | WIDEBAND EXPAK 
| IPPROTO_EON         |    80              | ISO cnlp 
| IPPROTO_VMTP        |    81              | VMTP 
| IPPROTO_SVMTP       |    82              | Secure VMTP 
| IPPROTO_VINES       |    83              | Banyon VINES 
| IPPROTO_TTP         |    84              | TTP 
| IPPROTO_IGP         |    85              | NSFNET-IGP 
| IPPROTO_DGP         |    86              | dissimilar gateway prot. 
| IPPROTO_TCF         |    87              | TCF 
| IPPROTO_IGRP        |    88              | Cisco/GXS IGRP 
| IPPROTO_OSPFIGP     |    89              | OSPFIGP 
| IPPROTO_SRPC        |    90              | Strite RPC protocol 
| IPPROTO_LARP        |    91              | Locus Address Resoloution 
| IPPROTO_MTP         |    92              | Multicast Transport 
| IPPROTO_AX25        |    93              | AX.25 Frames 
| IPPROTO_IPEIP       |    94              | IP encapsulated in IP 
| IPPROTO_MICP        |    95              | Mobile Int.ing control 
| IPPROTO_SCCSP       |    96              | Semaphore Comm. security 
| IPPROTO_ETHERIP     |    97              | Ethernet IP encapsulation 
| IPPROTO_ENCAP       |    98              | encapsulation header 
| IPPROTO_APES        |    99              | any private encr. scheme 
| IPPROTO_GMTP        |    100             | GMTP
|| 101-252| Partly Unassigned |
| IPPROTO_PIM         |    103             | Protocol Independent Mcast 
| IPPROTO_IPCOMP      |    108             | payload compression (IPComp) 
| IPPROTO_PGM         |    113             | PGM 
| IPPROTO_SCTP        |    132             | SCTP 
|| 253-254| Experimentation and testing;
|| 255|Reserved (RFC3692)
| IPPROTO_DIVERT      |    254             | divert pseudo-protocol 
| IPPROTO_RAW         |    255             | raw IP packet 
| IPPROTO_MAX         |    256
| IPPROTO_DONE        |    257 | last return value of `*_input()`, meaning "all job for this pkt is done".  