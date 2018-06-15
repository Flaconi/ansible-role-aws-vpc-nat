# Ansible role: AWS VPC NAT

This role is able to create any number of NAT gateways per VPC and per subnet.

[![Build Status](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-nat.svg?branch=master)](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-nat)
[![Version](https://img.shields.io/github/tag/Flaconi/ansible-role-aws-vpc-nat.svg)](https://github.com/Flaconi/ansible-role-aws-vpc-nat/tags)
[![Ansible Galaxy](https://img.shields.io/ansible/role/d/26013.svg)](https://galaxy.ansible.com/Flaconi/aws-vpc-nat/)

## Requirements

* Ansible 2.5

## Additional variables

Additional variables that can be used (either as `host_vars`/`group_vars` or via command line args):

| Variable                               | Description                  |
|----------------------------------------|------------------------------|
| `aws_vpc_nat_profile`                  | Boto profile name to be used |
| `aws_vpc_nat_default_region`           | Default region to use        |
| `aws_vpc_nat_eip_filter_additional`    | Additional `key` `val` filter to add to `eip_filter` and `eip_name` by default |
| `aws_vpc_nat_subnet_filter_additional` | Additional `key` `val` filter to add to `subnet_filter` and `subnet_name` by default |


## Example definition

#### With sane defaults
When using the sane defaults, the only thing to configure for each nat gateway is:

* either the `subnet_filter` to find one unique subnet by filter (tags, ids, etc)
* or the `subnet_name` to find one unique subnet by name

```yml
aws_vpc_nat_gateway:
  # Add Nat GW to a subnet found by filter and create EIP automatically
  - subnet_filter:
      - key: "tag:Name"
        val: "sn-1"
  # Add Nat GW to a subnet found by name and create EIP automatically
  - subnet_name: sn-2
```

#### All available parameter
Instead of using somebody's sane defaults, you can also add tags for each nat gateway.

```yml
# Ensure EIP filter (name or filter) and subnet filter (name or filter)
# includes that their state is already created. (not pending nor deleted)
aws_vpc_nat_eip_filter_additional:
  - key: state
    val: available

aws_vpc_nat_subnet_filter_additional:
  - key: state
    val: available

aws_vpc_nat_gateway:
  # Add Nat GW to a subnet found by filter
  - subnet_filter:
      - key: "tag:Name"
        val: "sn-1"
    # re-use existing EIP found by filter
    eip_flter:
      - key: "tag:Name"
        val: "eip-1"
    tags:
      - key: Name
        val: nat1
      - key: env
        val: production
    region: eu-central-1

  # Add Nat GW to a subnet found by name
  - subnet_name: sn-2
    # re-use existing EIP found by name
    eip_name: eip-2
    tags:
      - key: Name
        val: nat2
```


## Testing

#### Requirements

* Docker
* [yamllint](https://github.com/adrienverge/yamllint)

#### Run tests

```bash
# Lint the source files
make lint

# Run integration tests with default Ansible version
make test

# Run integration tests with custom Ansible version
make test ANSIBLE_VERSION=2.4
```
