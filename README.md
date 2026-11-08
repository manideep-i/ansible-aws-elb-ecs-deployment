# Ansible AWS Load Balancer & ECS Deployment

![Ansible](https://img.shields.io/badge/Ansible-E00000?style=for-the-badge&logo=ansible&logoColor=white)
![AWS](https://img.shields.io/badge/Amazon_AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

Automated Ansible playbooks and roles for provisioning AWS Elastic Load Balancers (ELB) integrated with Virtual Private Clouds (VPC), Security Groups, and Elastic Container Service (ECS) Auto Scaling clusters.

---

## 🎯 Project Overview

This repository focuses on automated deployment of cloud infrastructure with an emphasis on **Elastic Load Balancing (ELB)** in internal/external deployment modes, seamlessly connected with Amazon ECS cluster compute nodes.

---

## 📂 Repository Structure

```
.
└── test-elb/                    # ELB & ECS provisioning root
    ├── ecs.yml                  # Infrastructure deployment playbook
    ├── group_vars/              # Centralized variable definitions
    │   └── all/
    │       ├── application.yml
    │       └── aws/             # Service-specific configuration files (ec2, ecs, elb, vpc, tags, region)
    ├── roles/                   # Infrastructure automation roles
    │   ├── aws-elb/             # Provisions Classic Load Balancer with custom health checks and schemes
    │   ├── aws-vpc/             # Network provisioning (VPC, CIDRs, Subnets)
    │   ├── aws-security-groups/ # Security Group rules for Load Balancers & EC2
    │   └── aws-ecs-autoscale/   # ECS Cluster & Auto Scaling Launch Configuration
    ├── aws-env.json             # Environment profile configuration
    └── dependency.py            # Boto library dependency helper
```

---

## 🔧 Ansible Roles Breakdown

| Role | Purpose | Key Responsibilities |
| :--- | :--- | :--- |
| **`aws-vpc`** | Networking | Creates custom AWS VPC, CIDR blocks, subnets across AZs, and routing rules. |
| **`aws-security-groups`** | Security | Configures stateful ingress/egress firewall rules for web traffic and internal communication. |
| **`aws-elb`** | Load Balancing | Provisions AWS Elastic Load Balancer (ELB) attached to VPC subnets and security groups. |
| **`aws-ecs-autoscale`** | Container Compute | Provisions ECS cluster, Launch Configurations, and Auto Scaling Groups for dynamic scaling. |

---

## 🛠️ Usage Instructions

### Prerequisites

- **Ansible** 2.9+
- **Python** with `boto` / `boto3` installed:
  ```bash
  pip install boto boto3
  ```
- Active AWS credentials configured (`AWS_ACCESS_KEY_ID` & `AWS_SECRET_ACCESS_KEY`).

### Execution

Run the deployment playbook from the project directory:

```bash
cd test-elb
ansible-playbook ecs.yml
```

---

## 📄 License

This repository is available under the [MIT License](LICENSE).
