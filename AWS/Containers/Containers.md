
## Tpyes of Container Orchestration in AWS

## Elastic Container Service (ECS)

`ECS`: This is a fully mananged container orchestration service that helps manage, and scale containerized applications
- Its Managed by AWS
- Containers runs on EC2 Instance or Fargate


## Elastic Kubernetes Service (EKS)

- AWS EKS is a Managed K8s Service i.e EKS manages the` control-plane` for us
- We as a User are still resposing for managing the `Worker Nodes`
- If we make use of `Fargate` instead of `EC2` AWS will manage the `worker nodes `


## Benefit of EKS
- Runs and Scale Control-plane accross multiple AZ
- Scale Control-plane instancea based on load
- Can integrate with other AWS services
  - `IAM` for Authentication
  - Elastic Load Balancer
  - ECR for Container Image


## Difference Btw ECS & EKS

- `ECS` is proprietary to AWS so Migration to another cloud Provider can be diffifcult
- `EKS` is Kubernetes which is open source and can be run on any plaform
  - **Note**: The more AWS Services we configure our cluster to interact with the harder it will be to move to another provider
  - `ECS` has a simplier Architecture
    - simpler API
    - Easier to ramp up new team members
- `EKS` is very complex and has a steep learning curve but has a larger communinity
- `ECS` doesnt charge for control plane. only pay for infrastucture running applications (EC2/Fargate,EBS)
- 