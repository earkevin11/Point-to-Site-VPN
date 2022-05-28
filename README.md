# Point-to-Site-VPN

# What is the point of a VPN connection for Azure?
- Purpose is to allow users to access resources part of an Azure Virtual Network.
- A secure VPN connection is needed to connect to azure resources via the internet via its private IP.

# Difference between a point-to-site VPN vs site-to-site VPN connection
# Point-to-site
- This is for small number of machines that need to connect onto the azure VN.

# Site-to-site VPN connection
- this is for connecting an entire branch office or entire on-prem network onto a azure virtual network

# How to set up a Point-to-Site VPN connection
- Create a Vnet by creating a VM and open ports HTTP and RDP.
- Install IIS


# Ensure that the VNet has a /16 and the subnet has a /24
- Must be enough IP address ranges in the Vnet for additional subnets
- There needs be a special subnet known as the gateway subnet

# Main point of a VPN connection is so that users can connect to the VM via its private IP address

# Create an notepad and save it as html in "wwwrooot"
- Get the public IP and access the page


# Use case: Connect to the VM via its private IP address from personal machine via a VPN connection
- Install a VPN client - which is responsible for establishing a VPN connection onto the azure vnet
- Add a gatewau subnet 
- On the azure side, install a Vnet gateway, which is responsible for establishing the point-to-site VPN connection with your laptop
- Vnet gateway will create the vpn environment, but it needs its own host of VMs for having the VPN connection in place
- Gateway subnet must be EMPTY and VMs in the gateway subnet are configured with the VPN gateway settings
- Gateway subnet must be configured with /29, but Microsoft recommends /27, /26

# Create Virtual Network Gateway
- Link the created network gateway to the azure vnet
- Must create a public IP address
- Bandwith is important because it will dictate how much traffic can flow via the vnet gateway onto the network
- The higher the bandwidth, the more traffic can flow from client via the gateway onto the network

