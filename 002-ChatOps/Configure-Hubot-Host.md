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

WebHooks
https://developer.github.com/webhooks/

Install apache2
Install Ruby and Sinatra
Install Node.js and Node Package Manager
Install PM2

http://www.sinatrarb.com/
https://github.com/sinatra/sinatra
https://nodejs.org
http://pm2.keymetrics.io/
```
apt install -y apache2
apt install -y ruby


ruby -v
ruby 2.3.1p112 (2016-04-26) [x86_64-linux-gnu]
gem list
gem install sinatra
```

```
cd /opt
mkdir webhooks
vi webhooks.rb

# webhooks.rb
require 'sinatra'

get '/' do
  'Copyleft Cloud Webhook for Hubot'
end

get '/deploy' do
  'Deploy Webhook'
end
```

```
# config.ru
require './webhooks'
run Webhooks
```

```
root@hubot:/opt/webhooks# rackup
[2017-01-10 11:36:07] INFO  WEBrick 1.3.1
[2017-01-10 11:36:07] INFO  ruby 2.3.1 (2016-04-26) [x86_64-linux-gnu]
[2017-01-10 11:36:07] INFO  WEBrick::HTTPServer#start: pid=16489 port=9292
127.0.0.1 - - [10/Jan/2017:11:36:59 +0000] "GET / HTTP/1.1" 200 13 0.0153
127.0.0.1 - - [10/Jan/2017:11:37:07 +0000] "GET /deploy HTTP/1.1" 200 14 0.0008
```


root@hubot:/var/log# curl 127.0.0.1:9292/
Hello, world!

root@hubot:/var/log# curl 127.0.0.1:9292/deploy
Deploy Webhook

RUN APPLICATION
```
root@hubot:/opt/webhooks# ruby webhooks.rb
[2017-01-10 11:24:29] INFO  WEBrick 1.3.1
[2017-01-10 11:24:29] INFO  ruby 2.3.1 (2016-04-26) [x86_64-linux-gnu]
== Sinatra (v1.4.7) has taken the stage on 4567 for development with backup from WEBrick
[2017-01-10 11:24:29] INFO  WEBrick::HTTPServer#start: pid=16389 port=4567
```

VERIFY PORT
```
root@hubot:~# netstat -tulpn
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1629/sshd
tcp        0      0 127.0.0.1:4567          0.0.0.0:*               LISTEN      16462/ruby
tcp6       0      0 :::22                   :::*                    LISTEN      1629/sshd
```

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
