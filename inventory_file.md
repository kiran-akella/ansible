# Ansible inventory file in yaml.

## path: /etc/ansible/hosts

```yaml
---
all:
  children:
    kubernetes:
      hosts:
        kube-master:
          ansible_host: 34.124.218.101
        kube-worker:
          ansible_host: 35.240.168.48
    
    os:
      hosts:
        rhel: 
          ansible_host: 34.93.72.135
        ubuntu: 
          ansible_host: 34.131.230.70

    db: 
      hosts:
        postgres_sql:
          ansible_host: 34.131.83.173

  vars:
    ansible_user: root
    ansible_ssh_common_args: '-o StrictHostKeyChecking=accept-new'
```

# To validate/view the ansible inventory file

```bash
ansible-inventory --list
```

```bash
ansible-inventory --graph
```

```bash
ansible-inventory --host hostname
```
