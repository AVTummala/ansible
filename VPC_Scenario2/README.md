# VPC_Scenario2

The architecture created is

- A VPC with a public and private subnets
- An Internet Gateway
- A NAT Gateway for allowing Internet access from private subnets
- Routing tables for both public and private subnet
- Two  VPC security groups for public or private instance
- N number of ec2-instances which start hello-world docker conatiner upon launch


Installations Required
--------------

- Install Ansible
- Clone this repo , copy vpc-scenario2 and configure-docker roles under <ansible_home>/roles folder. Place the configure_vpc.yml playbook under your playbooks folder
- Install boto, boto3, botocore, docker and docker-py using pip
- AWS account and credentials ( set them in .aws/credentials file under your home directory)
~~~
  [default]
  aws_access_key_id = <your_access_id>
  aws_secret_access_key = <your_secret_access_key>
~~~
- Create a key using ssh-keygen and add the path to the public key in <ansible_home>/roles/vpc-scenario2/vars/main.yml
~~~
  key_file_path: "<path_to_public_key>"
~~~
- Add the following parameters to your ansible.cfg file under [defaults] section
~~~
  inventory      = /etc/ansible/hosts
  ansible_python_interpreter = python
  roles_path    = /etc/ansible/roles
  host_key_checking = False
  private_key_file = <path_to_private_key_file>
~~~
User Specific Variables
--------------

Modify vars/main.yml under vpc-scenario2 role to your specific needs(cidr blocks, ami, user, names). Otherwise, the architecture and instances(ubuntu) will be created with the default values.


Executing the Playbook
----------------

Go to the path where the playbook is saved
Run the following command (<no_of_instances> is the number of ec2 instaces you want to create)
~~~
sudo ansible-playbook configure_vpc.yml --extra-vars "instance_number=<no_of_instances>"
~~~
