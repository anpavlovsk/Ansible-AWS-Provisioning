# Ansible-AWS-Provisioning
### Build a web server infrastructure and application
![alt text](https://github.com/anpavlovsk/Ansible-AWS-Provisioning/blob/main/screenshots/web-infra.png?raw=true)


Demo of full-stack infrastructure deployment including:

* Security groups
* ELB target groups
* Application load balancer
* Dedicated key pair
* 2x EC2 instance
* Configured web server with default website content

### Execute the Ansible playbook
Enter the following to tell Ansible to create all the resources and show the ELB's URL to access the website:
````
ansible-playbooks aws-infra-provisioning.yaml
````
<details>
<summary>Output</summary>
<pre>$ 

PLAY [Provision AWS Infrastructure] ************************************************************************************************************************************************************************

TASK [Fetch VPC ID] ****************************************************************************************************************************************************************************************

TASK [aws-get-vpc-details : Get VPC Details] ***************************************************************************************************************************************************************
ok: [localhost]

TASK [aws-get-vpc-details : Collect VPC ID] ****************************************************************************************************************************************************************
ok: [localhost]

TASK [aws-get-vpc-details : Fetch VPC Subnets] *************************************************************************************************************************************************************
ok: [localhost]

TASK [aws-get-vpc-details : Collect VPC Subnets] ***********************************************************************************************************************************************************
ok: [localhost] => (item={'availability_zone': 'ap-southeast-1a', 'availability_zone_id': 'apse1-az2', 'available_ip_address_count': 4089, 'cidr_block': '172.31.32.0/20', 'default_for_az': True, 'map_public_ip_on_launch': True, 'map_customer_owned_ip_on_launch': False, 'state': 'available', 'subnet_id': 'subnet-0177f75a16971ab08', 'vpc_id': 'vpc-0b67847579bbf7187', 'owner_id': '647065240363', 'assign_ipv6_address_on_creation': False, 'ipv6_cidr_block_association_set': [], 'subnet_arn': 'arn:aws:ec2:ap-southeast-1:647065240363:subnet/subnet-0177f75a16971ab08', 'id': 'subnet-0177f75a16971ab08', 'tags': {}})
ok: [localhost] => (item={'availability_zone': 'ap-southeast-1c', 'availability_zone_id': 'apse1-az3', 'available_ip_address_count': 4091, 'cidr_block': '172.31.0.0/20', 'default_for_az': True, 'map_public_ip_on_launch': True, 'map_customer_owned_ip_on_launch': False, 'state': 'available', 'subnet_id': 'subnet-000ec41b3feafb785', 'vpc_id': 'vpc-0b67847579bbf7187', 'owner_id': '647065240363', 'assign_ipv6_address_on_creation': False, 'ipv6_cidr_block_association_set': [], 'subnet_arn': 'arn:aws:ec2:ap-southeast-1:647065240363:subnet/subnet-000ec41b3feafb785', 'id': 'subnet-000ec41b3feafb785', 'tags': {}})
ok: [localhost] => (item={'availability_zone': 'ap-southeast-1b', 'availability_zone_id': 'apse1-az1', 'available_ip_address_count': 4089, 'cidr_block': '172.31.16.0/20', 'default_for_az': True, 'map_public_ip_on_launch': True, 'map_customer_owned_ip_on_launch': False, 'state': 'available', 'subnet_id': 'subnet-0a578af70b41de329', 'vpc_id': 'vpc-0b67847579bbf7187', 'owner_id': '647065240363', 'assign_ipv6_address_on_creation': False, 'ipv6_cidr_block_association_set': [], 'subnet_arn': 'arn:aws:ec2:ap-southeast-1:647065240363:subnet/subnet-0a578af70b41de329', 'id': 'subnet-0a578af70b41de329', 'tags': {}})

TASK [Create Security Group] *******************************************************************************************************************************************************************************

TASK [aws-create-sg : Create Security group] ***************************************************************************************************************************************************************
ok: [localhost]

TASK [Create Keypair] **************************************************************************************************************************************************************************************

TASK [aws-create-keypair : Create key pair] ****************************************************************************************************************************************************************
ok: [localhost]

TASK [Create ELB] ******************************************************************************************************************************************************************************************

TASK [aws-create-elb : Create Amazon ELB] ******************************************************************************************************************************************************************
ok: [localhost]

TASK [aws-create-elb : Print Public DNS] *******************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "ansible-iac-demo-elb-app-lb-1354161592.ap-southeast-1.elb.amazonaws.com"
}

TASK [aws-create-elb : Collect ELB Public DNS] *************************************************************************************************************************************************************
ok: [localhost]

TASK [Create ec2 instances] ********************************************************************************************************************************************************************************

TASK [aws-create-ec2 : Fetch Instances by tag, subnet and type] ********************************************************************************************************************************************
ok: [localhost] => (item={'key': 'aws_web_101', 'value': {'name': 'AWS_WEB_101', 'key_name': 'ansible_iac_demo_key', 'group': 'SG-Ansible-Demo', 'instance_type': 't2.micro'}})
ok: [localhost] => (item={'key': 'aws_web_102', 'value': {'name': 'AWS_WEB_102', 'key_name': 'ansible_iac_demo_key', 'group': 'SG-Ansible-Demo', 'instance_type': 't2.micro'}})

TASK [aws-create-ec2 : Collect ec2 in a list] **************************************************************************************************************************************************************
ok: [localhost] => (item=['AWS_WEB_101'])
ok: [localhost] => (item=['AWS_WEB_102'])

TASK [aws-create-ec2 : debug] ******************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": [
        "AWS_WEB_101",
        "AWS_WEB_102"
    ]
}

TASK [aws-create-ec2 : Launching EC2 instances] ************************************************************************************************************************************************************
skipping: [localhost] => (item={'key': 'aws_web_101', 'value': {'name': 'AWS_WEB_101', 'key_name': 'ansible_iac_demo_key', 'group': 'SG-Ansible-Demo', 'instance_type': 't2.micro'}}) 
skipping: [localhost] => (item={'key': 'aws_web_102', 'value': {'name': 'AWS_WEB_102', 'key_name': 'ansible_iac_demo_key', 'group': 'SG-Ansible-Demo', 'instance_type': 't2.micro'}}) 

TASK [aws-create-ec2 : Collect newly created ec2 in a list] ************************************************************************************************************************************************
skipping: [localhost] => (item={'changed': False, 'skipped': True, 'skip_reason': 'Conditional result was False', 'item': {'key': 'aws_web_101', 'value': {'name': 'AWS_WEB_101', 'key_name': 'ansible_iac_demo_key', 'group': 'SG-Ansible-Demo', 'instance_type': 't2.micro'}}, 'ansible_loop_var': 'item'}) 
skipping: [localhost] => (item={'changed': False, 'skipped': True, 'skip_reason': 'Conditional result was False', 'item': {'key': 'aws_web_102', 'value': {'name': 'AWS_WEB_102', 'key_name': 'ansible_iac_demo_key', 'group': 'SG-Ansible-Demo', 'instance_type': 't2.micro'}}, 'ansible_loop_var': 'item'}) 

TASK [aws-create-ec2 : Status] *****************************************************************************************************************************************************************************

TASK [aws-create-ec2 : Wait for SSH] ***********************************************************************************************************************************************************************

TASK [aws-create-ec2 : Fetch Instances by tag, subnet and type] ********************************************************************************************************************************************
ok: [localhost] => (item={'key': 'aws_web_101', 'value': {'name': 'AWS_WEB_101', 'key_name': 'ansible_iac_demo_key', 'group': 'SG-Ansible-Demo', 'instance_type': 't2.micro'}})
ok: [localhost] => (item={'key': 'aws_web_102', 'value': {'name': 'AWS_WEB_102', 'key_name': 'ansible_iac_demo_key', 'group': 'SG-Ansible-Demo', 'instance_type': 't2.micro'}})

TASK [aws-create-ec2 : Update Amazon ELB and add instance ids] *********************************************************************************************************************************************
ok: [localhost] => (item={'instances': [{'ami_launch_index': 0, 'image_id': 'ami-02f26adf094f51167', 'instance_id': 'i-0400a0652832893dc', 'instance_type': 't2.micro', 'key_name': 'ansible_iac_demo_key', 'launch_time': '2022-08-10T18:09:17+00:00', 'monitoring': {'state': 'disabled'}, 'placement': {'availability_zone': 'ap-southeast-1a', 'group_name': '', 'tenancy': 'default'}, 'private_dns_name': 'ip-172-31-33-221.ap-southeast-1.compute.internal', 'private_ip_address': '172.31.33.221', 'product_codes': [], 'public_dns_name': 'ec2-52-77-215-237.ap-southeast-1.compute.amazonaws.com', 'public_ip_address': '52.77.215.237', 'state': {'code': 16, 'name': 'running'}, 'state_transition_reason': '', 'subnet_id': 'subnet-0177f75a16971ab08', 'vpc_id': 'vpc-0b67847579bbf7187', 'architecture': 'x86_64', 'block_device_mappings': [{'device_name': '/dev/xvda', 'ebs': {'attach_time': '2022-08-10T18:09:18+00:00', 'delete_on_termination': True, 'status': 'attached', 'volume_id': 'vol-0bc8a14479f734bb6'}}], 'client_token': '8450d373e4ce46eb9a8e8c5f29bec439', 'ebs_optimized': False, 'ena_support': True, 'hypervisor': 'xen', 'network_interfaces': [{'association': {'ip_owner_id': 'amazon', 'public_dns_name': 'ec2-52-77-215-237.ap-southeast-1.compute.amazonaws.com', 'public_ip': '52.77.215.237'}, 'attachment': {'attach_time': '2022-08-10T18:09:17+00:00', 'attachment_id': 'eni-attach-00d28ec5765be2969', 'delete_on_termination': True, 'device_index': 0, 'status': 'attached', 'network_card_index': 0}, 'description': '', 'groups': [{'group_name': 'ansible_iac_demo_sg', 'group_id': 'sg-0b31c3f5a7b9db9d5'}], 'ipv6_addresses': [], 'mac_address': '06:2d:a5:34:a1:60', 'network_interface_id': 'eni-0557406f0281642e3', 'owner_id': '647065240363', 'private_dns_name': 'ip-172-31-33-221.ap-southeast-1.compute.internal', 'private_ip_address': '172.31.33.221', 'private_ip_addresses': [{'association': {'ip_owner_id': 'amazon', 'public_dns_name': 'ec2-52-77-215-237.ap-southeast-1.compute.amazonaws.com', 'public_ip': '52.77.215.237'}, 'primary': True, 'private_dns_name': 'ip-172-31-33-221.ap-southeast-1.compute.internal', 'private_ip_address': '172.31.33.221'}], 'source_dest_check': True, 'status': 'in-use', 'subnet_id': 'subnet-0177f75a16971ab08', 'vpc_id': 'vpc-0b67847579bbf7187', 'interface_type': 'interface'}], 'root_device_name': '/dev/xvda', 'root_device_type': 'ebs', 'security_groups': [{'group_name': 'ansible_iac_demo_sg', 'group_id': 'sg-0b31c3f5a7b9db9d5'}], 'source_dest_check': True, 'tags': {'Name': 'AWS_WEB_101'}, 'virtualization_type': 'hvm', 'cpu_options': {'core_count': 1, 'threads_per_core': 1}, 'capacity_reservation_specification': {'capacity_reservation_preference': 'open'}, 'hibernation_options': {'configured': False}, 'metadata_options': {'state': 'applied', 'http_tokens': 'optional', 'http_put_response_hop_limit': 1, 'http_endpoint': 'enabled'}, 'enclave_options': {'enabled': False}}], 'invocation': {'module_args': {'aws_access_key': 'AKIAZNKAYAMVREFS7CUB', 'aws_secret_key': 'VALUE_SPECIFIED_IN_NO_LOG_PARAMETER', 'region': 'ap-southeast-1', 'filters': {'tag:Name': 'AWS_WEB_101', 'instance-type': 't2.micro', 'instance-state-name': ['running', 'stopped', 'stopping', 'starting', 'pending']}, 'debug_botocore_endpoint_logs': False, 'validate_certs': True, 'instance_ids': [], 'ec2_url': None, 'security_token': None, 'aws_ca_bundle': None, 'profile': None, 'aws_config': None}}, 'failed': False, 'changed': False, 'item': {'key': 'aws_web_101', 'value': {'name': 'AWS_WEB_101', 'key_name': 'ansible_iac_demo_key', 'group': 'SG-Ansible-Demo', 'instance_type': 't2.micro'}}, 'ansible_loop_var': 'item'})
ok: [localhost] => (item={'instances': [{'ami_launch_index': 0, 'image_id': 'ami-02f26adf094f51167', 'instance_id': 'i-0af69193cf82fb0aa', 'instance_type': 't2.micro', 'key_name': 'ansible_iac_demo_key', 'launch_time': '2022-08-10T18:12:29+00:00', 'monitoring': {'state': 'disabled'}, 'placement': {'availability_zone': 'ap-southeast-1b', 'group_name': '', 'tenancy': 'default'}, 'private_dns_name': 'ip-172-31-21-220.ap-southeast-1.compute.internal', 'private_ip_address': '172.31.21.220', 'product_codes': [], 'public_dns_name': 'ec2-18-136-207-125.ap-southeast-1.compute.amazonaws.com', 'public_ip_address': '18.136.207.125', 'state': {'code': 16, 'name': 'running'}, 'state_transition_reason': '', 'subnet_id': 'subnet-0a578af70b41de329', 'vpc_id': 'vpc-0b67847579bbf7187', 'architecture': 'x86_64', 'block_device_mappings': [{'device_name': '/dev/xvda', 'ebs': {'attach_time': '2022-08-10T18:12:30+00:00', 'delete_on_termination': True, 'status': 'attached', 'volume_id': 'vol-0c1630db9d2501745'}}], 'client_token': 'a28f7b8d8ea04226b96c3a26ce5f5f8c', 'ebs_optimized': False, 'ena_support': True, 'hypervisor': 'xen', 'network_interfaces': [{'association': {'ip_owner_id': 'amazon', 'public_dns_name': 'ec2-18-136-207-125.ap-southeast-1.compute.amazonaws.com', 'public_ip': '18.136.207.125'}, 'attachment': {'attach_time': '2022-08-10T18:12:29+00:00', 'attachment_id': 'eni-attach-08e84843c98e2cac8', 'delete_on_termination': True, 'device_index': 0, 'status': 'attached', 'network_card_index': 0}, 'description': '', 'groups': [{'group_name': 'ansible_iac_demo_sg', 'group_id': 'sg-0b31c3f5a7b9db9d5'}], 'ipv6_addresses': [], 'mac_address': '02:bd:18:32:a8:94', 'network_interface_id': 'eni-07e657c07c5b1afd0', 'owner_id': '647065240363', 'private_dns_name': 'ip-172-31-21-220.ap-southeast-1.compute.internal', 'private_ip_address': '172.31.21.220', 'private_ip_addresses': [{'association': {'ip_owner_id': 'amazon', 'public_dns_name': 'ec2-18-136-207-125.ap-southeast-1.compute.amazonaws.com', 'public_ip': '18.136.207.125'}, 'primary': True, 'private_dns_name': 'ip-172-31-21-220.ap-southeast-1.compute.internal', 'private_ip_address': '172.31.21.220'}], 'source_dest_check': True, 'status': 'in-use', 'subnet_id': 'subnet-0a578af70b41de329', 'vpc_id': 'vpc-0b67847579bbf7187', 'interface_type': 'interface'}], 'root_device_name': '/dev/xvda', 'root_device_type': 'ebs', 'security_groups': [{'group_name': 'ansible_iac_demo_sg', 'group_id': 'sg-0b31c3f5a7b9db9d5'}], 'source_dest_check': True, 'tags': {'Name': 'AWS_WEB_102'}, 'virtualization_type': 'hvm', 'cpu_options': {'core_count': 1, 'threads_per_core': 1}, 'capacity_reservation_specification': {'capacity_reservation_preference': 'open'}, 'hibernation_options': {'configured': False}, 'metadata_options': {'state': 'applied', 'http_tokens': 'optional', 'http_put_response_hop_limit': 1, 'http_endpoint': 'enabled'}, 'enclave_options': {'enabled': False}}], 'invocation': {'module_args': {'aws_access_key': 'AKIAZNKAYAMVREFS7CUB', 'aws_secret_key': 'VALUE_SPECIFIED_IN_NO_LOG_PARAMETER', 'region': 'ap-southeast-1', 'filters': {'tag:Name': 'AWS_WEB_102', 'instance-type': 't2.micro', 'instance-state-name': ['running', 'stopped', 'stopping', 'starting', 'pending']}, 'debug_botocore_endpoint_logs': False, 'validate_certs': True, 'instance_ids': [], 'ec2_url': None, 'security_token': None, 'aws_ca_bundle': None, 'profile': None, 'aws_config': None}}, 'failed': False, 'changed': False, 'item': {'key': 'aws_web_102', 'value': {'name': 'AWS_WEB_102', 'key_name': 'ansible_iac_demo_key', 'group': 'SG-Ansible-Demo', 'instance_type': 't2.micro'}}, 'ansible_loop_var': 'item'})

TASK [aws-create-ec2 : Collect ec2 Public IP in a list] ****************************************************************************************************************************************************
ok: [localhost] => (item={'instances': [{'ami_launch_index': 0, 'image_id': 'ami-02f26adf094f51167', 'instance_id': 'i-0400a0652832893dc', 'instance_type': 't2.micro', 'key_name': 'ansible_iac_demo_key', 'launch_time': '2022-08-10T18:09:17+00:00', 'monitoring': {'state': 'disabled'}, 'placement': {'availability_zone': 'ap-southeast-1a', 'group_name': '', 'tenancy': 'default'}, 'private_dns_name': 'ip-172-31-33-221.ap-southeast-1.compute.internal', 'private_ip_address': '172.31.33.221', 'product_codes': [], 'public_dns_name': 'ec2-52-77-215-237.ap-southeast-1.compute.amazonaws.com', 'public_ip_address': '52.77.215.237', 'state': {'code': 16, 'name': 'running'}, 'state_transition_reason': '', 'subnet_id': 'subnet-0177f75a16971ab08', 'vpc_id': 'vpc-0b67847579bbf7187', 'architecture': 'x86_64', 'block_device_mappings': [{'device_name': '/dev/xvda', 'ebs': {'attach_time': '2022-08-10T18:09:18+00:00', 'delete_on_termination': True, 'status': 'attached', 'volume_id': 'vol-0bc8a14479f734bb6'}}], 'client_token': '8450d373e4ce46eb9a8e8c5f29bec439', 'ebs_optimized': False, 'ena_support': True, 'hypervisor': 'xen', 'network_interfaces': [{'association': {'ip_owner_id': 'amazon', 'public_dns_name': 'ec2-52-77-215-237.ap-southeast-1.compute.amazonaws.com', 'public_ip': '52.77.215.237'}, 'attachment': {'attach_time': '2022-08-10T18:09:17+00:00', 'attachment_id': 'eni-attach-00d28ec5765be2969', 'delete_on_termination': True, 'device_index': 0, 'status': 'attached', 'network_card_index': 0}, 'description': '', 'groups': [{'group_name': 'ansible_iac_demo_sg', 'group_id': 'sg-0b31c3f5a7b9db9d5'}], 'ipv6_addresses': [], 'mac_address': '06:2d:a5:34:a1:60', 'network_interface_id': 'eni-0557406f0281642e3', 'owner_id': '647065240363', 'private_dns_name': 'ip-172-31-33-221.ap-southeast-1.compute.internal', 'private_ip_address': '172.31.33.221', 'private_ip_addresses': [{'association': {'ip_owner_id': 'amazon', 'public_dns_name': 'ec2-52-77-215-237.ap-southeast-1.compute.amazonaws.com', 'public_ip': '52.77.215.237'}, 'primary': True, 'private_dns_name': 'ip-172-31-33-221.ap-southeast-1.compute.internal', 'private_ip_address': '172.31.33.221'}], 'source_dest_check': True, 'status': 'in-use', 'subnet_id': 'subnet-0177f75a16971ab08', 'vpc_id': 'vpc-0b67847579bbf7187', 'interface_type': 'interface'}], 'root_device_name': '/dev/xvda', 'root_device_type': 'ebs', 'security_groups': [{'group_name': 'ansible_iac_demo_sg', 'group_id': 'sg-0b31c3f5a7b9db9d5'}], 'source_dest_check': True, 'tags': {'Name': 'AWS_WEB_101'}, 'virtualization_type': 'hvm', 'cpu_options': {'core_count': 1, 'threads_per_core': 1}, 'capacity_reservation_specification': {'capacity_reservation_preference': 'open'}, 'hibernation_options': {'configured': False}, 'metadata_options': {'state': 'applied', 'http_tokens': 'optional', 'http_put_response_hop_limit': 1, 'http_endpoint': 'enabled'}, 'enclave_options': {'enabled': False}}], 'invocation': {'module_args': {'aws_access_key': 'AKIAZNKAYAMVREFS7CUB', 'aws_secret_key': 'VALUE_SPECIFIED_IN_NO_LOG_PARAMETER', 'region': 'ap-southeast-1', 'filters': {'tag:Name': 'AWS_WEB_101', 'instance-type': 't2.micro', 'instance-state-name': ['running', 'stopped', 'stopping', 'starting', 'pending']}, 'debug_botocore_endpoint_logs': False, 'validate_certs': True, 'instance_ids': [], 'ec2_url': None, 'security_token': None, 'aws_ca_bundle': None, 'profile': None, 'aws_config': None}}, 'failed': False, 'changed': False, 'item': {'key': 'aws_web_101', 'value': {'name': 'AWS_WEB_101', 'key_name': 'ansible_iac_demo_key', 'group': 'SG-Ansible-Demo', 'instance_type': 't2.micro'}}, 'ansible_loop_var': 'item'})
ok: [localhost] => (item={'instances': [{'ami_launch_index': 0, 'image_id': 'ami-02f26adf094f51167', 'instance_id': 'i-0af69193cf82fb0aa', 'instance_type': 't2.micro', 'key_name': 'ansible_iac_demo_key', 'launch_time': '2022-08-10T18:12:29+00:00', 'monitoring': {'state': 'disabled'}, 'placement': {'availability_zone': 'ap-southeast-1b', 'group_name': '', 'tenancy': 'default'}, 'private_dns_name': 'ip-172-31-21-220.ap-southeast-1.compute.internal', 'private_ip_address': '172.31.21.220', 'product_codes': [], 'public_dns_name': 'ec2-18-136-207-125.ap-southeast-1.compute.amazonaws.com', 'public_ip_address': '18.136.207.125', 'state': {'code': 16, 'name': 'running'}, 'state_transition_reason': '', 'subnet_id': 'subnet-0a578af70b41de329', 'vpc_id': 'vpc-0b67847579bbf7187', 'architecture': 'x86_64', 'block_device_mappings': [{'device_name': '/dev/xvda', 'ebs': {'attach_time': '2022-08-10T18:12:30+00:00', 'delete_on_termination': True, 'status': 'attached', 'volume_id': 'vol-0c1630db9d2501745'}}], 'client_token': 'a28f7b8d8ea04226b96c3a26ce5f5f8c', 'ebs_optimized': False, 'ena_support': True, 'hypervisor': 'xen', 'network_interfaces': [{'association': {'ip_owner_id': 'amazon', 'public_dns_name': 'ec2-18-136-207-125.ap-southeast-1.compute.amazonaws.com', 'public_ip': '18.136.207.125'}, 'attachment': {'attach_time': '2022-08-10T18:12:29+00:00', 'attachment_id': 'eni-attach-08e84843c98e2cac8', 'delete_on_termination': True, 'device_index': 0, 'status': 'attached', 'network_card_index': 0}, 'description': '', 'groups': [{'group_name': 'ansible_iac_demo_sg', 'group_id': 'sg-0b31c3f5a7b9db9d5'}], 'ipv6_addresses': [], 'mac_address': '02:bd:18:32:a8:94', 'network_interface_id': 'eni-07e657c07c5b1afd0', 'owner_id': '647065240363', 'private_dns_name': 'ip-172-31-21-220.ap-southeast-1.compute.internal', 'private_ip_address': '172.31.21.220', 'private_ip_addresses': [{'association': {'ip_owner_id': 'amazon', 'public_dns_name': 'ec2-18-136-207-125.ap-southeast-1.compute.amazonaws.com', 'public_ip': '18.136.207.125'}, 'primary': True, 'private_dns_name': 'ip-172-31-21-220.ap-southeast-1.compute.internal', 'private_ip_address': '172.31.21.220'}], 'source_dest_check': True, 'status': 'in-use', 'subnet_id': 'subnet-0a578af70b41de329', 'vpc_id': 'vpc-0b67847579bbf7187', 'interface_type': 'interface'}], 'root_device_name': '/dev/xvda', 'root_device_type': 'ebs', 'security_groups': [{'group_name': 'ansible_iac_demo_sg', 'group_id': 'sg-0b31c3f5a7b9db9d5'}], 'source_dest_check': True, 'tags': {'Name': 'AWS_WEB_102'}, 'virtualization_type': 'hvm', 'cpu_options': {'core_count': 1, 'threads_per_core': 1}, 'capacity_reservation_specification': {'capacity_reservation_preference': 'open'}, 'hibernation_options': {'configured': False}, 'metadata_options': {'state': 'applied', 'http_tokens': 'optional', 'http_put_response_hop_limit': 1, 'http_endpoint': 'enabled'}, 'enclave_options': {'enabled': False}}], 'invocation': {'module_args': {'aws_access_key': 'AKIAZNKAYAMVREFS7CUB', 'aws_secret_key': 'VALUE_SPECIFIED_IN_NO_LOG_PARAMETER', 'region': 'ap-southeast-1', 'filters': {'tag:Name': 'AWS_WEB_102', 'instance-type': 't2.micro', 'instance-state-name': ['running', 'stopped', 'stopping', 'starting', 'pending']}, 'debug_botocore_endpoint_logs': False, 'validate_certs': True, 'instance_ids': [], 'ec2_url': None, 'security_token': None, 'aws_ca_bundle': None, 'profile': None, 'aws_config': None}}, 'failed': False, 'changed': False, 'item': {'key': 'aws_web_102', 'value': {'name': 'AWS_WEB_102', 'key_name': 'ansible_iac_demo_key', 'group': 'SG-Ansible-Demo', 'instance_type': 't2.micro'}}, 'ansible_loop_var': 'item'})

TASK [aws-create-ec2 : Add ec2 instances to a host group] **************************************************************************************************************************************************
ok: [localhost] => (item=52.77.215.237)
ok: [localhost] => (item=18.136.207.125)

PLAY [Deploy Webserver to EC2 instances] *******************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************************
[WARNING]: Platform linux on host 18.136.207.125 is using the discovered Python interpreter at /usr/bin/python, but future installation of another Python interpreter could change the meaning of that
path. See https://docs.ansible.com/ansible/2.10/reference_appendices/interpreter_discovery.html for more information.
ok: [18.136.207.125]
[WARNING]: Platform linux on host 52.77.215.237 is using the discovered Python interpreter at /usr/bin/python, but future installation of another Python interpreter could change the meaning of that path.
See https://docs.ansible.com/ansible/2.10/reference_appendices/interpreter_discovery.html for more information.
ok: [52.77.215.237]

TASK [Deploy Web service] **********************************************************************************************************************************************************************************

TASK [deploy-web-server : Delete content & directory] ******************************************************************************************************************************************************
changed: [52.77.215.237]
changed: [18.136.207.125]

TASK [deploy-web-server : Create directory] ****************************************************************************************************************************************************************
changed: [52.77.215.237]
changed: [18.136.207.125]

TASK [deploy-web-server : Install httpd and firewalld] *****************************************************************************************************************************************************
ok: [52.77.215.237]
ok: [18.136.207.125]

TASK [deploy-web-server : Enable and Run Firewalld] ********************************************************************************************************************************************************
ok: [18.136.207.125]
ok: [52.77.215.237]

TASK [deploy-web-server : firewalld permitt httpd service] *************************************************************************************************************************************************
ok: [18.136.207.125]
ok: [52.77.215.237]

TASK [deploy-web-server : httpd enabled and running] *******************************************************************************************************************************************************
ok: [18.136.207.125]
ok: [52.77.215.237]

TASK [deploy-web-server : Git checkout] ********************************************************************************************************************************************************************
changed: [52.77.215.237]
changed: [18.136.207.125]

TASK [deploy-web-server : Set Hostname on Site] ************************************************************************************************************************************************************
changed: [18.136.207.125]
changed: [52.77.215.237]

PLAY [IaC Summary] *****************************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************************
ok: [localhost]

TASK [debug] ***********************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Website is accessible on Appication ELB: ansible-iac-demo-elb-app-lb-1354161592.ap-southeast-1.elb.amazonaws.com (It may take some time to get the backend instance to come InService)"
}

PLAY RECAP *************************************************************************************************************************************************************************************************
18.136.207.125             : ok=9    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
52.77.215.237              : ok=9    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
localhost                  : ok=18   changed=0    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0   
</pre>
</details>


![alt text](https://github.com/anpavlovsk/Ansible-AWS-Provisioning/blob/main/screenshots/resources.png?raw=true)
![alt text](https://github.com/anpavlovsk/Ansible-AWS-Provisioning/blob/main/screenshots/instances.png?raw=true)
![alt text](https://github.com/anpavlovsk/Ansible-AWS-Provisioning/blob/main/screenshots/secgroups.png?raw=true)
![alt text](https://github.com/anpavlovsk/Ansible-AWS-Provisioning/blob/main/screenshots/lb.png?raw=true)
![alt text](https://github.com/anpavlovsk/Ansible-AWS-Provisioning/blob/main/screenshots/aws_web_101.png?raw=true)
![alt text](https://github.com/anpavlovsk/Ansible-AWS-Provisioning/blob/main/screenshots/aws_web_102.png?raw=true)
