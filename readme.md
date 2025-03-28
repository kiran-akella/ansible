# Ansible Automation ⚙️

## 🔍 **Introduction**
Ansible is an open-source IT automation tool that simplifies configuration management, application deployment, and orchestration. It uses an agentless architecture and YAML-based playbooks for easy automation.

---

## 🏗️ **Why Use Ansible?**
✅ Agentless (No need to install agents on managed nodes)  
✅ Simple YAML syntax (human-readable configurations)  
✅ Scalable and efficient  
✅ Secure and consistent  
✅ Works with cloud, containers, and on-prem infrastructure  

---

## 📥 **Installation**
### 📌 **Install Ansible on Linux (Ubuntu/Debian)**
```bash
sudo apt update
sudo apt install ansible -y
```

### 📌 **Install Ansible on RHEL/CentOS**
```bash
sudo yum install ansible -y
```

### 📌 **Verify Installation**
```bash
ansible --version
```

---

## 📂 **Ansible Directory Structure**
```bash
ansible-project/
│-- inventory  # List of managed nodes
│-- playbook.yml  # Ansible playbook
│-- roles/  # Reusable roles
│   ├── webserver/
│   │   ├── tasks/
│   │   ├── handlers/
│   │   ├── templates/
```

---

## 📑 **Ansible Inventory File**
Ansible manages servers using an **inventory file**, typically located at `/etc/ansible/hosts`.
```ini
[web_servers]
web1.example.com
web2.example.com

[database_servers]
db1.example.com
```
Test connectivity to servers:
```bash
ansible all -m ping
```

---

## 📜 **Ansible Playbook**
Playbooks are YAML files that define automation tasks.

### 📌 **Basic Playbook Example**
```yaml
- name: Install and start Nginx
  hosts: web_servers
  become: yes
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start Nginx
      service:
        name: nginx
        state: started
```
Run the playbook:
```bash
ansible-playbook playbook.yml
```

---

## 🔄 **Common Ansible Modules**

| Module  | Purpose |
|---------|---------|
| `ping`  | Check connectivity |
| `apt`   | Install packages (Debian-based systems) |
| `yum`   | Install packages (RHEL-based systems) |
| `copy`  | Copy files to remote systems |
| `file`  | Manage file attributes (permissions, ownership) |
| `service` | Start/Stop services |
| `user`  | Manage user accounts |
| `command` | Run shell commands |
| `shell`  | Execute shell scripts |

Example:
```bash
ansible all -m command -a "uptime"
```

---

## 🏗️ **Ansible Roles**
Roles help organize playbooks into reusable components.
```bash
ansible-galaxy init my_role
```
This creates a structured directory with `tasks/`, `handlers/`, `templates/`, etc.

Example role task (`tasks/main.yml`):
```yaml
- name: Ensure Apache is installed
  apt:
    name: apache2
    state: present
```

Include the role in a playbook:
```yaml
- name: Deploy Web Server
  hosts: web_servers
  roles:
    - my_role
```

---

## 📅 **Scheduling Ansible Tasks**
### 📌 **Using Cron Job**
Run a playbook every day at midnight:
```bash
crontab -e
```
Add the entry:
```bash
0 0 * * * ansible-playbook /path/to/playbook.yml
```

---
