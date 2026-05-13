PART:1:
Step:1: ceate a three instances with aws linux and t3.micro with proper key name,
    and name it as "Controller-Node","Node1"and "Node2".
Step:2: connet the three server in MobaXterm and update, install Net-tools,wget,vim package in it,
 change the Hostname as Controller-Node,Node1,Node2 in three 3 server.
step:3: mapping the ip of 3 servers in vim /etc/hosts,

 EX:

 172.31.24.135   Controller-Node
 172.31.30.120   Node1
 172.31.31.109    Node2

 and exit it by typing :wq!
step:4: * In Controller-Node type all 3
        * In Node1 - make only Controller-Node and Node1
        * In Node2 -make only Controller-Node and Node2
step:5: Now we have to add users in all 3 Node

EX: #useradd narasimha
    #passwd narasimha
    pass:1234

  make it in three servers
 step:6:Then we have to do #vim/etc/sudoers and make it Ex: 
       root ALL=(ALL)  ALL
       narasimha  ALL=(ALL)  NOPASSWD:ALL    {it is no 100 line}
    and we have to it in 3 nodes
 step:7: Now we have make SSH configuration useing #vim /etc/ssh/sshd_config  and make passwordAuthetition "YES" and exit useind :wq!
     Make it in three server
 step:8: And restart all 3 servers by using #systemctl restart sshd
 step:9:And we log in user ex narasimha by using #su - name EX: su - narasimha in Controller-node only
 step:10 : #ssh-keygen  ---it will gerate key
 and type yes ,yes and yes
 step:11: And type "$ ls ~/.ssh" for checking keys
 ex: id_rsa  id_rsa.pub
  
 ###################################
 Part:2:
 step:1: To connet the node1 and node2 sever type $ssh narasimha@Node1 --for Node1 type passwd:1234
 $ssh narasimha@Node2 --for Node2 type passwd:1234

step:2: to copy the file : $ssh-copy-id narasimha@Node1   ---for Node1
$ssh-copy-id narasimha@Node2

#############################################
Part:3: How to install package Ansible

step:1:Ansilble installation
 $ sudo dnf install ansible -y
 $ ansible --version
 $ sudo cd /etc/ ansible/
 $pwd
 /home/narasimha
 $cd /etc/ansible/
 /ect/ansible
 $ls
 roles 
 $ sudo touch hosts
 -rw-r--r--. 1 root root 0 May 12 05:22 hosts
 sudo chmod 777 hosts
 ls -l hosts
 $sudo vim hosts


[webservers]
Node1
Node2

[appservers]
app1
app2
app3

[dbservers]
db1
db2

host1
host2


:wq!

step:2: 
$ ansible -m command-a "uptime"webservers
$ sudo vim ~/.ansible.cfg

interpreter_python=auto_silent



:wq!

$ ansible -m command -a "uptime" webservers

