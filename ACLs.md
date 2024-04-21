# ACLs Concepts
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
How ACLs Work

## How to do
Plan: Determine what traffic to filter (permit/deny)
Create List: Write ACL entries specifying the traffic types.
Apply: Attach the ACL to a router interface (inbound/outbound).

## Router's Behavior
Checks each packet against the ACL entries in order.
If a match is found, action is taken (permit or deny).
If no match is found, the packet is implicitly denied.

