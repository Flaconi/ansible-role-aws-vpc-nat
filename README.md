# Nat Gateways

Create one or more nat gateways

## Requirements

* Ansible 2.5

## Example definition

#### With sane defaults
When using the sane defaults, the only thing to configure for each nat gateway is:

* the subnet_filter (tags) find the subnet-id

```yml
aws_nat_gateway:
  - subnet_filter:
      - key: "tag:Name"
        val: "sn-1"
  - subnet_filter:
      - key: "tag:Name"
        val: "sn-2"
  -  subnet_filter:
      - key: "tag:Name"
        val: "sn-3"
```

#### Customized array
Instead of using somebody's sane defaults, you can also add tags for each nat gateway.

```yml
aws_nat_gateway:
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
  -  subnet_filter:
      - key: "tag:Name"
        val: "sn-3"
```
