# 1. ACCESS CONTROL LISTS Concepts
## Key Points
Default Behavior: Traffic not explicitly permitted is denied by default.

Ordering: ACL entries are processed top-down.

Steps to Implement: 

1) Plan: Determine what traffic to filter (permit/deny)

2) Create List: Write ACL entries specifying the traffic types.

3) Apply: Attach the ACL to a router interface (inbound/outbound).

## Purpose
Filter network traffic on a router, controlling what gets forwarded and what gets blocked => Network Security

## Router's Behavior
Checks each packet against the ACL entries in order. If a match is found, action is taken (permit or deny). If no match is found, the packet is implicitly denied.

# 2. STANDARD ACLS

## Purpose
Basic IP address-based traffic filtering on a router. Can only match based on source IP address. Cannot filter based on destination address, protocols (TCP, UDP, etc.), or port numbers.

## Important Notes

Standard ACLs have an implicit deny any any at the end. If no ACL entry matches, the packet is dropped!

Use the "host" keyword to specify individual IP addresses.

Access lists are processed in order – the first match determines the permit/deny action.

## Basic ACL Structure

### Plan

Define what traffic to permit/deny based on its source IP address.

### Create

(config)# access-list [number 1-99] [permit | deny] [source address] 

Example:

(config)# access-list 1 deny host 10.16.0.10

(config)# access-list 1 permit any 

### Apply an ACL to a router interface in the specified direction.

(config-if)# ip access-group [number 1-99] [in | out]


# 3. STANDARD ACLS WITH WILDCARD MASKS

## Purpose
Filter traffic based on network address ranges rather than individual IP addresses, reducing the number of ACL entries needed.

## Important Notes

Implicit Deny: Always include a permit any statement to avoid blocking everything.

OSPF Connection: Wildcard masks work the same way in OSPF and standard ACLs.

## How Wildcard Masks Work

Inversion of Subnet Mask:  A wildcard mask is the opposite of a subnet mask. Where the subnet mask has a '1', the wildcard mask has a '0' (indicating a match). Where the subnet mask has a '0', the wildcard mask has a '1' (indicating "don't care")

Example:

10.16.0.0 /24 network

Subnet Mask: 255.255.255.0

Wildcard Mask: 0.0.0.255


## ACL Syntax with Wildcard Mask

access-list [number 1-99] [permit | deny] [network address] [wildcard mask]

Example:

access-list 2 deny 10.16.0.0 0.0.0.255 

access-list 2 permit any

This ACL blocks the entire 10.16.0.0/24 subnet and permits any other traffic.


# 4. Wildcard Masks for Irregular Subnets

## Purpose
When network addresses don't fall on neat octet boundaries (e.g., /21, /27), wildcard masks let you filter traffic based on those specific networks.

## Important Notes
The concept is identical to how wildcard masks are used in OSPF. Implicit Deny: Include a permit any statement to avoid unintentionally blocking all traffic.

## Steps:

### Identify the subnet mask:
In each octet, subtract the subnet mask value from 255 to get the wildcard mask value.

Example: 10.16.0.0/21

Subnet Mask: 255.255.248.0

Wildcard Mask: 0.0.7.255

### Applying Wildcards in ACLs

Syntax: access-list [number] [permit | deny] [network address] [wildcard mask]

Example: 
access-list 3 deny 10.16.0.0 0.0.7.255

access-list 3 permit any 

ip access-list 3 in 


# 5. Extended ACLs: Beyond Basic Filtering

## Purpose
Extended ACLs provide fine-grained control over network traffic by filtering based on a wide range of criteria: 

- Match on source/destination IP addresses

- Match on Layer 3 protocols (ICMP, TCP, UDP, etc.)

- Match on Layer 4 port numbers (e.g., 80 for HTTP, 22 for SSH)

- Filter on even more specific criteria (like ICMP message types)

- Filtering Process

## Important Notes
Extended ACLs can be complex. Monitor ACL hit counters to ensure the ACL is working as intended. Always remember the implicit 'deny any any' at the end!

## Performance

Plan, create, apply

## Command
access-list [number] [permit | deny] [protocol] [source] [destination] [options]

number: Standard ACLs: 1-99; Extended ACLs: 100-199 or 2000-2699

protocol: ICMP, TCP, UDP, or other supported protocols

source: Source IP address (can use wildcards)

destination: Destination IP address (can use wildcards)

options:
eq [port number]: Matches specific destination port (e.g., eq 80 for HTTP)

log: Generates log messages for matched packets

### Example Scenario
User - Bob (10.16.0.10)

Goals:

Block Bob's ICMP pings to 192.168.1.100

Block Bob's HTTP (port 80) traffic to the same server

Allow all other traffic from Bob

ACL Entries:

access-list 100 deny icmp 10.16.0.10 192.168.1.100 any 

access-list 100 deny tcp 10.16.0.10 192.168.1.100 eq 80

access-list 100 permit ip any any

# 6. NAMED ACLs

## Purpose
Provide a more manageable way to create and maintain ACLs, especially with multiple entries. Easier to manage and modify than numbered ACLs. You can insert or remove lines without rewriting the entire ACL. 

## Important Note
Use tools like show access-list to check hit counters.

Test and troubleshoot to ensure the ACL is working as intended.

Mind Your Routing: ACLs only work on interfaces where traffic is routed THROUGH the device. Beware of unintended bypasses!

## Command

ip access-list extended [name]

[permit | deny] [protocol] [source] [destination] [options]

Example: 

ip access-list extended Our-ACL 

deny tcp host 10.16.0.10 any eq 21   

deny ip 10.16.0.0 0.0.0.255 10.16.16.0 0.0.7.255  

deny icmp 10.16.0.0 0.0.0.255 10.16.2.0 0.0.0.255

permit ip any any

### Applying Named ACLs:

interface [interface-id]

ip access-group Our-ACL in 




