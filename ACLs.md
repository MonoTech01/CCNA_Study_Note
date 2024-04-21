# 1. ACLs Concepts
## Key Points
Default Behavior: Traffic not explicitly permitted is denied by default.

Ordering: ACL entries are processed top-down.

Steps to Implement: 1) Plan 2) Create List 3) Apply to interface

## Purpose
Filter network traffic on a router, controlling what gets forwarded and what gets blocked = Your Network's Security Guard

## How it works
Router: The gated community

ACL: List of permitted/denied visitors held by the security guard

Traffic: People trying to enter/exit

## How to do
Plan: Determine what traffic to filter (permit/deny)

Create List: Write ACL entries specifying the traffic types.

Apply: Attach the ACL to a router interface (inbound/outbound).

## Router's Behavior
Checks each packet against the ACL entries in order.

If a match is found, action is taken (permit or deny).

If no match is found, the packet is implicitly denied.


# 2. Standard ACLs

## Purpose
Basic IP address-based traffic filtering on a router.

Standard ACLs have an implicit deny any any at the end. If no ACL entry matches, the packet is dropped!

Use the "host" keyword to specify individual IP addresses.

Access lists are processed in order – the first match determines the permit/deny action.

## Limitations:

Can only match based on source IP address. Cannot filter based on destination address, protocols (TCP, UDP, etc.), or port numbers.

## Basic ACL Structure

### Plan:

Define what traffic to permit/deny based on its source IP address.

### Create:

(config)# access-list [number 1-99] [permit | deny] [source address] 

Example:

(config)# access-list 1 deny host 10.16.0.10

(config)# access-list 1 permit any 

### Apply:

(config-if)# ip access-group [number 1-99] [in | out]

## Commands

access-list [number] [permit | deny] [source address] - Creates an ACL entry

ip access-group [number] [in | out] - Applies ACL to a router interface in the specified direction.

# 3. Standard ACLs with Wildcard Masks

## Purpose
Filter traffic based on network address ranges rather than individual IP addresses, reducing the number of ACL entries needed.

## How Wildcard Masks Work

Inversion of Subnet Mask:  A wildcard mask is the opposite of a subnet mask.

Where the subnet mask has a '1', the wildcard mask has a '0' (indicating a match)

Where the subnet mask has a '0', the wildcard mask has a '1' (indicating "don't care")

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

## Important Notes
Implicit Deny: Always include a permit any statement to avoid blocking everything.
OSPF Connection: Wildcard masks work the same way in OSPF and standard ACLs. Understanding one helps with the other!
