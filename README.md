# Ansible role: AWS VPC NAT

This role is able to create any number of NAT gateways per VPC and per subnet.

[![Build Status](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-nat.svg?branch=master)](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-nat)
[![Version](https://img.shields.io/github/tag/Flaconi/ansible-role-aws-vpc-nat.svg)](https://github.com/Flaconi/ansible-role-aws-vpc-nat/tags)
<!-- [![Ansible Galaxy](https://img.shields.io/ansible/role/d/25920.svg)](https://galaxy.ansible.com/Flaconi/aws-vpc-nat/) -->

## Requirements

* Ansible 2.5


## Additional variables

Additional variables that can be used (either as `host_vars`/`group_vars` or via command line args):

| Variable                     | Description                  |
|------------------------------|------------------------------|
| `aws_vpc_nat_profile`        | Boto profile name to be used |
| `aws_vpc_nat_default_region` | Default region to use        |


## Example definition

NAT gateways can be created per VPC either by supplying a VPC `name` or a VPC `filter`.

#### Required parameter only

```yml
aws_vpc_nats: []
```

#### All available parameter
```yml
aws_vpc_nats: []
```
