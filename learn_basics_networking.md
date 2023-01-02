---
---
# Networking Basics

## Plan 🕙
- [ ]  Networking Basics
    - [x]  L4 & L7 Layers
    - [x]  SSL/TLS
    - [ ]  Proxy
    - [x]  DNS
    - [ ]  IPTables
    - [ ]  IPVS
    - [ ]  SDN
    - [ ]  Virtual Interfaces
    - [ ]  Overlay networking

## Index
- [DNS](dns)
- [L4 & L7 network Layers](l4-l7-layers)
- [SSL/TLS](tls/ssl)
---
### DNS
- Domain Name System
- All devices conected over internet has its own address called IP Address which is a numeric.
- Remembering numeric address is difficult so it is linked with meaningful name called domain name.
- And a server which stores the mapping of this as a directory is called DNS server.

Look up IP Address for something.com
Browser --> DNS recursive resolver (hosted by Internet Service Provider(ISP) like Jio) --> Root Server --> TLD nameserver (Top Level Domain like .com .edu .gov) -> second-level domain server (name of website, here "something") -- (IP Adress) --> Browser -- (IP Adress) --> something server.

---
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

---
### TLS/SSL
SSL(Secure Session Layer) is older version of TLS, But certificate is still called SSL certificate.

TLS(Transport Layer Security) is cryptographic protocol to securely communicate over network.
- Encryption
- Authentication

> HTTPS = HTTP + TLS
**TLS Handshake**
This process depends on TLS version used. dvance versions reduces the handshake hops hence time.
 > Client --("Clien random", TLS version, supported cipher suites)--> Server --("Server random", SSL certificate, Chosen cipher suite)--> Client
 > Client --(SSL certificate)--> SSL certificate authority --(Verified Server domain)--> Client
 > Client --("Master random string" encrypted with public key(part of SSL cert received))--> Server
 > Client & Server --("client random", server random, master random, public key)--> Session Key
 
 - Session key is now for further communication between client & server.

---

👷 WORK IN PROGRESS
