# ono-playbook
---
#- hosts: localhost
#- hosts: 
#- hosts: fortinet
- hosts: all
  #become: true

  tasks:
       - name: Clone a public GIT repo
         git:
           repo: https://github.com/ProblemSetters/devops-inventory.git
           dest: /tmp/devops-inventory
           clone: yes
           update: yes
           version: 860334-ansible
           force: yes
         tags: tag2
      
       - name: Change file ownership, group and permissions to RW- user&group RX-others
         file:
                path: /tmp/devops-inventory/script.sh
                mode: '0775'
         tags: tag2

       - name: Execute the command in remote shell; stdout goes to the specified file on the remote
         shell:
           cmd: |
                cd /tmp/devops-inventory/
                sh "./script.sh" >>onologs.txt
         args:
           executable: /bin/bash
         tags: tag2


