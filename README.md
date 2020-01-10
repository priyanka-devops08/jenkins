Ansible Role: osm_jenkins
=========

This ROLE will install jenkins server 
- Supported Distributions
  * RedHat:7
  * RedHat:6
  * Ubuntu:bionic
  * Ubuntu:xenial

References
=========
- **[software](https://jenkins.io/)**

Version History
---------------

|**Date**| **Version**| **Description**| **Changed By** |
|----------|---------|---------------|-----------------|
|**June '15** | v.1.0 | Initial Draft | Sudipt Sharma |

Jenkins Versions
=========

- This role will fetch and install latest jenkins version available in repository but if you want to install a specific veriosn you may pass it in variables. I have tested it with last 5 versions on RHEL7 and it is working fine.


Requirements
------------
```
* curl
* libselinux-python
* initscripts
* apt-transport-https
```

Role Variables
--------------

**jenkins username and password {change them for your installation}**
|**Variables**| **Default Values**| **Description**|
|----------|---------|---------------|
| jenkins_admin_username | admin | Username of Admin |
| jenkins_admin_password | admin | Password of Admin user|
| jenkins_connection_delay | 5 | Wait for Jenkins to start up before proceeding |
| jenkins_connection_retries | 60| Retry to execute task if it fails to start Jenkins |
| jenkins_home | /var/lib/jenkins | Home Directory of jenkins|
| jenkins_hostname | localhost| Hostname for Jenkins |
| jenkins_http_port | 8080 | Port on which Jenkins runs|
| jenkins_jar_location | /opt/jenkins-cli.jar | Location where jar file for jenkins stores|
| jenkins_url_prefix | ""| URL prefix used in jenkins url|
| jenkins_java_options | "-Djenkins.install.runSetupWizard=false" | Set java options|
| jenkins_plugins| ['git']| Plugins add in Jenkins|
| jenkins_plugins_state | present | Jenkins plugin state|
| jenkins_plugin_updates_expiration | 86400 | Number of seconds after which a new copy of the update-center.json file is downloaded|
| jenkins_plugin_timeout | 300 | Jenkins Server connection timeout in secs|
| jenkins_plugins_install_dependencies | yes | Defines whether to install plugin dependencies. |
| jenkins_process_user | jenkins | Jenkins process username|
| jenkins_process_group | "{{ jenkins_process_user }}" | Jenkins process groupname|

Dependencies
------------

- Java {version 8 preferred}

Inventory
----------
An inventory should look like this for galera cluster:-
```ini
[jenkinshost]                 
192.168.1.198    ansible_user=ubuntu   
192.168.3.201    ansible_user=opstree 
```

Example Playbook
----------------

* Here is an example playbook:-

```sh
---
- hosts: jenkinshost
  become: yes
  roles:
    - jenkins

```
* ansible-playbook site.yml --vault-password-file vault_secret.sh
> vault_secret.sh is a simple script with single echo statement as: echo $password, where $password will be used to decrypt variables file: vars/adminpass.yml containing jenkins admin user login credentials.

* Password for decrypting vars/adminpass.yml for this role is: OcCeybCiWist3

Plugins
-------
* By default it will install 'git' but you may pass more plugins in the list in defualts/main.yml playbook 

Test Cases/Functionality
------------------------
* 

Author Information
------------------

- Yashvinder Hooda
- yashvinder.hooda@opstree.com
