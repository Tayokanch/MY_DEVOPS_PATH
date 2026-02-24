# Default VPC & Custom VPC

## Default VPC
- Every `AWS Account` comes with a defauly VPC
- Default VPCs have configuration defined by`AWS`
- This VPC is designed for use by AWS so we can quickly and easily deploy resources
- By default there will be one` Default VPC` per region with /16 IPv4 `CIDR block **172.31.0.0/16**`
- Within **Default VPC**, there will be a **Default Subnet** inside each **Availabity Zone** in that region with /20 IPv4 Range
- **Internet Gateway** is always attached to the `Default VPC`
- We are also going to have a `route (0.0.0.0/0)` that points all traffic to thhis `Internet Gateway`
- Therefore, any resources in these **default subnets** will be accessible from the internet by default


## Custom VPC
- This VPCs allow us to create / modify all configurastion associated with the VPC


# Creating a Custom VPC

- on the `Managment Console`
    1. Search `VPC`, click on it and Click `Create VPC`
    2. Give it a **name** and give it an IPv4 CIDR Block e.g **(192.168.0.0/16)**, then click Create VPC
    3. Add a `Subnets` to we can be able to deploy resources on the VPC.By:
        - Click on `subnets`, Click **Create Subnet**, select which VPC we want to the subnet to
        - Give the Subnet a Name
        - Select the **Availaibilty zone** we want the **Subnet** to be Deployed on
        - Provide IPv4 CIDR Block for the **Subnet**. Note this must be in the range of **VPC CIDR** e.g **(192.168.10.0/24)**, then Click Create Subnet. At this stage we have created a Created a Subnet Inside our VPC and we can now Deploy Resources (`e.g EC2`) into our VPC. `NOTE`: This Subnet is currently A **Private Subnet** Therefore, The resources deployed on it can't have access to the internet i.e if we deployed a WebServer unto the `EC2` inside this subnet, this webserver can't be reachable through the internet. To solve this we would configure our VPC with `Internet Gateway`.

    4. `Internet Gateway`
            - click on **internet gateways** then click **create internet gateway**
            - give the **internet gateways** a name , then create the gateway
            - After creating the  **internet gateways** , Click on **Attach to a VPC** then Select the `VPC`
            - Now Devices and our Resources can make use of that internet gateway in our VPC, However, We need to configure the subnets with a **route table** that directs all outbound traffic (0.0.0.0/0) to the Internet Gateway.
    
    5. `Route Table`: 
            - We go back to the **subnets** we are working on, Click **Route Table**'
            - Click on `Create Route Table` Click Add Route
            - For Destination `0.0.0.0`: This is accept traffic from all interface / IP
            - For Target: Pick **Internet Gateway**
            - This would make our Subnet to be officially Public to the Internet
    
    6. `Security Group`: In Addition we could add **Security Group** To control the Traffic that go In and Out of our Resources Deployed on Each Subnets
            - Click on `Security Group`, Click `Create Security Group`
            - Give it a Name , Select the **VPC** it should be part of
            - Add Inbound Rules E.g **Type** ( HTTPS, HTPP, SSH), **PORT**(E.g 443), **Source** Either anywhere 0.0.0.0/0 or a Specific IP Address.
            - Click `Create Security Group`