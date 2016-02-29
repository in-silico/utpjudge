# utpjudge


WARNING: Work in progress.

Online judge for programming contest

### Clone

    git clone --recursive git@github.com:in-silico/utpjudge.git


Set-up judge behind reverse proxy
==================================

- Install nginx

        aptitude update
        aptitude install nginx

- Add basic dns configuration at '/etc/hosts'

        127.0.1.1	judge.is
        127.0.1.1	api.judge.is


- Add basic configuration for nginx at '/etc/nginx/sites-available/default'

```
server {
  listen 80;

  server_name judge.is;

  location / {
    proxy_pass http://localhost:8081;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
  }
}


server {
  listen 80;

  server_name api.judge.is;

  location / {
    proxy_pass http://localhost:8080;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
  }
}

```

Get API keys from github
========================

In order to authenticate users with github you'll need to get your own keys from github.com

Register you app here https://github.com/settings/applications/new and then copy
your private/public key into the config/oauth file.

*NOTE:* I strongly recommend you to use the following command to avoid sharing your keys:

        git update-index --assume-unchanged config/oauth.js


-------
<a href="//github.com/in-silico" target="_blank"><p align="center"><img src="https://cloud.githubusercontent.com/assets/14989202/11768037/94347c26-a18e-11e5-84ad-a8554c9fe75d.png" width=110px></img></p></a>

<p align="center">Developed by In-silico.</p>
