
---

### README.md for Shared PostgreSQL and Liferay Host

```markdown
# Ansible Playbook for Deploying PostgreSQL and Liferay on a Shared Host

This README provides step-by-step instructions for deploying PostgreSQL and Liferay on a single host using Ansible.

## Prerequisites

1. **Ansible Control Node**: Ensure Ansible is installed on your control node (the machine from which you run Ansible commands).
2. **Target Server**: One target server with SSH access.
3. **SSH Keys**: Configure SSH key-based authentication for the Ansible control node to access the target server.
4. **Ansible Vault**: Store sensitive data such as database passwords securely.

## Steps to Execute

### 1. Clone the Repository

```sh
git clone <repository_url>
cd <repository_directory>


2. Configure Inventory File
Edit the inventory/hosts file to specify the target server:


[shared_host]
shared_host.example.com

3. Configure Ansible Vault

Create a vault.yml file to store sensitive information, then encrypt it using Ansible Vault:

vault_postgres_db_password: "your_postgres_password"
vault_liferay_db_password: "your_liferay_password"

Encrypt the vault file:

ansible-vault encrypt vault.yml

4. Configure Group Variables

	Edit the group_vars/all.yml file to specify common variables:

liferay_user,liferay_version,liferay_db_user,liferay_db_name,postgres_user,postgres_version,liferay_host,postgres_host,postres_port etc..


5. Run the Playbook
Execute the playbook using Ansible:

ansible-playbook -i inventory/hosts site.yml --ask-vault-pass

6. Verify Installation
		
		Check PostgreSQL Status:

			sudo systemctl status postgresql
	
		Check Liferay Service:	

			sudo systemctl status liferay

		Verify Database and User:

			sudo -u postgres psql -c "\l"
			sudo -u postgres psql -c "\du"
		
		Access Liferay UI: Open a web browser and go to http://<shared_host_ip>:8080`.
