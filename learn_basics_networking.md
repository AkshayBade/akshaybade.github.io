---
---
# Networking Basics

## Plan 🕙
- [ ]  Networking Basics
    - [ ]  L4 & L7 Layers
    - [ ]  SSL/TLS
    - [ ]  Proxy
    - [x]  DNS
    - [ ]  IPTables
    - [ ]  IPVS
    - [ ]  SDN
    - [ ]  Virtual Interfaces
    - [ ]  Overlay networking

## Index
- [DNS](dns)


### DNS
- Domain Name System
- All devices conected over internet has its own address called IP Address which is a numeric.
- Remembering numeric address is difficult so it is linked with meaningful name called domain name.
- And a server which stores the mapping of this as a directory is called DNS server.

Look up IP Address for something.com
Browser --> DNS recursive resolver (hosted by Internet Service Provider(ISP) like Jio) --> Root Server --> TLD nameserver (Top Level Domain like .com .edu .gov) -> second-level domain server (name of website, here "something") -- (IP Adress) --> Browser -- (IP Adress) --> something server.


👷 WORK IN PROGRESS
