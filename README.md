# Umami-final

## What you need to Have before Installing Umami! 
1. Update your Ubuntu Server 
`Sudo Apt Update` and `Sudo Apt upgrade`
2. Get A domain Name! 
3. Install Node.JS & NVM 
4. Install Mysql

## First Creating your Umami Database
1. you should log in to MySQL as root by this command 

     `# mysql -u root`

2. You will be creating a database and A user and putting a password for the user.
   Database Name : umami 
   
      `mysql> CREATE DATABASE UMAMI;`
      
   Database user name : UmamiUser - note that you have to change MyPass123 to a unique password.
   
      `CREATE USER 'UmamiUser'@'localhost' IDENTIFIED WITH mysql_native_password BY 'MyPass123';`
      
   Granting Privileges is Important, how to do it?
   
      `GRANT ALL PRIVILEGES ON umami.* TO 'UmamiUser'@'localhost';
       Flush Privileges;`

3. Exiting MySQL

      `QUIT;`
      
## Installing Umami

1. Clone Repository from GitHub.

    `git clone https://github.com/mikecao/umami.git`
    
 2. Change directory to the umami directory.
    
    `cd umami`
 
 3. Install the Needed dependencies.
    Installing NPM:
   
    1. `sudo apt update`
    2. `sudo apt install nodejs npm`
    3. `nodejs --version` -- this should show you the version. 
    4. `curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -`
    5. `sudo apt install nodejs`
    6. `node --version` & `npm --version` -- these will show you the version 
    7. `sudo apt install build-essential`

 4. Configure Umami database, when it's done add the password used for UmamiUser user
 
    `# mysql -u UmamiUser -p umami < sql/schema.mysql.sql`
 
 5. Create an environment file for Umami
    you can use whatever file editor, for me I prefer nano. 
   
    `nano .env`
 
 6. Add the following to your Environment file.
    1. Replace MyPass123 to a the password you sat. 
    2. also replace the HASH_SALT with a unique value of your own. 
    
    `DATABASE_URL=mysql://UmamiUser:MyPass123@localhost:3000/umami
     HASH_SALT=Replace_This_With_A_Unique_Value_OF_Your_Own
     HOSTNAME=127.0.0.1
     PORT=3000`

 7. Close the file after saving it. 
 8. Installing PM2 
 
    `npm install pm2 -g`
  
 9. Launching Umami with PM2. 
 
     `pm2 start npm --name "umami" -- run`
     
 10. Generate the startup Script and save PM2 configuration. 
 
    `pm2 startup
     pm2 save`
 
 ## Installing Caddy as a proxy Server - You can Use Nginx  as an alternative of caddy. 
 
 1. Installing Caddy 
 
    `apt install -y debian-keyring debian-archive-keyring apt-transport-https
     curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo tee /etc/apt/trusted.gpg.d/caddy-stable.asc
     curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
     apt update
     apt install caddy`
  
  2. Editting CaddyFile
  
    `nano /etc/caddy/Caddyfile`
    
  3. Rplacing Contents of your Caddyfile, umami.example.com with your Server's domain name.
   
     `domain.name.com
      reverse_proxy 127.0.0.1:3000 `
      
  4. Save and Exit 
  
  6. Starting Caddy 
  
     ` Caddy Run`
     
  6. Check caddy status. 
  
     `systemctl status caddy`
     
## Testing Umami!! 

in your web browser, Search for the domain name of yourserver with HTTPS.

`https://umami.connect.com`

use these information to login:
username: admin
Password: umami. 


## Thank you!



      
       
       
