# LinuxTask

## Q1:
```
pvcreate /dev/sda7 /dev/sda8
vgcreate -s 16M vg1 /dev/sda7 /dev/sda8
lvcreate -l 50 -n lvm02
mkfs.ext4 /dev/vg1/lvm02
mkdir -p /mnt/data
blkid /dev/vg1/lv1
vim /etc/fstab
UUID=5ba707bd-a49e-4bc2-b4d4--57a55008d234 /mnt/data ext4 defaults 0 0
:wq!
mount -a
df -h
```

## Q2:
```
useradd -u 601 -s /sbin/nologin user1
passwd user1
redhat

groupadd TrainingGroup
usermod -g TrainingGroup user1

groupadd admin
useradd -G admin user2
useradd -G admin user3
passwd user2
redhat
passwd user3
redhat

su root
visudo
user3 ALL=(ALL) ALL
:wq!
```

## Q3:
```
ssh-keygen -t rsa
ssh-copy-id ralboom@192.168.43.122 
ssh ralboom@192.168.43.122
```

## Q4:
```
cp /etc/fstab /var/tmp/
chgrp admin /var/tmp/fstab
setfacl -m u:user1:rwx /var/tmp/fstab
setfacl -m u:user2:--- /var/tmp/fstab
```

## Q5:
```
setenforce enforcing 
vi /etc/selinux/config
SELINUX=enforcing
:wq!
```

## Q6:
```
vi script2.sh
#/bin/bash
(while true; do echo -n "radwan " >> /home/ralboom/Desktop/out;sleep 1; done)
:wq!
chmod +x ./script2.sh
timeout -sHUP 10m ./script2.sh &
ps -ef
kill -15 3480
```

## Q7:
```
yum install tmux
yum install httpd
yum install yum-utils createrepo -y
rpm -ivh https://repo.zabbix.com/zabbix/4.4/rhel/7/x86_64/zabbix-release-4.4-1.el7.noarch.rpm
yum install epel-release -y
yum-config-manager --disable extras
yum -y install zabbix zabbix-web php zabbix-server zabbix-agent
```

## Q8:
```
systemctl status firewalld
systemctl start  firewalld
firewall-cmd --zone=public --add-port=443/tcp --permanent
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --add-rich-rule='rule family=ipv4 source address =192.168.0.109 service name=ssh reject'
firewall-cmd --reload
 ```

## Q9:
```
vi script.sh
#/bin/bash
utmpdump /var/log/wtmp | awk -F "[" '{print $9, $5}' | awk -F "]" '{print $1,$2}'| awk '{print $1,$2,$3,$4,"UTC "$5,"- "$6}' > output
:wq!
chmod +x script.sh 
crontab -e
30 01 * * * /home/ralboom/Desktop/script.sh
:wq!
crontab -l
```

## Q10:
```
yum -y install mariadb-server
mysql_secure_installation
yum install iptables-services
systemctl enable iptables
iptables -A INPUT -p tcp --dport 3306 -j ACCEPT
service iptables save

mysql -u root -p
create database studentdb;
grant all privileges on studentdb.* to user@'localhost' identified by 'user';
exit
mysql -u user -p
use studentdb;
CREATE TABLE student(id INT NOT NULL AUTO_INCREMENT,firstname VARCHAR(100) NOT NULL,lastname VARCHAR(100) NOT NULL, 
program VARCHAR(100) NOT NULL, graduation_year INT NOT NULL,number VARCHAR(100) NOT NULL,primary key (id));

INSERT student VALUES (1,'Allen','Brown','mechanical', 2017,'110-001');
INSERT student VALUES (2,'David','Brown','mechanical', 2017,'110-010');
INSERT student VALUES (3,'Mary','Green','mechanical', 2018,'110-011');
INSERT student VALUES (4,'Dennis','Green','electrical', 2018,'110-100');
INSERT student VALUES (5,'Joseph','Black','electrical', 2018,'110-101');
INSERT student VALUES (6,'Dennis','Black','electrical', 2020,'110-110');
INSERT student VALUES (7,' Ritchie','Salt','computer science', 2020,'110-111');
INSERT student VALUES (8,' Rebort','Salt','computer science', 2020,'111-000');
INSERT student VALUES (9,'David','Suzuki','computer science', 2020,'111-001');
INSERT student VALUES (10,'Mary','Chen','computer science', 2020,'111-010');

SELECT * FROM student;
exit
```


