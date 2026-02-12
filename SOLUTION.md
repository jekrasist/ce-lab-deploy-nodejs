# Lab Solution
Last login: Thu Feb 12 12:44:07 on ttys002
ahmeterdogan@Ahmets-MacBook-Pro ~ % 
curl -sL https://rpm.nodesource.com/setup_18.x | sudo bash -
sudo yum install -y nodejs
Password:
2026-02-12 16:20:32 - Error: This script is intended for RPM-based systems. Please run it on an RPM-based system. (Exit Code: 1)
sudo: yum: command not found
ahmeterdogan@Ahmets-MacBook-Pro ~ % 1
zsh: command not found: 1
ahmeterdogan@Ahmets-MacBook-Pro ~ % // app.js
zsh: permission denied: //
ahmeterdogan@Ahmets-MacBook-Pro ~ % # Download and install nvm:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# in lieu of restarting the shell
\. "$HOME/.nvm/nvm.sh"

# Download and install Node.js:
nvm install 24

# Verify the Node.js version:
node -v # Should print "v24.13.1".

# Verify npm version:
npm -v # Should print "11.8.0".

zsh: command not found: #
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 16631  100 16631    0     0  46922      0 --:--:-- --:--:-- --:--:-- 46847
You may be on a Mac, and need to install the Xcode Command Line Developer Tools.
If so, run `xcode-select --install` and try again. If not, please report this!
zsh: command not found: #
.: no such file or directory: /Users/ahmeterdogan/.nvm/nvm.sh
zsh: command not found: #
zsh: command not found: nvm
zsh: command not found: #
zsh: command not found: node
zsh: command not found: #
zsh: command not found: npm
ahmeterdogan@Ahmets-MacBook-Pro ~ % // app.js
const express = require('express');
const app = express();
const port = process.env.PORT || 8080;

app.get('/', (req, res) => {
  res.json({
    message: 'Week 2 Deployment Lab',
    hostname: process.env.HOSTNAME,
    uptime: process.uptime(),
    environment: process.env.NODE_ENV || 'development'
  });
});

app.get('/health', (req, res) => {
  res.json({ status: 'healthy', timestamp: new Date() });
});

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
zsh: parse error near `}'
ahmeterdogan@Ahmets-MacBook-Pro ~ % // app.js
const express = require('express');
const app = express();
const port = process.env.PORT || 8080;

app.get('/', (req, res) => {
  res.json({
    message: 'Week 2 Deployment Lab',
    hostname: process.env.HOSTNAME,
    uptime: process.uptime(),
    environment: process.env.NODE_ENV || 'development'
  });
});
zsh: parse error near `}'
ahmeterdogan@Ahmets-MacBook-Pro ~ % ssh -i bootcamp-week2-key.pem ec2-user@100.28.222.217
Warning: Identity file bootcamp-week2-key.pem not accessible: No such file or directory.
ec2-user@100.28.222.217: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
ahmeterdogan@Ahmets-MacBook-Pro ~ % ssh -i bootcamp-week2-key.pem ec2-user@172.31.67.153 
Warning: Identity file bootcamp-week2-key.pem not accessible: No such file or directory.
ssh: connect to host 172.31.67.153 port 22: Operation timed out
ahmeterdogan@Ahmets-MacBook-Pro ~ % mkdir ~/app && cd ~/app
ahmeterdogan@Ahmets-MacBook-Pro app % npm init -y
Wrote to /Users/ahmeterdogan/app/package.json:

{
  "name": "app",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "type": "commonjs"
}


ahmeterdogan@Ahmets-MacBook-Pro app % mkdir ~/app && cd ~/app
npm init -y
npm install express
mkdir: /Users/ahmeterdogan/app: File exists
Wrote to /Users/ahmeterdogan/app/package.json:

{
  "name": "app",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "type": "commonjs"
}



added 65 packages, and audited 66 packages in 3s

22 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ahmeterdogan@Ahmets-MacBook-Pro app % sudo npm install -g pm2
Password:

added 133 packages in 6s

13 packages are looking for funding
  run `npm fund` for details
ahmeterdogan@Ahmets-MacBook-Pro app % pm2 start app.js --name myapp

                        -------------

__/\\\\\\\\\\\\\____/\\\\____________/\\\\____/\\\\\\\\\_____
 _\/\\\/////////\\\_\/\\\\\\________/\\\\\\__/\\\///////\\\___
  _\/\\\_______\/\\\_\/\\\//\\\____/\\\//\\\_\///______\//\\\__
   _\/\\\\\\\\\\\\\/__\/\\\\///\\\/\\\/_\/\\\___________/\\\/___
    _\/\\\/////////____\/\\\__\///\\\/___\/\\\________/\\\//_____
     _\/\\\_____________\/\\\____\///_____\/\\\_____/\\\//________
      _\/\\\_____________\/\\\_____________\/\\\___/\\\/___________
       _\/\\\_____________\/\\\_____________\/\\\__/\\\\\\\\\\\\\\\_
        _\///______________\///______________\///__\///////////////__


                          Runtime Edition

        PM2 is a Production Process Manager for Node.js applications
                     with a built-in Load Balancer.

                Start and Daemonize any application:
                $ pm2 start app.js

                Load Balance 4 instances of api.js:
                $ pm2 start api.js -i 4

                Monitor in production:
                $ pm2 monitor

                Make pm2 auto-boot at server restart:
                $ pm2 startup

                To go further checkout:
                http://pm2.io/


                        -------------

[PM2] Spawning PM2 daemon with pm2_home=/Users/ahmeterdogan/.pm2
[PM2] PM2 Successfully daemonized
[PM2][ERROR] Script not found: /Users/ahmeterdogan/app/app.js
ahmeterdogan@Ahmets-MacBook-Pro app % pm2 save
[PM2] Saving current process list...
[PM2][WARN] PM2 is not managing any process, skipping save...
[PM2][WARN] To force saving use: pm2 save --force
ahmeterdogan@Ahmets-MacBook-Pro app % sudo yum install -y nginx
sudo tee /etc/nginx/conf.d/app.conf <<EOF
server {
    listen 80;
    location / {
        proxy_pass http://localhost:8080;
        proxy_http_version 1.1;
        proxy_set_header Host \$host;
    }
}
heredoc> 
heredoc> 
heredoc> sudo systemctl start nginx
heredoc> 
ahmeterdogan@Ahmets-MacBook-Pro app % pm2 start app.js --name myapp
[PM2][ERROR] Script not found: /Users/ahmeterdogan/app/app.js
ahmeterdogan@Ahmets-MacBook-Pro app % sudo npm install -g pm2

changed 133 packages in 634ms

13 packages are looking for funding
  run `npm fund` for details
ahmeterdogan@Ahmets-MacBook-Pro app % pm2 start app.js --name myapp

[PM2][ERROR] Script not found: /Users/ahmeterdogan/app/app.js
ahmeterdogan@Ahmets-MacBook-Pro app % pm2 start app.js --name app  
[PM2][ERROR] Script not found: /Users/ahmeterdogan/app/app.js
ahmeterdogan@Ahmets-MacBook-Pro app % nano app.js
ahmeterdogan@Ahmets-MacBook-Pro app % cd ~/Downloads 
ahmeterdogan@Ahmets-MacBook-Pro Downloads % chmod 400 bootcamp-week2-key.pem
ahmeterdogan@Ahmets-MacBook-Pro Downloads % ssh -i "bootcamp-week2-key.pem" ec2@100.28.222.217
ec2@100.28.222.217: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
ahmeterdogan@Ahmets-MacBook-Pro Downloads % ssh -i "bootcamp-week2-key.pem" ec2-user@100.28.222.217
   ,     #_
   ~\_  ####_        Amazon Linux 2023
  ~~  \_#####\
  ~~     \###|
  ~~       \#/ ___   https://aws.amazon.com/linux/amazon-linux-2023
   ~~       V~' '->
    ~~~         /
      ~~._.   _/
         _/ _/
       _/m/'
Last login: Wed Feb 11 16:15:49 2026 from 46.196.81.56
[ec2-user@ip-172-31-67-153 ~]$ sudo yum install -y nginx
sudo tee /etc/nginx/conf.d/app.conf <<EOF
server {
    listen 80;
    location / {
        proxy_pass http://localhost:8080;
        proxy_http_version 1.1;
        proxy_set_header Host \$host;
    }
}
Amazon Linux 2023 Kernel Livepatch repository                                           245 kB/s |  31 kB     00:00    
Dependencies resolved.
========================================================================================================================
 Package                         Architecture       Version                               Repository               Size
========================================================================================================================
Installing:
 nginx                           x86_64             1:1.28.1-1.amzn2023.0.1               amazonlinux              33 k
Installing dependencies:
 generic-logos-httpd             noarch             18.0.0-12.amzn2023.0.3                amazonlinux              19 k
 gperftools-libs                 x86_64             2.9.1-1.amzn2023.0.3                  amazonlinux             308 k
 libunwind                       x86_64             1.4.0-5.amzn2023.0.3                  amazonlinux              66 k
 nginx-core                      x86_64             1:1.28.1-1.amzn2023.0.1               amazonlinux             687 k
 nginx-filesystem                noarch             1:1.28.1-1.amzn2023.0.1               amazonlinux             9.6 k
 nginx-mimetypes                 noarch             2.1.49-3.amzn2023.0.3                 amazonlinux              21 k

Transaction Summary
========================================================================================================================
Install  7 Packages

Total download size: 1.1 M
Installed size: 3.7 M
Downloading Packages:
(1/7): libunwind-1.4.0-5.amzn2023.0.3.x86_64.rpm                                        1.6 MB/s |  66 kB     00:00    
(2/7): generic-logos-httpd-18.0.0-12.amzn2023.0.3.noarch.rpm                            428 kB/s |  19 kB     00:00    
(3/7): gperftools-libs-2.9.1-1.amzn2023.0.3.x86_64.rpm                                  6.1 MB/s | 308 kB     00:00    
(4/7): nginx-1.28.1-1.amzn2023.0.1.x86_64.rpm                                           1.4 MB/s |  33 kB     00:00    
(5/7): nginx-filesystem-1.28.1-1.amzn2023.0.1.noarch.rpm                                360 kB/s | 9.6 kB     00:00    
(6/7): nginx-core-1.28.1-1.amzn2023.0.1.x86_64.rpm                                       18 MB/s | 687 kB     00:00    
(7/7): nginx-mimetypes-2.1.49-3.amzn2023.0.3.noarch.rpm                                 877 kB/s |  21 kB     00:00    
------------------------------------------------------------------------------------------------------------------------
Total                                                                                   8.3 MB/s | 1.1 MB     00:00     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                1/1 
  Running scriptlet: nginx-filesystem-1:1.28.1-1.amzn2023.0.1.noarch                                                1/7 
  Installing       : nginx-filesystem-1:1.28.1-1.amzn2023.0.1.noarch                                                1/7 
  Installing       : nginx-mimetypes-2.1.49-3.amzn2023.0.3.noarch                                                   2/7 
  Installing       : libunwind-1.4.0-5.amzn2023.0.3.x86_64                                                          3/7 
  Installing       : gperftools-libs-2.9.1-1.amzn2023.0.3.x86_64                                                    4/7 
  Installing       : nginx-core-1:1.28.1-1.amzn2023.0.1.x86_64                                                      5/7 
  Installing       : generic-logos-httpd-18.0.0-12.amzn2023.0.3.noarch                                              6/7 
  Installing       : nginx-1:1.28.1-1.amzn2023.0.1.x86_64                                                           7/7 
  Running scriptlet: nginx-1:1.28.1-1.amzn2023.0.1.x86_64                                                           7/7 
  Verifying        : generic-logos-httpd-18.0.0-12.amzn2023.0.3.noarch                                              1/7 
  Verifying        : gperftools-libs-2.9.1-1.amzn2023.0.3.x86_64                                                    2/7 
  Verifying        : libunwind-1.4.0-5.amzn2023.0.3.x86_64                                                          3/7 
  Verifying        : nginx-1:1.28.1-1.amzn2023.0.1.x86_64                                                           4/7 
  Verifying        : nginx-core-1:1.28.1-1.amzn2023.0.1.x86_64                                                      5/7 
  Verifying        : nginx-filesystem-1:1.28.1-1.amzn2023.0.1.noarch                                                6/7 
  Verifying        : nginx-mimetypes-2.1.49-3.amzn2023.0.3.noarch                                                   7/7 

Installed:
  generic-logos-httpd-18.0.0-12.amzn2023.0.3.noarch           gperftools-libs-2.9.1-1.amzn2023.0.3.x86_64              
  libunwind-1.4.0-5.amzn2023.0.3.x86_64                       nginx-1:1.28.1-1.amzn2023.0.1.x86_64                     
  nginx-core-1:1.28.1-1.amzn2023.0.1.x86_64                   nginx-filesystem-1:1.28.1-1.amzn2023.0.1.noarch          
  nginx-mimetypes-2.1.49-3.amzn2023.0.3.noarch               

Complete!
> EOF
server {
    listen 80;
    location / {
        proxy_pass http://localhost:8080;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
    }
}
[ec2-user@ip-172-31-67-153 ~]$ sudo systemctl start nginx
[ec2-user@ip-172-31-67-153 ~]$ sudo systemctl enable nginx
Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service → /usr/lib/systemd/system/nginx.service.
[ec2-user@ip-172-31-67-153 ~]$ 
