## Terraform Assignment

### Given below are some steps 

#### Step 1: Define the VPC

This step creates a custom VPC using the aws_vpc resource. The VPC is given a CIDR block of 10.0.0.0/16, which allows for a range of IP addresses within the VPC. The tags block is used to assign a name tag to the VPC for identification.

<img width="867" alt="Screenshot 2023-06-05 at 11 58 03 AM" src="https://github.com/srinivasteja150/terraform_assignment/assets/122455311/c1902515-1c56-47b4-853d-687c9182f74e">


#### Step 2: Define the public subnet

- In this step, the aws_subnet resource is used to create a public subnet within the VPC. It is associated with the VPC using the vpc_id parameter. 
- The subnet is given a CIDR block of 10.0.1.0/24, which allows for a range of IP addresses within the subnet. The subnet is placed in the us-east-1a availability zone. 
- The map_public_ip_on_launch parameter is set to true, indicating that instances launched in this subnet should be assigned a public IP address automatically. 

#### Step 3: Define the private subnet

- Similar to the previous step, this step creates a private subnet within the VPC using the aws_subnet resource. The subnet is associated with the VPC using the vpc_id parameter. 
- It is given a CIDR block of 10.0.2.0/24 and placed in the us-east-1b availability zone. Instances launched in this subnet will not be assigned a public IP address.

<img width="1003" alt="Screenshot 2023-06-05 at 11 57 28 AM" src="https://github.com/srinivasteja150/terraform_assignment/assets/122455311/3148a0e3-034d-4ef0-9bbb-a36fe8bcc0e4">


#### Step 4: Generate and Create SSH key pair

- This step generates an RSA SSH key pair using the tls_private_key resource. The key pair will be used for SSH access to the EC2 instances.
- In this step, an AWS key pair is created using the aws_key_pair resource. The key_name parameter specifies the name of the key pair, which is set to "ssh-key". 
- The public key generated in the previous step (tls_private_key.ssh_key.public_key_openssh) is assigned to the public_key parameter. This key pair will be associated with the instances for SSH access.

<img width="709" alt="Screenshot 2023-06-05 at 11 58 15 AM" src="https://github.com/srinivasteja150/terraform_assignment/assets/122455311/315728e9-080e-4eb4-bdcd-baf781413dbf">


<img width="680" alt="Screenshot 2023-06-05 at 11 56 59 AM" src="https://github.com/srinivasteja150/terraform_assignment/assets/122455311/79d78673-f6aa-4e84-a35a-29283b0f2de1">


#### Step 6: Create the public EC2 instance

- This step creates an EC2 instance in the public subnet using the aws_instance resource. The ami parameter specifies the Amazon Machine Image (AMI) ID of the instance. 
- The instance_type parameter determines the instance size, set to "t2.micro" in this case. The key_name parameter specifies the key pair to associate with the instance for SSH access. 
- The subnet_id parameter references the ID of the public subnet created earlier (aws_subnet.public_subnet.id). 
- The provisioner block defines a remote-exec provisioner, which runs a set of inline commands on the instance after it is launched. In this case, it updates the package repository, installs Nginx, and starts the Nginx service on the instance.

<img width="1018" alt="Screenshot 2023-06-05 at 11 56 30 AM" src="https://github.com/srinivasteja150/terraform_assignment/assets/122455311/fa59c5ba-e1dc-4f8f-b5c3-159c43e4abf0">


#### Step 7: Create the private EC2 instance

- Similar to the previous step, this step creates an EC2 instance in the private subnet. It uses the specified AMI, instance type, SSH key pair, and subnet ID. 
- The provisioner block runs inline commands to update packages, install Nginx, and start the Nginx service on the instance. 

<img width="1015" alt="Screenshot 2023-06-05 at 11 55 30 AM" src="https://github.com/srinivasteja150/terraform_assignment/assets/122455311/307cac75-9934-4db6-80d4-5d4006ab7199">


#### These steps, when executed with Terraform, create a custom VPC, subnets, SSH key pair, and EC2 instances in AWS. The provisioner blocks install and start Nginx on both instances.

