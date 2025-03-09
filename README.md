# 📌 MySQL-Galera Cluster Configuration with Ansible

This Ansible project automates the installation, configuration, and validation of a **MySQL-Galera** cluster on multiple nodes.

## 🚀 Requirements
- Servers with SSH access and sudo enabled.
- Ansible installed on the control machine.
- A properly configured inventory of hosts in `hosts.ini`.
- Variables defined in `roles/mysql/vars/main.yml`:
  - `mysql_root_password`: The root password for MySQL.
  - `galera_cluster_name`: The name of the Galera cluster.

## 📂 Playbook Structure
The playbook is divided into several phases, each identified with a tag (`tags`). This allows executing specific parts of the process as needed.

### 🎯 Available Tags
| Tag                    | Description |
|------------------------|-------------|
| `mysql_setup`         | Installs dependencies, configures repositories, and prepares the nodes for MySQL-Galera. |
| `stop_apparmor`       | Disables Apparmor on the MySQL nodes. |
| `bootstrap_cluster`   | Starts the primary node of the cluster with `wsrep-new-cluster`. |
| `start_secondary_nodes` | Starts the secondary nodes and adds them to the cluster. |
| `haproxy_setup`       | Configures and deploys HAProxy. |

---

## 🔧 Running the Playbook
You can run the complete playbook with:
```bash
ansible-playbook playbook.yml
```

If you only want to run a specific part of the process, use the `--tags` option:

### 1️⃣ Configure MySQL repositories and dependencies
```bash
ansible-playbook playbook.yml --tags mysql_setup
```

### 2️⃣ Disable Apparmor
```bash
ansible-playbook playbook.yml --tags stop_apparmor
```

### 3️⃣ Start the primary node of the cluster
```bash
ansible-playbook playbook.yml --tags bootstrap_cluster
```

### 4️⃣ Start secondary nodes
```bash
ansible-playbook playbook.yml --tags start_secondary_nodes
```

### 5️⃣ Configure and deploy HAProxy
```bash
ansible-playbook playbook.yml --tags haproxy_setup
```

---

## ⚡ Execution Flow
1. **`mysql_setup`** – Installs dependencies, configures repositories, and prepares the nodes.
2. **`stop_apparmor`** – Disables Apparmor on the MySQL nodes.
3. **`bootstrap_cluster`** – Starts the primary node with `wsrep-new-cluster`.
4. **`start_secondary_nodes`** – Adds the secondary nodes to the cluster.
5. **`haproxy_setup`** – Configures and deploys HAProxy.

---

## ✅ Additional Notes
- To avoid synchronization issues, ensure that the clocks of the nodes are synchronized.
- Security and authentication settings should be adjusted according to the environment requirements.
- It is recommended to test first in a development environment before running it in production.

📢 **Contributions and improvements are welcome!**

