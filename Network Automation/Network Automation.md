# Use Cases
Generating configuration backups

Ensuring there are no duplicate IP addresses in the network

Validating that all OSPF speakers have unique RIDs, and peers are in the "FULL" state

Testing that each adjacent network node is on the same subnet

Validating that all devices comply with the company baseline policy (must be running a specific software version, firewall rules are compliant, etc.)

Checking the health of network devices (high CPU utilization, memory use, etc.)

Testing that all interfaces configured with IP addresses are in the "UP" state

And much, much more...

# Which of the following options are valid reasons to automate network management? (Choose all that apply)
- Faster deployment of configuration changes
- Reduction of costs
- Reduces the probability of human error

# Which of the following best describes "configuration drift"?
- Gradual changes over time that result in the running configuration diverging from the intended configuration.

# How can automation best solve the problem of configuration drift?
- Automation can allow you to enforce the desired state of the network from a single, centralized node.

# With respect to the "pull" model, what is the name given to the piece of software running on the managed device that is used to communicate back to the master node?
- agent

# Which of the following options best describes Ansible?
- Ansible is an agentless automation tool that uses the "push" model

# Which of the following is the name of the Ansible component used to define the set of tasks to be performed on the target devices?
- playbook

# Ansible in Action
***
    ---
    - name: "Test Playbook for fun"
      hosts: uk
      connection: network_cli
      gather_facts: false
    
      vars:
        ansible_user: john
        ansible_ssh_pass: cisco
        ansible_network_os: "cisco.ios.ios"
    
      tasks:
        - name: "Configure Cisco Devices"
          cisco.ios.ios_config:
            src: "network_configs.j2"
          register: device_output
    
        - name: "Print device output"
          debug:
            msg: "{{ device_output }}"
# Which of the following is the smallest unit of operation used to define an action to take inside an Ansible playbook?
- task
