## Assignment

The directory Structure is as follows:
```
assignment
|── .git
│   |── HEAD
│   |── branches
│   ├── config
│   ├── description
│   ├── hooks
│   │   ├── applypatch-msg.sample
│   │   ├── commit-msg.sample
│   │   ├── post-update.sample
│   │   ├── pre-applypatch.sample
│   │   ├── pre-commit.sample
│   │   ├── pre-push.sample
│   │   ├── pre-rebase.sample
│   │   ├── prepare-commit-msg.sample
│   │   └── update.sample
│   ├── info
│   │   └── exclude
│   ├── objects
│   │   ├── info
│   │   └── pack
│   └── refs
│       ├── heads
│       └── tags
├── README.md
├── ansible.cfg
├── configure_database_firewall.yml
├── hosts
├── orchestrate_app1_server.yml
├── orchestrate_database_server.yml
├── orchestrate_haproxy_server.yml
├── provision_app1_server.yml
└── roles
    ├── configure_product1
    │   ├── tasks
    │   │   └── main.yml
    │   ├── templates
    │   │   ├── index.html.j2
    │   │   └── product1.conf.j2
    │   └── vars
    │       └── main.yml
    ├── configure_product2
    │   ├── tasks
    │   │   └── main.yml
    │   ├── templates
    │   │   ├── index.html.j2
    │   │   └── product2.conf.j2
    │   └── vars
    │       └── main.yml
    ├── database_server_firewall
    │   ├── tasks
    │   │   └── main.yml
    │   └── vars
    │       └── main.yml
    ├── orchestrate_haproxy_server
    │   ├── tasks
    │   │   └── main.yml
    │   ├── templates
    │   │   └── haproxy.cfg
    │   └── vars
    │       └── main.yml
    ├── provision_app1_server
    │   ├── tasks
    │   │   └── main.yml
    │   └── vars
    │       └── main.yml
    ├── setup_database
    │   ├── tasks
    │   │   └── main.yml
    │   ├── templates
    │   │   ├── mysql.cnf.j2
    │   │   ├── product1_table.sql
    │   │   └── product2_table.sql
    │   └── vars
    │       └── main.yml
    └── setup_nginx_passenger
        ├── tasks
        │   └── main.yml
        ├── templates
        │   ├── p1.conf.j2
        │   └── passenger.list
        └── vars
            └── main.yml
```
**Roles:**
* **provision_app1_server** - To provision a server with ubuntu-14.04 installed.
* **setup_nginx_passenger** - To install nginx and passenger on the provisioned server.
* **configure_product1** - To copy required templates on the server and configure for the product1 app.
* **configure_product2** - To copy required templates on the server and configure for the product2 app.
* **setup_database** - Role to setup mysql and create database for product1 and product2. Also creates one sample table for both databases.
* **database_server_firewall** - To setup firewall for allowing traffic from app1 server on the port on which mysql operates using ufw.
* **orchestrate_haproxy_server** - Role to setup haproxy server to point to app1.

**Playbooks:**
> Few playbooks are there which can be used directly to provision the instance, orchestrate it and configure the required things. Further playbook can be created with different combination of roles to solve different requirements.

**Considerations:**
* AWS Cloud is being used.
* `provision_app1_server` role can be used to launch number of instances for database server, app server, HAProxy servers in case we need to scale.
* `Ruby/Rails` is assumed to be installed on the system.
* sample `index.html` file with different content is being used to display the sample content of `product1` and `product2`.
* Firewall is being setup using `ufw`.
* Default `VPC` and `subnet` is being used.
* `product1` and `product2` are considered to be on the same instance.
* Already created `security groups` are being used for the provisioned server.