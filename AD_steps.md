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

# Create A Domain

1) Add roles and features
2) Install Active Directory Domain Services
3) Add a new forest (Like root, head): mydomain.com
4) Apply configurations and Install:

    ![AD Configs](https://media.discordapp.net/attachments/645079991310090243/1398736202365927684/AD_Config.png?ex=68867219&is=68852099&hm=d70b6cd68570596d64df3987497ad8bf207aec8abae0dcf1c14076dfca0b0b36&=&format=webp&quality=lossless&width=752&height=541)

5) Create own Domain Adminstrator Account -> Replace the default one provided at installation

   ![Anik Budhathoki (me) Admin Account](https://media.discordapp.net/attachments/645079991310090243/1398748136121434184/new_admin_account.png?ex=68867d37&is=68852bb7&hm=6019565bcf2d2588817c5d2bfb6e30011db5f7b5ba3918b8ba71238e9eab0106&=&format=webp&quality=lossless)
   
   
