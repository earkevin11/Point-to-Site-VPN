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

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170834722-6139d7ea-d9e7-4e1c-b9dc-9303ff0e8819.png" height="100%" width="100%" alt="application gateway"/>

<p/> 


# Main point of a VPN connection is so that users can connect to the VM via its private IP address

# Create an notepad and save it as html in "wwwrooot"
- Get the public IP and access the page
- You will have to save it as UTC and change file type to "All documents"


# Use case: Connect to the VM via its private IP address from personal machine via a VPN connection
- Install a VPN client - which is responsible for establishing a VPN connection onto the azure vnet
- On the azure side, install a Vnet gateway, which is responsible for establishing the point-to-site VPN connection with your laptop/workstation
- For the vnet gateway, we need a gateway subnet within the Virtual Network created
- Vnet gateway will create the vpn environment, but it needs its own host of VMs for having the VPN connection in place
- Gateway subnet must be EMPTY and VMs in the gateway subnet are configured with the VPN gateway settings
- Gateway subnet must be configured with /29, but Microsoft recommends /27, /26

# Add a gateway subnet
- Select the virtual network > subnets > add gateway subnet 
- Note, a Virtual Network can only have one gateway subnet

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170837802-71f607c4-4fa6-4019-b500-7483e4a13651.png" height="100%" width="100%" alt="application gateway"/>

<p/> 

# Create Virtual Network Gateway
- Link the created network gateway to the azure vnet
- Must create a public IP address
- Bandwith is important because it will dictate how much traffic can flow via the vnet gateway onto the network
- The higher the bandwidth, the more traffic can flow from client via the gateway onto the network

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170837970-efec7ccf-c427-4bd3-807d-fed4d3fc63ee.png" height="65%" width="65%" alt="application gateway"/>

<p/> 

# Set up certificates for authentication
- Ensure that certificates are installed on client's machines as a form of authentication
- Not just any machine can connect to an azure virtual network.
- Install the certificates
- Create a client certificate from a root certificate
- Enterprises will have a enterprise CA authority

# Use azure powershell to create a self-signed root certificate then create the client certificate
- root certificate -> client certificate
- install client certificate on machine that will establish the point-to-site VPN connection



# Configure the point-to-site configuration on Azure Portal
- Virtual network gateway > point-to-site configuration > configure now
- Add an address pool - an IP address will be assigned to the client machine trying to establish a vpn connection
- Select tunnel type > Azure certificate as authentication type
- Export VPNRoot onto the desktop > don't export the private key > finish 
- Go to the Vnet gateway > point-to-site configuration > upload the root certificate's data onto public certificate data on the virtual network gateway
- The root certificate is part of the virtual network gateway and the client cert is on the client's workstation
- The client cert will be authenticated against the root certificate on the gateway 
- Anyone who is trying to establish a connection to the virtual network gateway must have the client certificate installed

<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170839871-bb5dbe05-c952-4703-ab4e-a72bafa087b9.png" height="65%" width="65%" alt="vnet gateway"/>

<p/> 


# Open up root certificate that was exported and copy the data onto the vnet gateway
<p align="center">
  
<img src="https://user-images.githubusercontent.com/104326475/170839940-14f69f2d-b6ed-41e6-9054-c5e79eb9378b.png" height="65%" width="65%" alt="vnet gateway"/>

<p/> 



