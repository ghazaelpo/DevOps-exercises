# Working with loops and systemd module

- You must provisioning a new server. Requiered packages to install in all nodes:
    - cups
    - vim
    - httpd
    - gcc
        
        
        First part of the activity, installing packages
        
        ![Screen Shot 2021-10-21 at 0.09.31.png](Working%20with%20loops%20and%20systemd%20module%20d9897e40340449bea4d39145a75a5a9e/Screen_Shot_2021-10-21_at_0.09.31.png)
        
        ![Screen Shot 2021-10-21 at 0.03.33.png](Working%20with%20loops%20and%20systemd%20module%20d9897e40340449bea4d39145a75a5a9e/Screen_Shot_2021-10-21_at_0.03.33.png)
        
    
    Even if we execute again the command will see OK
    
    ![Screen Shot 2021-10-21 at 0.03.58.png](Working%20with%20loops%20and%20systemd%20module%20d9897e40340449bea4d39145a75a5a9e/Screen_Shot_2021-10-21_at_0.03.58.png)
    
- Enable and start the service of httpd and cups, using the correct module for your distribution (service or systemd).
    
    ![Screen Shot 2021-10-21 at 0.22.25.png](Working%20with%20loops%20and%20systemd%20module%20d9897e40340449bea4d39145a75a5a9e/Screen_Shot_2021-10-21_at_0.22.25.png)
    
    ![Screen Shot 2021-10-21 at 0.19.06.png](Working%20with%20loops%20and%20systemd%20module%20d9897e40340449bea4d39145a75a5a9e/Screen_Shot_2021-10-21_at_0.19.06.png)
    

- Create playbook that install all of those packages using loops and the system configuration also must be done using loops.

```bash
---
# provisioning.yml playbook
- name: Provisioning               # Playbook name 
  hosts: all                       # Host to connect definied in inventory file
  become: yes                      # Become sudo user
  vars:                            # Variables
    packages:                      # packages variables to iterate after
      - cups                       # cups package
      - vim                        # vim package
      - apache2                    # httpd package
      - build-essential            # gcc package
    services:
      - apache2
      - cups    

  tasks:                           # Tasks to performance
    - name: Installing packages    # Task name
      apt:                         # apt module to install packages
        name: "{{ item }}"         # Item from package names 
        state: present             # state present
      loop: "{{packages}}"         # Iterate on package items

    - name: Starting services      # Task name
      service:                     # service module
        name: "{{ item }}"         # Item from service names
        state: started             # state started
      loop: "{{services}}"         # Iterate on service items
```