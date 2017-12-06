# r1soft-agent
Install r1soft agent
The R1Soft Server Backup Manager is a backup application for Linux and Windows machines that runs nearly continuously and is developed by R1Soft. This application allows users to schedule disk-based backups of their server that essentially create a virtual disk image, which is then stored online.

This yml will show you how to setup your CentOS 7 server with an R1Soft Agent so that you can start taking advantage of the security of near-continuous backups.

  

 Fisrts it will install dependency, othervise it gonna give an error to install it. roles for installing all packages you can find inside tasks file
     roles:
       - r1soft-agent-centos7
#r1soft repository
    - copy:   #copy and paste r1soft.repo , i will put configuration file on r1soft.repo file
        src: /etc/ansible/roles/r1soft-agent-centos7/r1soft.repo  #change it for you own preference 
        dest: /etc/yum.repos.d
        owner: root
        group: root
        mode: 0644
#firewall
     - name: Opening appropriate port on Remote system for agent
       firewalld:
         port: 1167/tcp
         permanent: true
         state: enabled
         zone: public


    - name: restart firewalld
      service: name=firewalld state=restarted


    - name: restart service    # agent service restart
      shell: /etc/init.d/cdp-agent restart
    - name: get a key 
      command: r1soft-setup --get-key http://ip:8080






# r1soft-agent-centos7
