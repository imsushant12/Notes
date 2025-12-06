<h1 style="text-align:center;"> Ansible </h1>

We can define Ansible as an **agent-less** (meaning that it does not require a client-side agent to be installed on the managed hosts (servers or devices) for communication and execution of tasks), open-source IT configuration management, deployment, and orchestration tool. It aims to provide large productivity gains to a variety of automation challenges. 

It works by connecting to remote nodes over **SSH** and executing small programs, called **Ansible modules**, on them. These modules are written in Python and are responsible for making changes to the nodes' configuration or state.

- It turns your code into IAS (Infrastructure As Code)
- It works with the PUSH mechanism (Chef works with the PULL mechanism).
- It was developed by **Michael Dehaan** in 2012. Red Hat bought it in 2015.
- Its GUI software is Ansible Tower owned by RedHat.
- No constraint on OS.
- It is quite secure due to the usage of SSH and being agent-less in nature. It is also very lightweight.
- We cannot achieve full automation by Ansible as we have to push the update. But we can design our automation workflow.
  

--- 
### Architecture

```
+-----------------+   +-----------------+   +-----------------+
|                 |   |                 |   |                 |
|  Control Node   |   | Managed Node(s) |   | Managed Node(s) |
| (Your Computer) |   |  (Servers or    |   |  (Servers or    |
|                 |   |   Devices)      |   |   Devices)      |
+-----------------+   +-----------------+   +-----------------+
        ^                      ^                     ^
        |                      |                     |
        |         push         |         push        |
        |                      |                     |
        |                      |                     |
        +----------------------+---------------------+
                 Ansible Server (Control Node)
```

- We write our scripts in YAML and store them in the **playbook**.

---

### Important Terms

#### Task
A task is a single step in a playbook. Tasks are executed sequentially, and each task can call one or more modules. Tasks are defined using ``YAML`` syntax, and each task has a name and a set of parameters.

#### Play
A play is a collection of tasks that are executed on a specific group of hosts. Plays are defined within a playbook, and they are executed sequentially. Each play has a name and a set of tasks.

#### Playbook
A playbook is a ``YAML`` file that defines a set of tasks to be executed on a group of hosts. It is the primary unit of automation in Ansible. A playbook is divided into **plays**, which define a set of tasks to be executed on a specific group of hosts. It serves as the main blueprint for an automation workflow.

```xml
task > play > playbook
```

#### Role
A role is a way to organize and structure your automation tasks. It's like a collection of related tasks, variables, and files that are grouped together to perform a specific function or set of functions. Roles make it easier to reuse and share your automation code. Roles are a way to modularize your automation code, making it more organized, reusable, and easier to understand. They are a key concept in Ansible that promotes best practices in terms of structuring your playbooks (automation scripts) and making your automation code more maintainable.

---
#### Relationship between Roles, Plays, and Playbooks:
The relationship is hierarchical: Playbooks contain plays, and plays can include roles.

---

#### Module
A module is a reusable piece of code that performs a specific task. Modules are written in Python and are typically located in the ``/usr/share/ansible/modules`` directory. To use a module in a playbook, you specify the module's name and any required parameters.

#### Fact
A fact is a piece of information about a managed host. Facts are collected by Ansible before a playbook is executed, and they can be used in tasks to customize the automation. Facts are typically collected using modules, and they are stored in a ``JSON`` format.

#### Inventory
An inventory is a list of managed hosts. The inventory is used by Ansible to connect to the managed hosts and execute tasks. Inventories can be defined in ``YAML`` or ``JSON`` format, and they can be stored in a file or in a database.

#### Handler
A handler is a special task that is executed when a condition is met. Handlers are typically used to handle events, such as notifications or errors. Handlers are defined using ``YAML`` syntax, and they have a name and a set of parameters.

#### Host
A host is a managed node. Hosts are defined in the inventory, and they are the targets of automation tasks. Hosts can be physical servers, virtual machines, or network devices.

### Useful commands
1. List all the hosts
    ```bash
    ansible all --list-hosts
    ```
    - This will display a list of all the hosts in your ``inventory``, including their ``hostnames`` and ``IP addresses``.
2. List all the hosts of a specific group, we can use:
    ```bash
    ansible <group-name> --list-hosts
    ```
    - We can also specify the range of groups as: ``<group-name>[start: stop]``. Example: ``ansible[0:4]``.
    - We can also specify more than one group using a colon. Example: ``<group-1>:<group-2>``. 

---

### Working with Ansible
1. The first step should be to install Ansible on the control node, not the managed nodes. Ansible is an agent-less tool, so there is no need to install it on the machines that you want to automate.
2. To add other nodes to the Ansible server, we need to paste the private IP of those nodes in the **hosts** file. The path of this file is: ``/etc/ansible/hosts``.
3. After updating the ``hosts`` file, we need to update the configuration file. The path of this file is: ``/etc/ansible/ansible.cfg``. We need to un-comment the ``inventory`` and ``sudo`` lines in the configuration file (if not). 
   
    > **Note**: 
    > 1. The ``inventory`` line specifies the location of the host file, which contains the private IP addresses of the managed nodes that Ansible should manage. 
    > 2. The ``sudo-user`` line specifies the username that Ansible should use when executing commands on the managed nodes.
4. To establish the connection with the node, we need to use the command: ``ssh <node-private-IP-address>``. If we want to modify the ``SSH`` configuration file, we can find it at: ``/etc/ssh/sshd_config``.

---

### How to use the private-public key for connection using ``SSH``
1. Generate the key-value pair, use the command: ``ssh-keygen``. The key will be generated with the ``.ssh`` extension and it will be hidden. The private key will be ``id_rsa`` and the public one will be ``id_rsa_pub``.
2. Copy the public key in the nodes to be managed. We can use the command: ``ssh-copy-id <user>@<node-IP-address>``.
    > **Note**: Once you have entered the password, the public key will be copied to the node's ``~/.ssh/authorized_keys`` file.

---

### Ad-hoc commands, Modules, and Playbooks
To push our code to the managed node, we have three ways:
1. Using Ad-hoc commands
2. Using modules
3. Using playbooks

#### 1. Ad-hoc commands
Ad-hoc commands are quick and easy way to execute simple Linux commands on one or more managed nodes. They are not idempotent, meaning that they will always run the specified command, even if the state of the node has not changed. This makes them suitable for one-time tasks, such as checking the uptime of a server or restarting a service. The ad-hoc command uses the ``usr/bin/ansible`` command line tool to automate the single task.

##### Syntax
We can give the commands with the help of an option **``-a``**.
```bash
ansible <group-name> -a <linux-command>``
```

##### How to use them?
- Example:
    ```bash
    ansible all -a "ls"
    ```
    - This command will list the files of all the managed nodes.
- We can also install packages and do other such works with ad-hoc commands but it is not recommended to do with ad-hoc commands. Example:
    ```bash
    ansible <group-name> -a "sudo yum install <package-name> -y"
    ```
    - We can also use the ``-b`` tag for the same. The ``-b`` tag resembles become. 
        > **Note**: The ``-b`` option can be used for privilege escalation (similar to "become") if you need root privileges.  
    - Example:
    ```bash
    ansible <group-name> -ba "yum install <package-name> -y"
    ```

#### 2. Modules
It uses the reusable YAML scripts to run a single task. Ansible ships with a number of modules (called module libraries) that can be executed directly on the remote host or through the playbook.

They are more powerful than ad-hoc commands because they are idempotent and can be used to manage complex configurations. Ansible provides a large collection of modules for a variety of tasks, such as installing packages, managing users and groups, and configuring services.

The ansible modules can be found on the location: ``/etc/ansible/hosts``.

##### Syntax
```bash
ansible -m <module-name> -a "<YAML-script>"
```

##### How to use them?
- We can give the command with the help of option **``-m``** specified with the module name. In the argument, we don't write the Linux command but we write the YAML scripts.
    - To denote a package: ``pkg=<package-name>``
    - To denote the state of the package:
        - install: ``state=present``
        - update: ``state=latest``
        - uninstall: ``state=absent``
        - start: ``state=started``
    - Example:
        ```bash
        ansible -b -m yum -a "pkg=<package-name> state=present"
        ```
- Some important modules of Ansible are: ``copy``, ``yum``, ``service``, ``setup``, etc.
- The **``setup``** module is quite an important module that runs automatically to fetch the current configuration of the managed node. We can also call it to get the current details of the machine. Example:
    ```bash
    ansible -m setup
    ```
    - To get a specific detail, we can use the filter. Example:
        ```
        ansible -m setup -a "filter=*ipv4*"
        ```

#### 3. Playbooks
Playbooks are written in YAML format. Playbooks usually consist of vars, tasks, handlers, roles, etc. Each playbook consists of a list of modules. The extension of a playbook is ``.yml``.


A playbook can be divided into several sections such as:
- **Target Section**: In this section, we define the host.
- **Task Section**: In this section, we define the list of modules that need to run in an ordered manner.
- **Variable Section**: In this section, we define the variables used in the task. 

##### Important Points
- To write a playbook, we use the YAML language. 
- The playbook begins with ``---`` marking the starting, and it ends with ``...`` (optional) which marks the end of the playbook. 
- We start a line by adding ``-``. - - We also need to follow indentation strictly while writing the YAML scripts. 
- To run a playbook, we use the command: 
    ```bash
    ansible-playbook <playbook-name.yml>
    ```

##### Examples:
1. To gather information about the managed node, we can use the target section. Here we don't need to define the task as we are not doing anything on the managed node.
    ```yaml
    --- # (Gathering information)
    - hosts: <group-name>
      user: <user-name>
      become: yes
      connection: ssh
      gather_fact: yes
    ```
2. To do some work on the managed node, we can define our task in the task section. In the task section, we can give the name to our task (optional) after that we use ``action`` to define the actual task. 
    ```yaml
    --- # (Installing http)
    - hosts: <group-name>
      user: <user-name>
      become: yes
      connection: ssh
      tasks:
        - name: install httpd 
          action: yum name=httpd
          state=installed
    ```
    > **Note**: Here, we define the name of the package with ``name`` and what we have to do using ``state``.
3. We can also use **variables**. A variable gives us more flexibility. We put the variable section (**``vars``**) above the tasks section. First, we need to define the variable(s) and then use it. 
    ```yaml
    --- # (Installing httpd using variable)
    - hosts: <group-name>
      user: <user-name>
      become: yes
      connection: ssh
      vars:
        packageName: httpd
      tasks:
        - name: install httpd 
          action: yum 
          name='{{packageName}}'
          state=installed
    ```
    > **Note**: We use the double curly braces to use variables (``{{}}``).
4. We can also use **handlers**. Handlers are similar to tasks but they are dependent on some other task. So, if one task is done, it notifies the system and then the handler works.
    ```yaml
    --- # (Handlers)
    - hosts: <group-name>
      user: <user-name>
      become: yes
      connection: yes
      tasks:
        - name: install httpd 
          action: yum name=httpd
          state=installed
          notify: restart HTTPD
      handlers:
        - name: restart HTTPD
          action: service name=httpd
          state=restarted
    ```
    > **Note**: The ``notify`` statement must be the same as the ``name`` statement of handlers because this let's handler know that the previous task has been successfully done and it should start now.
5. We can also use the ``loops``. 
    ```yaml
    --- # (Loops)
    - hosts: <group-name>
      user: <user-name>
      become: yes
      connection: yes
      tasks:
        - name: adding list of users.
          user:
            name: '{{item}}'
            state: present
          loop:
            - username1
            - username2
            - username3
            - username4
            - username5

    ```

> **Note**: We can also dry run our YAML script using the ``--check`` option as:
```bash
ansible-playbook <playbook-name.yml> --check
```

---

### Condition, Roles, and Vault

#### Condition
We can use the condition (``when``) to define the specific task. For example, we have to install Apace Server on managed nodes depending upon the type of Linux distribution. Then we can write our YAML script as:
```yaml
--- # Conditional Playbook
- hosts: <group-name>
  user: <user-name>
  become: yes
  connection: ssh
  tasks:
    - name: install apache on debian
      command: apt-get -y install apache2
      when: ansible_os_family == "Debian"
    - name: install apache for RedHat
      command: yum -y install httpd
      when: ansible_os_family == "RedHat"
```
In the above script, we are using the ``command`` module to provide Linux commands depending upon the type of Linux distribution (check using ``ansible_os_family``).

#### Vault
If we want to encrypt our playbook so that it cannot be edited by any other person then we can use the concept of vault in Ansible. We can also create an encrypted playbook. Ansible uses the **AES256** encryption technique to encrypt the file.

##### Commands:
1. To encrypt an existing playbook:
    ```bash
    ansible-vault encrypt <playbook-name.yml>
    ```
2. To decrypt an encrypted playbook:
    ```bash
    ansible-vault decrypt <playbook-name.yml>
    ```
3. To create a new encrypted playbook:
    ```bash
    ansible-vault create <playbook-name.yml>
    ```
4. To edit an encrypted playbook:
    ```bash
    ansible-vault edit <playbook-name.yml>
    ```
5. To change the password of an encrypted playbook:
    ```bash
    ansible-vault rekey <playbook-name.yml>
    ```

> **Note**: At the time of encryption, you will be prompted to provide a password and confirm the password. For the decryption, you need to provide the same password else the file will be shown with random data. 

#### Roles
To manage large playbooks, we use two techniques tasks and roles.

Roles are good for organizing tasks and encapsulating data. We can organize our playbooks in a directory structure called ``roles``.

#### Diving Deep into roles
Roles in Ansible are a way to organize and structure your automation content. They allow you to group related tasks, handlers, variables, and files together in a reusable and modular way. Roles provide a higher level of abstraction, making your playbooks more maintainable and scalable.

Now, let's break down the different directories and files used in roles:

##### Roles Directory Structure:
```
+-- roles/
    +-- WebServer/
        +-- tasks/
        |   +-- main.yml
        +-- handlers/
        |   +-- main.yml
        +-- files/
        +-- templates/
        +-- vars/
        |   +-- main.yml
        +-- defaults/
        |   +-- main.yml
        +-- meta/
        |   +-- main.yml
```

The **master.yml** file is essentially your playbook file that ties everything together. It specifies which hosts to run the tasks on, the user to connect to, and which roles to include. The **master.yml** file references roles and orchestrates their execution.

We have numerous types of roles in Ansible. Some of them are:
- **default**: It stores the default variable values for the role. These can be overridden by the user.
- **files**: This directory contains static files that need to be transferred to the remote machine.
- **handlers**: Handlers are tasks that are only run when notified by other tasks. They are defined in the ``main.yml`` file inside the ``handlers`` directory.
- **meta**: This directory contains information about the role, such as dependencies, supported platforms, etc. The ``main.yml`` file inside this directory is where you define these details.
- **tasks**: This directory contains the main list of tasks to be executed by the role. The main.yml file inside the ``tasks`` directory is where you define these tasks.
- **vars**: It is the variable file for the role. The ``main.yml`` file inside this directory contains variables specific to the role. Both the **default** and **vars** can have the variables.
- **templates**: If you are using Jinja2 templates in your tasks, you can store them in this directory.

##### Why Use Roles:
- **Modularity**: Roles allow you to break down your automation into smaller, reusable components. This modularity makes it easier to manage and understand your automation code.
- **Reusability**: Once defined, roles can be easily reused across different playbooks and projects. This can save a lot of time and effort.
- **Organization**: Roles provide a clear and organized structure for your automation code, making it more maintainable and scalable, especially as your automation project grows.
- **Abstraction**: Roles abstract away the complexity of individual tasks, allowing you to focus on the high-level organization of your automation.



An overall structure can be:
```
+----------------------------------------+
|    master.yml          Roles           |
|  +--------------+   +---------------+  |
|  | Targets      |   |   WebServer   |  |
|  | Roles        |   | +----------+  |  |
|  |  - WebServer |   | |   task   |  |  |
|  |              |   | +----------+  |  |
|  +--------------+   |               |  |
|                     | +----------+  |  |
|                     | | handlers |  |  |
|                     | +----------+  |  |
|                     |               |  |
|                     | +----------+  |  |
|                     | |   vars   |  |  |
|                     | +----------+  |  |
|                     |               |  |
|                     +---------------+  |
+----------------------------------------+
```



##### How to create a role?
1. Create directory:
    ```bash
    mkdir -p playbook/roles/WebServer/tasks 
    ```
2. Create ``main.yml`` file here:
    ```bash
    touch playbook/roles/WebServer/tasks/main.yml
    ```
3. Create a ``master.yml`` file:
    ```bash
    touch master.yml
    ```
4. Write the script in the playbook (``main.yml`` file):
    ```bash
    vi playbook/roles/WebServer/tasks/main.yml
    ```

    ```yml
    - name: install apache
      yum: pkg=httpd state=latest
    ```
5. Finally, make ``mater.yml`` know about the tasks present in the ``main.yml``.
    ```bash
    vi master.yml
    ```
    ```yml
    - hosts: <group-name>
      user: <user-name>
      become: yes
      connection: ssh
      roles: 
        - WebServer 
    ```
6. Run the playbook
    ```bash
    ansible-playbook master.yml
    ```

---