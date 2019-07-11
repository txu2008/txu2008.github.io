---
layout: post
title:  "RSA ssh key login 互信"
date:   2019-07-11 12:34:51
categories: Linux
tags: ssh
---

* content
{:toc}

RSA ssh key login



1. vi /etc/ssh/sshd_config
```
PubkeyAuthentication yes
PasswordAuthentication no
AuthorizedKeysFile .ssh/authorized_keys
```

2. vi /etc/ssh/ssh_config
```
Host *
        GSSAPIAuthentication yes
        RSAAuthentication yes
        PasswordAuthentication no
```
   
3. 生成rsa key:
```
ssh-keygen -t rsa -P ''     
cat ~/.ssh/id_rsa.pub > ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
systemctl restart sshd
```

4. copy 到其他机器上：
```
ssh-copy-id -i ~/.ssh/id_rsa.pub <IP>
或
cat /root/.ssh/id_rsa.pub | ssh root@node2 'cat - > ~/.ssh/authorized_keys'
chmod 600 ~/.ssh/authorized_keys
```