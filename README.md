Команды и вывод

1. max@max-VirtualBox:~$ python3 -V
Python 3.10.12
2.  max@max-VirtualBox:~$ ansible --version
ansible 2.10.8

3. max@max-VirtualBox:~/Ansible$ vagrant ssh-config
vagrant ssh-config
Host nginx
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /home/max/Ansible/.vagrant/machines/nginx/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL
  PubkeyAcceptedKeyTypes +ssh-rsa
  HostKeyAlgorithms +ssh-rsa

4. max@max-VirtualBox:~/Ansible$ ansible nginx -i inventory -m ping
nginx | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
5. max@max-VirtualBox:~/Ansible$ ansible nginx -m command -a "uname -r"
nginx | CHANGED | rc=0 >>
3.10.0-1127.el7.x86_64

6. max@max-VirtualBox:~/Ansible$ ansible nginx -m systemd -a name=firewalld | grep "ActiveState" 
        "ActiveState": "inactive",

7. max@max-VirtualBox:~/Ansible$ ansible-playbook nginx.yml --list-tags

playbook: nginx.yml

  play #1 (nginx): NGINX	TAGS: []
      TASK TAGS: [epel-package, nginx-configuration, nginx-package, packages]

8. max@max-VirtualBox:~/Ansible$ ansible-playbook nginx.yml

PLAY [NGINX] *****************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************
ok: [nginx]

TASK [Install EPEL Repo package from standart repo] **************************************************************************************
ok: [nginx]

TASK [Install NGINX] *********************************************************************************************************************
ok: [nginx]

TASK [Create NGINX config-file from template] ********************************************************************************************
changed: [nginx]

RUNNING HANDLER [reload nginx] ***********************************************************************************************************
changed: [nginx]

PLAY RECAP *******************************************************************************************************************************
nginx                      : ok=5    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 

8.1. При повторном запуске выполнился без ошибок

PLAY [NGINX] *****************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************
ok: [nginx]

TASK [Install EPEL Repo package from standart repo] **************************************************************************************
ok: [nginx]

TASK [Install NGINX] *********************************************************************************************************************
ok: [nginx]

TASK [Create NGINX config-file from template] ********************************************************************************************
ok: [nginx]

PLAY RECAP *******************************************************************************************************************************
nginx                      : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

9. curl http://192.168.56.150:8080
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
<head>
  <title>Welcome to CentOS</title>
  <style rel="stylesheet" type="text/css"> 

	html {
	background-image:url(img/html-background.png);
	background-color: white;
	font-family: "DejaVu Sans", "Liberation Sans", sans-serif;
	font-size: 0.85em;
	line-height: 1.25em;
	margin: 0 4% 0 4%;
	}

	body {....

