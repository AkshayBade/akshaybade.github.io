---

---
# How Containers Work?

1. [What are Linux Namespaces](#linux-namespaces)
    * [Practical](#practical-namespaces)
2. [What is Linux CGroups](#linux-cgroups)
    * [Practical](#practical-cgroups)
3. [Project](#project)
    * [Run Process Within Namespace](#run-process-within-namespace)
    * [Access From Outside](#access-from-outside)
4. [Eureka Docker](#eureka)


## Linux Namespaces
- Provides isolation for processes

![Kernal process namespace](/assets/images/PID-Namespace.jpg "PID Namespace")

- Partitions kernel resources per namespace
- Gives look and feel of a complete VM

#### Namespace Types
- **CGroup Namespaces**
- **User namespace**: owns set of user ids and group ids
- **ProcessID (PID) namespace**: assigns and manages PIDs to processes within namespace. 1st process has ID 1
- **Network namespace**: has its own routing table, IP addresses, firewall, sockets and other network resources
- **Mount namespace**:
- **InterProcessCommuniction namespace**
- **UNIX time sharing namespace**

### Practical Namespaces
Check ids for current user
```console
$ id
uid=123(bade) gid=4221()
```

Create namespace with its own user and PID
```console
$ unshare --user --pid --map-root-user --mount-proc --fork bash

@command unshare      : command which creates a new namespace for you
@param --user         : creates namespace with its own user
@param --pid          : creates namespace with its own pid table
@param --map-root-user: links current user as root for new isolated area
@param --mount-proc   : creates a proc file system for process lifecycle management
@param --fork         : starts first process called bash within namespace

root$ ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 15:26 pts/0    00:00:00 bash
root       353     1  0 15:27 pts/0    00:00:00 ps -ef

root$ id
uid=0(root) gid=0(root) groups=0(root),65534(nfsnobody)

```

Create namespace with shared PID
```console
bade@machine $ unshare --user --map-root-user --fork bash
root@machine $

root@machine $ ps
  PID TTY          TIME CMD
22626 pts/0    00:00:00 unshare
22627 pts/0    00:00:00 bash
23009 pts/0    00:00:00 ps
32027 pts/0    00:00:00 bash
root@machine $
```


## Linux CGroups

### Practical CGroups


## Project

### Run Process Within Namespace

### Access From Outside

## Eureka

