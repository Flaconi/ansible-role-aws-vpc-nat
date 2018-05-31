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

#### With sane defaults
When using the sane defaults, the only thing to configure for each nat gateway is:

* the subnet_filter (tags) to find the subnet-id

```yml
aws_vpc_nat_gateway:
  - subnet_filter:
      - key: "tag:Name"
        val: "sn-1"
  - subnet_filter:
      - key: "tag:Name"
        val: "sn-2"
  - subnet_filter:
      - key: "tag:Name"
        val: "sn-3"
```

#### All available parameter
Instead of using somebody's sane defaults, you can also add tags for each nat gateway.

```yml
aws_vpc_nat_gateway:
  - subnet_filter:
      - key: "tag:Name"
        val: "sn-1"
    tags:
        - key: Name
          val: nat1
        - key: env
          val: production
    region: eu-central-1
  - subnet_filter:
      - key: "tag:Name"
        val: "sn-2"
    tags:
        - key: Name
          val: nat2
  - subnet_filter:
      - key: "tag:Name"
        val: "sn-3"
```
