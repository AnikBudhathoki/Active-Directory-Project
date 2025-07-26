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
   MY username: a-abudhathoki
   MY password: Password1

   ![Anik Budhathoki (me) Admin Account](https://media.discordapp.net/attachments/645079991310090243/1398748136121434184/new_admin_account.png?ex=68867d37&is=68852bb7&hm=6019565bcf2d2588817c5d2bfb6e30011db5f7b5ba3918b8ba71238e9eab0106&=&format=webp&quality=lossless)


# Install RAS/NAT

Purpose: When creating the windows 10 client, it will allow this client to be on own private virtual network, but it is still able to access internet through the Domain Controller. RAS/NAT on the DC will allow the windows 10 client to do this

1) Add roles/features
2) Install Remote Access with Routing
3) Remote Access and Routing Installation Configurations:

![Remote Access Config](https://media.discordapp.net/attachments/645079991310090243/1398751492021813268/Remote_Access_Routing_Config.png?ex=68868057&is=68852ed7&hm=ec4c7cd9adf9539a5c4a9998f59b2a0e040c13905711a9af0e699bb4d19db6f6&=&format=webp&quality=lossless)

# Install DCHP Server

Purpose:  Allow computer on the network to automatically get their IP Adresses. These include clients, users, adminstrators, etc.

1) Add Role/Features
2) DHCP Server
3) Create IP range from 172.16.0.100 - 172.16.0.200
   
![DHCP Config](https://media.discordapp.net/attachments/645079991310090243/1398756739264024586/DHCP_IP_Ranges.png?ex=6886853a&is=688533ba&hm=d04b77325bbb94954bc00363fdbdd1ed189bec8989a0a40fdea1f027bb13bfaf&=&format=webp&quality=lossless&width=752&height=639)


#Powershell Script to Automate Creating users

1) Run Powershell ISE as Adminstrator
2) I wrote/saved this code in notepad and saved it as a .ps1 file (Powershell script)
   ```
   ?# ----- Edit these Variables for your own Use Case ----- #
    $PASSWORD_FOR_USERS   = "Password1"
    $USER_FIRST_LAST_LIST = Get-Content .\names.txt
    # ------------------------------------------------------ #

    $password = ConvertTo-SecureString $PASSWORD_FOR_USERS -AsPlainText -Force
    New-ADOrganizationalUnit -Name _USERS -ProtectedFromAccidentalDeletion $false

    foreach ($n in $USER_FIRST_LAST_LIST) {
    $first = $n.Split(" ")[0].ToLower()
    $last = $n.Split(" ")[1].ToLower()
    $username = "$($first.Substring(0,1))$($last)".ToLower()
    Write-Host "Creating user: $($username)" -BackgroundColor Black -ForegroundColor Cyan
    
    New-AdUser -AccountPassword $password `
               -GivenName $first `
               -Surname $last `
               -DisplayName $username `
               -Name $username `
               -EmployeeID $username `
               -PasswordNeverExpires $true `
               -Path "ou=_USERS,$(([ADSI]`"").distinguishedName)" `
               -Enabled $true
    }
    ```

   - $PASSWORD_FOR_USERS = "Password1": This variable sets a temporary password
         - Important Security Note: In a real-world production environment, hardcoding passwords directly in scripts like this is generally not recommended due to security risks. For production, you would typically use more secure methods like prompting for a password              securely (Read-Host -AsSecureString), retrieving from a secure vault, or having users set their own password on first login (which this script does not automatically enforce). This script sets PasswordNeverExpires to $true but does not force a password                   change at next logon
    - $USER_FIRST_LAST_LIST = Get-Content .\names.txt: This line reads the content of a text file named names.txt into a variable called $USER_FIRST_LAST_LIST. It expects each line in names.txt to contain a user's first and last name

    - ConvertTo-SecureString: This cmdlet converts plain text into a SecureString object
    - $PASSWORD_FOR_USERS: This is the plain-text password defined earlier ("Password1")
    - -AsPlainText: Specifies that the input string is plain text and should be converted.

    - Force: This parameter is often used with ConvertTo-SecureString when converting from plain text to bypass a warning that it's less secure to do so
    - New-ADOrganizationalUnit: This cmdlet creates a new Organizational Unit (OU) in Active Directory.
    - Name _USERS: Specifies the name of the new OU. It's named _USERS (the underscore often helps it sort to the top of the OU list in ADUC).
    - ProtectedFromAccidentalDeletion $false: By default, when you create OUs in ADUC, they are protected from accidental deletion. This parameter explicitly sets that protection to $false, meaning the OU can be easily deleted later without first unchecking a box in          its properties
  
    - <ins>IN SUMMARY</ins>:
    - This PowerShell script automates Active Directory user creation: it first defines a temporary password and reads a list of "First Last" names from names.txt. For each name, it generates a username (first initial + last name), creates an "_USERS" Organizational          Unit (OU) if it doesn't exist, and then uses New-ADUser to create an enabled user account with the specified name, a non-expiring password, and places it within the dynamically located _USERS OU in the domain, providing console feedback during the process.

3) Enable execution of all Scripts using:
```
Set-ExecutionPolicy Unrestricted
```
4) Run the Script

![Powershell Script Running](https://media.discordapp.net/attachments/645079991310090243/1398764186204373022/Powershell_Script_running.png?ex=68868c29&is=68853aa9&hm=6020e371977acd36fd1f2656659ba316309c816d446b1e6ea01c9d94d4270c1e&=&format=webp&quality=lossless)



   
