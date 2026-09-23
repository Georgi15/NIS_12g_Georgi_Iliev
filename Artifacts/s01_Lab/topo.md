# s01 Lab Explanation

In this lab we create two virtual machines named gw and sv.

## Network Adapters

The gw has three adapters. Two of them are used for LAN1 and LAN2, one adapter for each, put into internal network so that we can create an isolated network. And the last one is in Bridged adapter mode so that it can get its ip directly from the same dhcp as the host machine and have access to the internet that way. The sv virtual machine on the other hand has only one adapter, that being the connection to LAN1, again in internal network, so we finalize the LAN1 connection for now.

## Configuration

In the gw virtual machine we have turned ip forwarding on by changing the value in the `/etc/sysctl.conf` file to 1, and we have added static ips for the two LAN networks, using 10.10.10.1/30 for LAN1 and 10.10.20.1 for LAN2, in the `/etc/network/interfaces` file. On the sv virtual machine we have only given a static ip to the adapter connected to the LAN1 network, giving it an ip of 10.10.10.2/30 in the same file, just for a different machine.

## Topology

So finally we have:

```
-----------------                     -----------------            -----------------
|               |   10.10.10.0/30     |               |     DHCP   |               |
|               |       LAN1          |               |     WAN1   |               |
|    Server     |   .2------------->.1|    Gateway    |  --------->|  Host Machine |
|               |                     |    enabled    |            |               |
|               |                     | ip forwarding |            |               |
-----------------                     -----------------            -----------------
                                              .1
                                              |
                                              |10.10.20.0/30
                                              |LAN2
                                              |
                                              v
```
