# ansible_tips

### Create a password file
``` ~/.ansible_vault_password```

### Create the vault
```
ansible-vault encrypt_string "wrd" --vault-password ~/.ansible_vault_password
```

```
Encryption successful
!vault |
          $ANSIBLE_VAULT;1.1;AES256
          37333366303230343330333939353539393232666165623165313063616539353638626362373234
          6237393331303838313165326531653938656365633365310a333935653166303933323164633630
          36356261383636633062633039346366613963383631346630336633303537653965346333393639
          6566333038656665640a643236323636323730356162636665663032636161623362343832373235
          6463
```

### file structure for ansible

```
├── playbooks
├── roles
│   ├── ssh
│       └── tasks
├── scripts
├── site
   ├── digitalocean
        ├── group_vars
        └── host_vars

group_vars - all.yml - this applies to any host in digitalocean
host_vars - servername.yml - this applies to only that server and will override group_vars if the same variable exists in both.
```

### example of vars
```
dogs_name: bob
```

### running ansible
```
ansible-playbook playbooks/ssh.yml --vault-password ~/.ansible_vault_password -i site/digitalocean/inventory -u Youruser --become --become-method sudo --become-user root
```

### exaplanation
```
ssh.yml is your playbook
--vault-password - is a file with the supersecret vault password
-i points to your inventory
-u your username to login to the server (the one you are running ansible against
--become - means you are going to elevate your permission
--become-method - how your going to elevate
--become-user - the user you are going to become **

**the become requires you add sudoers permissions for your user.

```

