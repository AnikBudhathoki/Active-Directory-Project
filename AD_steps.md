# Set up Virtual Machines

1) Set up windows 10 client
2) Set up windows 2019 server
3) Change network settings
    - Configure network adpater 1 to NAT network
    - Configure network adapter 2 to Internal network (I named mine "intnet")
  - Obtain ISO files for windows
  - Create Admin account in server

# Set up IP Addressing

As per diagram we have two NICs. One is for internet and one is for internal network. Internal NIC will get IP address from home router.

1) Open Network settings
2) Configure adapter option
     - Find which one is home network and rename to Internet
     - Other one is internal network
3) Change the internal Network IP Ranges for DHCP scope
   ![Internal IP Config](https://media.discordapp.net/attachments/645079991310090243/1398730886178148392/Internal_Network_Setup.png?ex=68866d26&is=68851ba6&hm=5639e5d5f59a943918edf1cb5f1cb9b3fce7cd4572f04e8c15b3d62924a812e7&=&format=webp&quality=lossless)
   
  
   
