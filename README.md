# ansible-role-system-config

Apply default configurations across all company based centOS systems.

This configurations are:

1. Change kernel variables using tuned;
2. Disable swap;
3. Change hostname when inventory_name is provided;
4. Enable sudo without asking for password;

**NOTE**: kernel variables and swap are only applied to hosts with docker or docker-ce installed. It is also applied to hosts located on a group with `k8s` in the group name.

# Requirements

# Role Variables

All default variables are predefined in [defaults/main.yml](defaults/main.yml).

# Example Playbook

Example playbook usage.

```
- name: Initial host setup
  hosts: 'all'
  vars:
    # Below there are some ansible values that could be also define in ansible.cfg
    ansible_become: yes
    ansible_connection: ssh
    ansible_user: ansible
    ansible_ssh_private_key_file: test_key.pem
    sudo_nopass: true
    tuned_profile_name: some-workflow
    tuned_main_summary: Optimizations for this specific workflow
    tuned_main_include: virtual-guest # Existing base profile for the new one.
    tuned_sysctl:
      - { type: "net.ipv4.ip_forward", value: "1" }
      - { type: "vm.swappiness", value: "5" }
  roles:
    - ansible-role-system-config
```

# License

MIT

# TODO


Author Information
------------------

This role was created in 2018 for Novomatic Technologies Poland purposes.
