## AWS EC2

- EC2 service provides secure, resizable compute capacity in the cloud
- EC2 allows you to provision a server on AWS within a minute


## Amazon Machine Image (AMI)

- `AMI` is an image that provides the information required to lunch an Ec2 instance e.g **Ubuntu Image**
  
- With `AMI` we can used to deploy multiple identical EC2 instance. 

- Its like a blueprint that contains information suh as what OS and what Software / Packages should be installed on an Instance
- We could think of `AMI` as an installer disk used for booting a new server
- `AMIs` can be fully customized to:
  - We can add application source code to our `AMI` so when we deploy our `EC2` the source code are already in there
  - Add our Appplication dependecies
  - customized firewall



## Instace Types

`General Purpose EC2`
- Provide a good blance of compute , memory, and networking resources
- can be used for diverse workloads
- ideal for applications that use reources in equal proportions


`Compute Optimized EC2`
- optimized for compute-heavy applications
- Contains high performance CPU
- Ideal for batch processing workload, media transcoding, machine learning and gaming servers

`Memory Optimized EC2`
- Deliver fast performance form memory-intensive workloads
- Ideal for Databases

`Storage Optimized`
- Optimized for workloads that require high, sequential read & write access to large data sets on local storage
- can deliver tens of thouands of low-latency, random I/O operations per second (IOPS)

`Accelarated Computing`
- Utlize Hardware acceleratos to perform expensive calculations
- Great for Graphic processing and Data Pattern Matching



## EC2 Pricing Options

`On-Demand Pricing`
- Pay for compute capacity per hour which the `EC2` is running 
- It only billed when Instance is running. However, We will still be charged for storage attached to instance
- No upfront Payment
- Great for short-term, Irregular or Unpredictable workloads
- Customer `EC2 Instance` runs on a shared hosts


`Spot Pricing`
- Amazon offers spare Compute Capacity at discounted rates
- Spot Instances  are recommended for 
  - Application that have flexible start time and end time
  - Application that need low compute prices
  - Not suited for workload that cant tolerate interruptions

`Reserve Pricing`
- This allows us to save EC2 costs
- offers discounted rates when reserved for a certain period (1 or 3 years contract)