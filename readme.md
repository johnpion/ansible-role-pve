# Ansible Role 'Proxmox VE 7'

Install and management Proxmox VE 7

## system
OS: Debian 11

Now need use 'token' in Proxmox

### vars
```
- name: Create CT
  delegate_to: localhost
  community.general.proxmox:
    api_host: "{{ inventory_hostname }}"
    api_user: root@pam
    api_token_id: ansible
    api_token_secret: "{{ proxmox_api_token_secret }}"
    cores: "{{ ct.cpu | default(pct_cpu) }}"
    cpus: "{{ ct.cpu | default(pct_cpu) }}"
    disk: "{{ ct.disk | default(pct_disk) }}"
    hostname: "{{ ct.hostname }}"
    memory: "{{ ct.memory | default(pct_memory) }}"
    nameserver: "{{ ct.nameserver | default(pct_nameserver) }}"
    netif: "{{ ct.netif }}"
    node: "{{ pct_node }}"
    onboot: "{{ ct.onboot | default(pct_onboot) }}"
    ostemplate: "{{ ct.ostemplate | default(pct_ostemplate) }}"
    pubkey: "{{ pct_pubkey }}"
    swap: "{{ ct.swap | default(pct_swap) }}"
    # searchdomain: "{% if item.searchdomain is defined %}{{ item.searchdomain }}{% else %}{{ pct_searchdomain }}{% endif %}"
    # storage: "{{ ct.storage | default(pct_storage) }}"
    unprivileged: "{{ ct.unprivileged | default(pct_unprivileged) }}"
    vmid: "{{ ct.vmid }}"
  when: pct is defined
  loop: "{{ pct }}"
  loop_control:
    loop_var: ct
  tags: pct_create
```
