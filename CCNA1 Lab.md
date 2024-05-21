# Router 
Entering Configuration Mode

en - Enters privileged EXEC mode for administrative tasks.

config t - Enters global configuration mode for configuring general router settings.

## Basic Settings
host R1 - Sets the router's hostname to “R1” for easier identification. 

enable secret class12345 - Sets a secret password for entering privileged EXEC mode (Aka enable mode).

service password-encryption - Encrypts all passwords.

banner motd #Authorized Access Only# - Sets a message of the day (MOTD) displayed on login. 

security passwords min-length 10 - Enforces a minimum password length of 10 characters for all password types. 

login block-for 120 attempts 2 within 30 - Blocks login attempts for 120 seconds after 2 failed attempts within 30 minutes.

## Name Resolution
no ip domain-lookup - Disable DNS lookups on the router.

ip domain-name CCNA.com - Sets a default domain name for name resolution.

## Cryptographic Keys
crypto key generate rsa 1024 - Create a 1024-bit RSA key for secure communication (e.g., SSH).

## Console Configuration
line console 0 - Go to the console configuration mode. 

password class123 - Set a password for console login. 

login - Enable login prompts.

logging synchronous - Log console activity in real-time. 

exec-timeout 60 - Terminate inactive console sessions after 60 seconds.

## Virtual Terminal Configuration
line vty 0 15 - Configure virtual terminal lines 0 to 15 for telnet or ssh access.

password class123 - Set a password for vty login.

transport input ssh - Specify SSH as the login protocol. SSH can be replaced by telnet or all (SSH + Telnet).

login local - Uses local user accounts storing the device for authentication.

logging synchronous - Log vty activity in real-time. 

exec-timeout 60 - Terminate inactive vty sessions after 60 seconds.

## SSH settings
ip ssh version 2 - Enables SSH version 2 for secure remote access.

ip ssh time-out 120 - Sets the SSH session inactivity timeout to 120 seconds.

username admin privilege 15 secret cisco123 - Creates a username "admin" with the highest privilege level (15) and a password " cisco123".

## Configuring Network Interfaces (IPv4, IPv6)
interface g0/0 - Enter configuration mode for Gigabit Ethernet interface 0/0.

ip address 192.168.1.126 255.255.255.224 - Assign an IP address and subnet mask for the interface connected to the First Floor.

description First Floor LAN - Add a descriptive label for clarity.

ipv6 address 2001:DB8:ACAD:A::1/64 - Assigns an IPv6 address and subnet mask. 

ipv6 address fe80::1 link-local - Enables link-local IPv6 addressing for the interface.

no shutdown - Activate the interface.

exit - Exit interface configuration mode.

### Note: IPv6 needs to be enabled
ipv6 unicast-routing - Enables IPv6 unicast routing on the router.

## Save the configuration
copy run start

# Switch
enable

config t

enable secret class12345

service password-encryption

banner motd #Authorized Access Only#

no ip domain-lookup

line console 0

password cisco12345

login

logging synchronous

exec-timeout 60

exit

line vty 0 15

password cisco12345

login

logging synchronous

exec-timeout 60

exit

interface vlan 1

ip address 192.168.1.157 255.255.255.240

no shutdown

ip default-gateway 192.168.1.158

exit

copy running-config startup
