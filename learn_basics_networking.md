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
- [L4 & L7 network Layers](l4l7 Layers)


### DNS
- Domain Name System
- All devices conected over internet has its own address called IP Address which is a numeric.
- Remembering numeric address is difficult so it is linked with meaningful name called domain name.
- And a server which stores the mapping of this as a directory is called DNS server.

Look up IP Address for something.com
Browser --> DNS recursive resolver (hosted by Internet Service Provider(ISP) like Jio) --> Root Server --> TLD nameserver (Top Level Domain like .com .edu .gov) -> second-level domain server (name of website, here "something") -- (IP Adress) --> Browser -- (IP Adress) --> something server.


### L4 L7 Layers
**L4 Layer**:
- Transport layer of OSI model.
- Helps load balance requests coming to server
- Based on number of requests & Server response time
- Simple packet level load balancing where routing happends based on packer header & no need to decrypt request content
- ➖ Cant route based on request content, like localization rule, media type

**L7 Layer**:
- Application layer  of OSI model
- Helps LB based on more details like HTTP header information, request message, cookies, URL type
- L7 inspects requsts - > decrypts -> interprets -> creates new TCP connection with respective instaces
- Performance hit

**Commonalities**
- Helps load balancing requests
- Network logging?
- Scaling network
- Application performance -> by selecting best responding server
- Availablility -> by distributing load across the instances



👷 WORK IN PROGRESS
