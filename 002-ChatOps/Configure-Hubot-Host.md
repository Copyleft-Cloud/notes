# Configure Hubot Host (DigitalOcean Droplet)


FIREWALL
```
root@hubot:/var/log# ufw default deny incoming
Default incoming policy changed to 'deny'
(be sure to update your rules accordingly)

root@hubot:/var/log# ufw default allow outgoing
Default outgoing policy changed to 'allow'
(be sure to update your rules accordingly)

root@hubot:/var/log# ufw allow ssh
Rules updated
Rules updated (v6)

root@hubot:/var/log# ufw allow http
Rules updated
Rules updated (v6)

root@hubot:/var/log# ufw allow https
Rules updated
Rules updated (v6)

root@hubot:/var/log# ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup

root@hubot:/var/log# ufw status verbose
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22                         ALLOW IN    Anywhere
80                         ALLOW IN    Anywhere
443                        ALLOW IN    Anywhere
22 (v6)                    ALLOW IN    Anywhere (v6)
80 (v6)                    ALLOW IN    Anywhere (v6)
443 (v6)                   ALLOW IN    Anywhere (v6)
```

Install Node.js and Node Package Manager ( https://nodejs.org )
Install PM2 ( http://pm2.keymetrics.io/ )

Node.js is available from the NodeSource Debian and Ubuntu binary distributions repository.

Install Nodejs and Node Package Manager (npm)
```
root@hubot:~# apt-get update
root@hubot:~# curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
root@hubot:~# apt-get -y install nodejs

```

Verify nodejs and npm Installed Versions
```
root@hubot:~# node -v
v7.4.0

root@hubot:~# npm -v
4.0.5
```

Install PM2 Process Manager for Node.js
```
npm install -g pm2
```


Start our Application using PM2
```
pm2 start <application>.js
```

Other PM2 Commands...
```
pm2 list
pm2 stop
pm2 restart
pm2 delete
```
