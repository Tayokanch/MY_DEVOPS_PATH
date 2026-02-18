## Networking Basics in AWS

1. `VPC`: 
   - A VPC allows us to use AWS infrastructure in a private and isolated network, where we control IP addressing, routing, and access to our resources.
   - Virtual Private Cloud (VPC) is a secure, isolated network segment hosted within AWS
   - VPC isolates computing respurces from other computing resources available in the cloud
   - it gives the customer full control of the **networking** in the cloud, with access to : `subnetting(IP Address)`, `Routing (Route Tables)`. `Firewalls (NACLs and Security Groups)`, `Gatways`
   - As an AWS customer, we can create mutilple VPC on account Example: `VPC  for Development`, `VPC for Staging`, `VPC Production`, `VPC for ApplicationName`

   # VPC and Regions
   - A `VPC` is specific to a single region. 
   - A `VPC` act like a network boundary in an `AWS Region`
   - By default `VPCs` can't talk to other `Vpcs` or `resources` in same `AWS Region` unless they are explicitly configured to do so
   - Every `VPC` has a range of **IP Address** assigned to it called the `CIDR Block`. This **IP Addresses** are the IP resources deployed on this VPC will use
---

2. `Subnets`:
   -  A `subnet` is a group of `IP Addresses ` within the range of our `VPC CIDR Block`
   -  A `subnet` resides within a single **Availability Zone**
   -  A `subnet` can be made **public** or **private** to allow external access to resources within them. 
      -  A **Private Subnet** is a subnet that isn't exposed to the internet i.e The resources in the subnet cant be reach through the Internet E.g Database
      -  A **Public Subnet** is meant for the public so that user can actually access the web server. Example Hosting a website
      -  Note: The first **4 IP Addresses** of a subnet are reserved and cannot be used. E.G:
      -  We have a `Subnet` with CIDR range 192.168.10.24, 
         -  *IP 192.168.10.0* : Reserved **Network Address** and can't be used
         - *IP 192.168.10.1 - 192.168.10.3* : **Reserved for AWS** and can't be used 
         -   *IP 192.168.10.255*: Which is the Last IP of a subnet is reserved as the **Broadcast address**
  
 ## VPC and subnet IP ranges

   ```yaml
   VPC: 10.0.0.0/16
   Subnets:
   - name: Subnet1
      range: 10.0.1.0/24
      usable: 10.0.1.4 - 10.0.1.254
   - name: Subnet2
      range: 10.0.2.0/24
      usable: 10.0.2.4 - 10.0.2.254

   ```

   ```yaml
   VPC: 192.168.0.0/16
      Subnets:
      - name: Subnet1
         range: 192.168.1.0/24
         usable: 192.168.1.4 - 192.168.1.254
      - name: Subnet2
         range: 192.168.2.0/24
         usable: 192.168.2.4 - 192.168.2.254
      - name: Subnet3
         range: 192.168.100.0/24
         usable: 192.168.100.4 - 192.168.100.254
      - name: Subnet4
         range: 192.168.200.0/24
         usable: 192.168.200.
   ```

 ## VPC External Connectivity
   - When **subnet** are created first within AWS, that subnet by default is going to be a private subnet, therefore not exposed to the internet, if it need a public access, we have to explicitly change it to a public subnet to give access to the internet, and to make a Private Subnet public, we make use of a service called `Internet Gateway`
---
3. `Internet Gateway`
   
   - Internet Gateway are assigned to VPC and allows subnets in a VPC to communicate with the Internet and vice versa
   - Internet Gateway determines if a subnet is public or private
---

4. `NAT Gateway`
   - With a Nat Gateway a connection must be initiated from within the VPC first i.e if the internet tries to send a request to a **private subnet**, the request is going to be blocked. However, if a private subnet sends a request out to the internet and gets a response, it going to allow the the response to the **Private Subnet**

   - An important dinstiction btw *Internet Gateway* and  *NAT Gateway* is that, *Internet Gateway* allows either side to initiate the connection, But * Nat Gateway* expect the connection to be initiated from the **private subnet**


   ## `Internet Gateway and NAT Gateway Compliment each other`

## Internet Gateway and NAT Gateway Complement Each Other

- An Internet Gateway (IGW) is attached to a VPC to allow **public subnets** to communicate with the internet.

  - Any EC2 instances in a public subnet with routes to the IGW can initiate outbound connections and receive inbound traffic from the internet.

- A NAT Gateway (NAT-GW) allows resources in **private subnets** to access the internet without exposing them publicly.

  - The NAT Gateway must be deployed in *a public subnet* and requires an *Internet Gateway* to route traffic out to the internet.

  - Resources inside a *Private Subnet* cannot receive inbound connections from the internet, but they can initiate outbound requests, and the responses will return securely.
  
---

## Example: EC2 in a Private Subnet Needing Internet Access

`Imagine:`
- An EC2 instance running in a private subnet (10.0.2.0/24)
  
- The instance needs to update packages (yum update / apt-get upgrade) or download software from the internet

- We don’t want the instance to be publicly reachable for security

`Flow of traffic:`

- The EC2 instance in the private subnet sends a request to the NAT Gateway (located in a public subnet).

- The NAT Gateway uses its Elastic IP and sends the request through the Internet Gateway to the internet.

- The response comes back through the Internet Gateway → NAT Gateway → EC2 instance.


---

5. Virtual Private Gateway (VPG) – Example: EC2 in Private Subnet Connecting to On-Prem PostgreSQL

A **Virtual Private Gateway (VPG)** enables a **secure, encrypted connection** between an **AWS VPC** and external private networks, such as on-premises data centers, homelabs, or branch offices.

## Example Scenario

You have:  
- An **EC2 instance running a web application** in a **private subnet** within an AWS VPC  
- A **PostgreSQL database running on an on-prem (homelab) server**

Because:  
- The EC2 instance is in a **private subnet** and does not have direct internet access  
- The PostgreSQL server is **not publicly exposed**  

They **cannot communicate over the public internet**.

---

## How a Virtual Private Gateway (VPG) Helps

- Attach a **VPG** to your **VPC**  
- Configure a **Site-to-Site VPN connection** between AWS and your on-prem network  
- The VPN creates an **encrypted tunnel** over the internet between your VPC and the on-prem environment

### Routing Configuration

- Traffic from the EC2 instance destined for the on-prem network is sent to the **VPG**  
- Traffic from the on-prem network destined for the VPC is sent through the **VPN tunnel**

---

## Benefits of This Setup

- The EC2 instance in the private subnet can **securely connect to the on-prem PostgreSQL database** using private IP addresses  
- The database is **not exposed to the public internet**  
- **No NAT Gateway or public IPs** are required  
- Traffic is **encrypted end-to-end** over the internet, ensuring secure communication


---

6. `Direct Connects`: This is another way of connecting to AWS an Private Resources. This works by we as a customer going to a location called a `DX location` or a `Direct Connect Location` and have to physically connect our router to that specific Location. This location has a direct high-speed connection to **AWS regions** which allows us to secureluy access our resources with AWS through the Direct Connect. So instead of going over the internet, we have a direct and secure high-speed link to that locatio which provides `LOW LATENCY`