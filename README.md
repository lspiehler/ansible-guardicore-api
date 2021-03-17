# Install Ansible
The example below is for RHEL/CentOS 8

```
sudo dnf -y install python3-pip
sudo pip3 install --upgrade pip
pip3 install ansible --user
```

# Clone Repo
```
git clone https://github.com/lspiehler/ansible-guardicore-api.git
cd ansible-guardicore-api
```

# Authenticate and get a JWT
### Set environment variables
```
export GCUSER=youruser
export GCPASS=yourpassword
ansible-playbook auth.yml
```
### Example vars.yml file:
```
cat << EOF > vars.yml
management_server: cus-2599.cloud.guardicore.com
EOF
```
### Run the playbook
```
ansible-playbook auth.yml -e @vars.yml
```
Use the response from the previous command to set your JWT environment variable to be used for API requests
```
export GCJWT=iOjE2MTU5ODYzNzMsImlhdCI6MTYxNTg5OmJmIjoxNjE1ODk5OTczLCJpZGVZGVudGl0eSI6ImFkbWluIiwicmFuZCI6IjQwNDwNDNiMzBhLWNlZDItNGQyMi05YjczLTBRu1VFGbB3AlN7KVjb5DuK5qbfT_h0qBDgHceyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9hdCI6MTYxNTg5OTk3MywibmJmIjoxNjE1ODk5OTczLCJ
```
# List Assets
### Example vars.yml file:
```
cat << EOF > vars.yml
management_server: yourhost.cloud.guardicore.com
EOF
```
### Run the playbook:
```
ansible-playbook list-assets.yml -e @vars.yml
```

# Show a Label
### Example vars.yml file:
```
cat << EOF > vars.yml
management_server: yourhost.cloud.guardicore.com
label:
  key: Site
  value: Test
EOF
```
### Run the playbook:
```
ansible-playbook show-label.yml -e @vars.yml
```

# Add one or more dynamic criteria to a label
### Example vars.yml file:
```
cat << EOF > vars.yml
management_server: yourhost.cloud.guardicore.com
label:
  key: Site
  value: Test
new_dynamic_criteria:
  - argument: 192.168.230.0/24
    field: numeric_ip_addresses
    op: SUBNET
  - argument: 192.168.231.0/24
    field: numeric_ip_addresses
    op: SUBNET
EOF
```
### Run the playbook:
```
ansible-playbook label-add-dynamic-criteria.yml -e @vars.yml
```
# Delete dynamic criteria from a label
### Example vars.yml file:
```
cat << EOF > vars.yml
management_server: yourhost.cloud.guardicore.com
label:
  key: Site
  value: Test
del_dynamic_criteria:
  argument: 192.168.230.0/24
  field: numeric_ip_addresses
  op: SUBNET
EOF
```
### Run the playbook:
```
ansible-playbook label-del-dynamic-criteria.yml -e @vars.yml
```