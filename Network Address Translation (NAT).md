# Network Address Translation (NAT) - IPv4 - The Backbone of Network Connectivity

What is NAT?
- A powerful technology that allows multiple internal devices to share a limited number of public IP addresses for internet access.
- Conserves IPv4 addresses while enabling connectivity & internal server hosting.
  
# Why Is NAT So Important?
NAT was developed to address the problem of IP address exhaustion in the IPv4 world.  Here's how it helps:

- IP Address Conservation: Multiple devices on a private network can access the internet using a single public IP address.
- Enhanced Security: NAT hides the internal network structure, creating an added layer of security against external threats.

# Types of NAT
## NAT Overload (aka PAT):
- Most popular method.
- Shares a single public IP address among many internal devices by using port numbers.
- Devices on a private network are identified by a unique combination of IP address and port number (a socket).
## Static NAT:
- Creates a one-to-one mapping between a private IP address and a public IP address.
- Typically used for allowing external access to internal servers (e.g., email or web servers).
## Dynamic NAT:
- Translates a pool of internal addresses to a pool of public addresses.
- Can be used to hide address conflicts or accommodate larger pools of internal devices.

# Key Points to Remember
NAT is a cornerstone of IPv4 networking.
NAT overload is the most common and versatile form.
Understanding port numbers is crucial for configuring NAT.
