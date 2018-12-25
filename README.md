Ansible Role: Deploy cloud init image on KVM
=========

This role help deploy a new CentOS 7 vm on KVM.

*Details*
- Download cloud init Image.
- Generate cloud init user/meta data and booting iso.
- Increase root storage size to 20G.
- Clean up cd-rom/booting iso/user/meta data

**Tested Cloud Init Image**
- CentOS

Requirements
------------
None

Role Variables
--------------

| Name                     | Default value                                                                    | Requird | Description                                                |
| ------------------------ | -------------------------------------------------------------------------------- | ------- | ---------------------------------------------------------- |
| kvm_install_host         | localhost                                                                        | no      | The host where KVM install                                 |
| kvm_vm_pool_dir          | /var/lib/libvirt/images                                                          | no      | The path where KVM VM images are stored                    |
| vm_data_dir              | /root/kvm/vms                                                                    | no      | The path where VM information are stored                   |
| vm_recreate              | true                                                                             | no      | Set false, if the same vm exist                            |
| cloud_init_vm_image      | CentOS-7-x86_64-GenericCloud.qcow2                                               | no      | Cloud init image name                                      |
| cloud_init_vm_image_link | https://cloud.centos.org/centos/7/images/CentOS-7-x86_64-GenericCloud-1809.qcow2 | no      | Cloud init image download link                             |
| cloud_init_user_data     | {{vm_data_dir}}/{{vm_name}}/user-data                                            | no      | Cloud init user data file                                  |
| cloud_init_meta_data     | {{vm_data_dir}}/{{vm_name}}/meta-data                                            | no      | Cloud init meta data file                                  |
| cloud_init_iso_image     | {{vm_data_dir}}/{{vm_name}}/cidata.iso                                           | no      | Cloud init booting image                                   |
| vm_name                  | CentOS_Base                                                                      | no      |                                                            |
| vm_local_hostname        | base.example.com                                                                 | no      | VM internal hostname(it can be the same with vm_hostname)  |
| vm_hostname              | base.example.com                                                                 | no      | VM public hostname                                         |
| vm_public_key            | {{lookup('file','~/.ssh/id_rsa.pub')}}                                           | no      | SSH public key to login to the VM(ocp/redhat,centos/(ssh)) |
| vm_cpu                   | 2                                                                                | no      |                                                            |
| vm_memory                | 2048                                                                             | no      |                                                            |
| vm_network_br            | virbr0                                                                           | no      | Default bridge name that the VM will use                   |
| vm_root_disk_size        | 20G                                                                              | no      |                                                            |


Dependencies
------------

None

Example Playbook
----------------
~~~
- name: Example Playbook
  hosts: localhost
  gather_facts: false
  tasks:
    - import_role:
        name: ansible-role-kvm-cloud-init-vm

~~~





License
-------

BSD/MIT

Author Information
------------------

This role was created in 2018 by [Jooho Lee](http://github.com/jooho).

