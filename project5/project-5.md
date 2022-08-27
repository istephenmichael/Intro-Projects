# PROJECT 5: Client/Server Architecture Using A MySQL Relational Database Management System



### Step 1: Install mysql-server on Linux server and mysql-client on Linux client 



`sudo apt update` `sudo apt install mysql-server` (for MySQL server)

`sudo apt update` `sudo apt install mysql-client` (for MySQL client)

---


### Step 2: Create new mysql user for client on mysql-server machine and grant privileges



`sudo mysql`


set a password for the root user, using mysql_native_password as default authentication method. We’re defining this user’s password as PassWord.1.

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

`sudo mysql_secure_installation`

`sudo mysql -p`

`sudo mysql -h localhost` (Enter mysql runtime)

`CREATE USER 'user'@'%' IDENTIFIED BY 'password';`

`GRANT ALL PRIVILEGES ON *.* TO 'user'@'%' WITH GRANT OPTION;`

`FLUSH PRIVILEGES;`

---


### Step 3: Configure mysql config file on server machine




`sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf` (Change the bind-address from ***127.0.0.1 to 0.0.0.0***)


![bind-address](https://user-images.githubusercontent.com/85305109/187007750-40785422-a752-433b-9d3d-90ded2748335.jpg)


`sudo systemctl restart mysql` (Restart mysql service)

---


### Step 4: Connect from client machine



`mysql -h internal-ip-of-server -p` (Connect to mysql server, enter password when prompted.)

![last](https://user-images.githubusercontent.com/85305109/187007673-93850928-ccf8-4db5-ae8a-df2fa16902de.jpg)




