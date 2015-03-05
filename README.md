# CentOS Recipes
Repository for learning linux in general and CentOS/Amazon Linux specifics. This repository contains basically a whole bunch of small recipes :)

 - How do I know how many cores my system has?
 - How do I install MySql?
 - How do I install Node.js?
 - How do I install Git?
 - How to allow specific user run command as sudo without password?

### How do I know how many cores my system has?

Run the command `cat /proc/cpuinfo` to list details for all cores, and run `grep 'model name' /proc/cpuinfo | wc -l` to know how many cores your system has.

### How do I install MySql?

```bash
sudo yum upgrade -y
sudo yum install mysql -y
sudo yum install mysql-server -y
sudo /etc/init.d/mysqld start
mysqladmin -u root password 'rootPassword'
sudo chkconfig mysqld on
 
# my.cnf should be located at; /etc/my.cnf
# add the following line to allow external connections; 
# bind-address = 0.0.0.0
# then restart mysql to reload configurations; 
# sudo /etc/init.d/mysqld restart
```

You will be required to grant remote access to any user you would like to be able to connect from outside localhost.

```sql
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'rootPassword';
FLUSH PRIVILEGES;
```

This is a per database permission so don't forget to use wildcards or specify specific databases.

### How do I install Node.js?

```bash
curl https://raw.githubusercontent.com/creationix/nvm/v0.13.1/install.sh | bash
source ~/.bashrc
nvm install 0.10
nvm use 0.10
sudo visudo # add `dirname $(which node)` to secure_path so you're able to `sudo node` and `sudo npm`
```

### How do I install Git?

Simply run `sudo yum install -y git`

### How to allow specific user run command as sudo without password?

Log in as root then run `sudo visudo` and add the following line `joe ALL=(ALL) NOPASSWD: /full/path/to/command`, or if you want to restrict wich arguments this user may pass you can change that line to `joe ALL=(ALL) NOPASSWD: /full/path/to/command ARG1 ARG2`.
