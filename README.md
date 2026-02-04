# Azure Networking & Secure Storage Lab (AZ-104)

## Overview
This project demonstrates how to design a secure Azure network, isolate workloads using subnets and NSGs, deploy a private Azure Storage Account with encryption and Private Endpoints, and automate deployments using ARM templates. The goal is to mirror real-world networking and storage governance practices aligned with AZ-104.

## Architecture
- Virtual Network with two subnets (Web, Database)
- Network Security Group attached to Web subnet
- Azure Storage Account (private access only)
- Private Endpoint in Database subnet
- Microsoft-managed encryption
- ARM Templates (exported and redeployed)
- Secure access via SAS (Storage Explorer / AzCopy)

## Implementation

### 1. Cost Guardrails
A subscription budget was used to ensure this lab stayed within safe spend limits.



---

### 2. Virtual Network & Subnets
Created a VNet with two subnets:
- `subnet-web` – for web tier
- `subnet-database` – for private backend access  
Service Endpoints were enabled for Microsoft.Storage on the database subnet.



---

### 3. Network Security Group (NSG)
An NSG was associated with the Web subnet to restrict inbound traffic:
- Allow HTTPS (443) from the internet  
- Optional: Allow SSH (22) from my IP  
- All other inbound traffic is denied by default



---

### 4. Secure Storage Account (Private Endpoint)
A Storage Account was deployed with:
- Public network access **disabled**
- Private Endpoint enabled to the database subnet
This ensures the storage account is not accessible from the public internet.



---

### 5. Encryption
Storage encryption at rest was enabled using Microsoft-managed keys (default).



---

### 6. ARM Templates (Export & Deploy)
The VNet and Storage Account were exported as ARM templates and deployed using Template Specs to demonstrate Infrastructure as Code awareness and repeatable deployments.



---

### 7. Secure Access with SAS
A Shared Access Signature (SAS) token was generated to provide time-limited access to Blob Storage. Access was tested using Azure Storage Explorer and AzCopy.


---

## Lessons Learned
- How VNets and subnets provide network isolation  
- How NSGs enforce zero-trust inbound access  
- How Private Endpoints remove public exposure of storage  
- How Azure encrypts data at rest by default  
- How ARM templates enable repeatable deployments  
- How SAS provides scoped, time-bound access to storage  

## Cleanup
All resources were deleted at the end of the lab to avoid ongoing costs.

