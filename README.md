# Terraform-Ansible dynamic inventory for IBM Cloud

Sample Python script to dynamically parse terraform.tfstate file into Ansible inventory

Copyright (c) 2018, IBM UK
steve_strutt@uk.ibm.com
ti_version = '0.3'

## Static and dynamic inventory
Can be used alongside static inventory files in the same directory 


## Terraform dependencies

This inventory script expects to find Terraform tags of the form 
group: host_group associated with each tf instance to define the 
host group membership for Ansible. Multiple group tags are allowed per host

## Configuration

To avoid co-mingling the Ansible and Terraform definitions in the same directory, 
the terraform.tfstate defining the current state of the deployed infrastructure,
can be read from the Terraform direcfory. This is specified using the  
terraform_inv.ini file in the same directory as this script, pointing to the 
location of the terraform.tfstate file to be inventoried

[TFSTATE]
TFSTATE_FILE = ~/terraform/ibm/Demoapp2x/terraform.tfstate
#TFSTATE_FILE = Users/JohnDoe/terraform/ibm/Demoapp2x/terraform.tfstate
#TFSTATE_FILE = /usr/share/terraform/ibm/Demoapp2x/terraform.tfstate
 
## Testing  
 
Validate correct execution: 
  With supplied test files - './terraform_inv.py -t test_files/terraformx.tfstate'
  With ini file './terraform.py -i . --list'
Successful execution returns groups with lists of hosts and _meta/hostvars with a detailed
host listing.
Validate successful operation with ansible:
  With - 'ansible-inventory -i . --list'

  