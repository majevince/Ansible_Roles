# Ansible Roles  
*A curated collection of reusable Ansible roles for infrastructure automation*

---

## Table of Contents  
1. [Project Overview](#project-overview)  
2. [Purpose & Scope](#purpose-and-scope)  
3. [Features & Content](#features-and-content)  
4. [Repository Structure](#repository-structure)  
5. [Getting Started](#getting-started)  
   1. [Prerequisites](#prerequisites)  
   2. [Installation / Setup](#installation-setup)  
   3. [Usage Examples](#usage-examples)  
6. [Customisation & Extending](#customisation-and-extending)  
7. [Best Practices and Operational Tips](#best-practices-and-operational-tips)  
8. [CI / Quality Assurance](#ci-quality-assurance)  
9. [Security Considerations](#security-considerations)  
10. [Contributing](#contributing)  
11. [License](#license)  
12. [Support & Contact](#support-and-contact)  

---

## Project Overview  
This repository contains a set of well-structured Ansible roles designed to simplify and standardise infrastructure configuration across various systems and services.  
Each role is modular and reusable, aiming to encapsulate a distinct service or configuration domain (e.g., networking, system hardening, application deployment) so that you can assemble playbooks by assembling roles like Lego blocks.

The idea is to promote:  
- **Consistency**: using the same code path for similar tasks across hosts/environments.  
- **Reusability**: roles are written once and can be applied many times.  
- **Maintainability**: using roles enforces separation of concerns, making updates easier.  
- **Scalability**: as environments grow in complexity, roles help you keep your automation maintainable.

---

## Purpose and Scope  
### Purpose  
- Provide a library of roles compatible with your existing automation workflows.  
- Offer a baseline of tested configurations for common infrastructure patterns.  
- Reduce the time needed to onboard new services or enforce baseline security/hardening.

### Scope  
- The roles address typical infrastructure components: OS configuration, services, monitoring, network settings, etc.  
- They are designed to be generic enough for reuse across multiple operating systems or environments (subject to support).  
- They may not cover every niche or vendor-specific scenario—if you need something custom, extend or add your own roles.

---

## Features & Content  
Within this collection you’ll find:  
- Roles for common system & service configuration (e.g., `common`, `hardening`, `nginx`, `firewall`)  
- Well-defined defaults and variable structures so you can override behaviour per environment  
- Templates and files built in for configuration management (via Jinja2, etc)  
- Handlers for service restarts and changes triggered by configuration drift  
- Meta information for dependencies between roles (so ordering and prerequisites are handled)  
- Documentation for usage and variables (in the role’s `README.md` or role directory)  

---

## Repository Structure  
Here’s a high-level view of how the repository is laid out (adjust names to reflect your actual folders):
├── ansible.cfg # Ansible configuration file
├── inventory/ # Inventory definitions (by environment)
│ ├── production.yml
│ └── staging.yml
├── playbooks/ # Example playbooks that make use of the roles
│ ├── site.yml
│ ├── webservers.yml
│ └── databases.yml
├── roles/ # Collection of reusable Ansible roles
│ ├── common/ # OS & baseline tasks
│ │ ├── tasks/…
│ │ ├── defaults/…
│ │ ├── handlers/…
│ │ └── meta/…
│ ├── hardening/ # Security‐hardening tasks
│ ├── nginx/ # Web server deployment/config
│ ├── firewall/ # Network/security firewall role
│ └── <other_role>/
├── tests/ # (Optional) Test environment for roles
└── README.md # This fil

Each role typically follows the standard structure: `tasks/`, `handlers/`, `defaults/`, `vars/`, `templates/`, `files/`, `meta/` etc. This structure is recommended by Ansible documentation. :contentReference[oaicite:1]{index=1}

---

## Getting Started  

### Prerequisites  
- A control node with Ansible installed (version 2.x or above)  
- Target hosts reachable via SSH, with appropriate privileges (sudo/root)  
- Inventory of hosts defined — either static or dynamic  
- For roles that manage services/configuration, ensure that the necessary package repos, OS versions, and network access are in place  
- Knowledge of Ansible basics: playbooks, variables, roles, inventories

### Installation / Setup  
```bash
# Clone the repository
git clone https://github.com/majevince/Ansible_Roles.git
cd Ansible_Roles

# (Optional) create a Python virtual environment
python3 -m venv .env
source .env/bin/activate
pip install ansible

# Review ansible.cfg and inventory files, update them for your environment
Usage Examples
Example playbook
# playbooks/site.yml
- hosts: all
  become: true
  roles:
    - role: common
    - role: hardening
    - role: nginx
      vars:
        nginx_listen_port: 8080
Running the playbook
ansible-playbook -i inventory/production.yml playbooks/site.yml --check
ansible-playbook -i inventory/production.yml playbooks/site.yml

