[![CI](https://github.com/de-it-krachten/ansible-role-vdo/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-vdo/actions?query=workflow%3ACI)


# ansible-role-vdo

Installs and configurtion VDO support



## Dependencies

#### Roles
None

#### Collections
- community.general

## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- Red Hat Enterprise Linux 10<sup>1</sup>
- RockyLinux 8
- RockyLinux 9
- RockyLinux 10
- OracleLinux 8
- OracleLinux 9
- OracleLinux 10
- AlmaLinux 8
- AlmaLinux 9
- AlmaLinux 10

Note:
<sup>1</sup> : no automated testing is performed on these platforms


## Role Variables
### defaults/main.yml
<pre><code>

</pre></code>

### defaults/family-RedHat-10.yml
<pre><code>
# VDO packages
vdo_packages:
  - lvm2
  - vdo
  - vdo-support
</pre></code>

### defaults/family-RedHat-8.yml
<pre><code>
# VDO packages
vdo_packages:
  - lvm2
  - vdo
  - vdo-support
  - kmod-kvdo

# VDO server
vdo_service: vdo

# Kernel module
vdo_module: kvdo
</pre></code>

### defaults/family-RedHat-9.yml
<pre><code>
# VDO packages
vdo_packages:
  - lvm2
  - vdo
  - vdo-support
  - kmod-kvdo

# Kernel module
vdo_module: kvdo
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'vdo'
  hosts: all
  become: 'yes'
  vars:
    molecule_driver: '{{ lookup(''env'', ''MOLECULE_DRIVER_NAME'') }}'
    vdo_lvm:
      vg:
        - name: vgvdo
          pv:
            - '3:0:0:0'
          pvresize: true
      lv:
        - name: lvvdo1
          type: vdo
          size: 5G
          pool_name: vpool0
          virtualsize: 10G
          vg: vgvdo
          fstype: xfs
          mp: /vdo1
    vdo_lvm2:
      vg:
        - name: vgvdo
          pv:
            - '3:0:0:0'
          pvresize: true
      lv:
        - name: lvvdo1
          type: vdo
          size: 9G
          pool_name: vpool0
          virtualsize: 40G
          vg: vgvdo
          fstype: xfs
          mp: /vdo1
  tasks:
    - name: Include role 'vdo'
      ansible.builtin.include_role:
        name: vdo
</pre></code>
