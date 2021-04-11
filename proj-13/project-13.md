# **Introduction**

## **Title: Implementing Ansible Dynamic Assignments (Include) and Community/Custom Roles**

* Ansible implements functionality to dynamically include various parts of the Ansible playbook tree into an entry playbook file.

* The various parts of the Ansible playbook tree are: `vars`, `tasks`, `play`

* Dynamic allocation is different from static allocation in that; statically allocated Ansible playbook tree (vars, tasks,play) are pre-loaded before the execution of the play, while dynamic allocation are evaluated and executed while the playbook in which they are allocated is being executed.

* It is recommended to use static assignments for playbooks, because it is more reliable. With dynamic ones, it is hard to debug playbook problems due to its dynamic nature.

