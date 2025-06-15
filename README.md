# Codebattle K3s Cluster Ansible Automation

## Prerequisites

1. **Ansible Control Machine**:
   - Ansible 2.12+ installed

2. **Network Requirements**:
   - Hosts must be able to communicate with each other
   - Internet access for downloading K3s, Flux, and packages

## Quick Start
1. **Update the inventory file** (`inventory/hosts.yml`):

   ```yaml
   all:
     children:
       masters:
         hosts:
           master-01:
             ansible_host: YOUR_MASTER_IP
       workers:
         hosts:
           worker-01:
             ansible_host: YOUR_WORKER_IP
           ...
   ```

2. **Configure users**:
   Edit `group_vars/all.yml` and add users with actual public keys:
   
   ```yaml
   users:
     - name: kjubybot
       ssh_key: "ssh-rsa YOUR_ACTUAL_PUBLIC_KEY kjubybot@yourdomain.com"
   ```
   
3. **Run the deployment**:
 
   ```bash
   ansible-playbook -i inventory site.yml
   ```
   
After verifying that everything's working, run the SSH playbook to fortify access:

```bash
ansible-playbook -i inventory ssh.yml
```