## Setting up a host from scratch

This is updated for Debian 12

Note: This guide is assuming the [myonesilaserver.com](https://myonesilaserver.com) host. Don’t forget to make changes to the domains, repo’s and other settings.  This guide also assumes all settings have been configured and is a working, deployable app.

### Create your server:

1. Create the server of the location of choice.
2. Add DNS record so you access it via hostname. Remember DNS can be slow and it can take time until the new record is visible.
3. Setup the server with Debian 12 according to this tutorial.

### Setup dependencies:

1. Setup password-less sudo for sudo users.

```python
# As root:
echo "%sudo ALL=(ALL) NOPASSWD:ALL" | tee -a /etc/sudoers
```

2. Create a user on the remote server, and **add your required keys**

```python
#ssh root@myonesilaserver.com
useradd onesila -m -g sudo -s /bin/bash
su onesila -c ssh-keygen
# Assuming you deployed with digitalocean, and setup the correct
# keys to begin with.
# If not, copy the keys to /home/onesila/.ssh/authorized_keys manually
cp /root/.ssh/authorized_keys /home/onesila/.ssh/
chown onesila -R /home/onesila/.ssh
```

3. Harden ssh by disabling password logins (Optional)

Warning! This settings will stop you from login to the server if you don't have your authorized keys setup correctly.
To verify if your authorized keys are working correctly try to login to the server with the user created above: `ssh onesila@myonesilaserver.com`

Also verify that that you can gain superuser privileges by typing `sudo su`

If all the above working correctly you can follow the instructions bellow:

```python
nano /etc/ssh/sshd_config
# Find the line with "PasswordAuthentication" and set it to:
# PasswordAuthentication no
# Ideally you want to make sure you cannot login root users via ssh
# PermitRootLogin no
/etc/init.d/ssh restart
```

4. Setup your proper hostname

```python
echo myonesilaserver.com | sudo tee /etc/hostname
```

5. Setup some more dependencies:

```python
sudo apt-get install vim htop screen python3-dev git build-essential python3-pip postgresql postgresql-client postgresql-server-dev-all postgresql-contrib nginx supervisor python3-hypercorn python3-virtualenv redis -y
```

6. Setup your certificates with letsencrypt, and generate a dhparam for use later

```python
sudo apt-get install python3-certbot python3-certbot-nginx nginx -y

sudo certbot certonly --agree-tos --nginx --rsa-key-size 4096 --email my@email.com -d myonesilaserver.com

sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 4096
```

7. Create your production db:

### Setup your project and hypercorn runners

```python
sudo su - postgres -c '''psql -c "CREATE DATABASE 'onesila'; "'''
sudo su - postgres -c 'psql -c "CREATE USER onesila WITH PASSWORD '\''NSturyJeLCEJdcGbIvdRmDspQPljvzajqqD'\'';"'
sudo su - postgres -c """psql -c 'GRANT ALL PRIVILEGES ON DATABASE "onesila" to onesila;'"""
sudo su - postgres -c """psql -c 'ALTER DATABASE onesila OWNER TO onesila;'"""
```

8. On the server, in your home-folder clone your repo

```python
cd /home/onesila
git clone git@github.com:OneSila/OneSilaHeadless.git
cd OneSilaHeadless
git checkout master
git pull
cd ..
virtualenv venv
source venv/bin/activate
pip install -r OneSilaHeadless/requirements.txt
```

1. Setup log-folders

```python
sudo mkdir -p /var/log/OneSilaHeadless/
sudo chown onesila:sudo -R /var/log/OneSilaHeadless/
sudo chmod g+ws /var/log/OneSilaHeadless/
```

1. Create a hypercorn_start file `hypercorn_start`. Run: `nano /home/onesila/hypercorn_start`

```python
#!/bin/bash
NAME="OneSilaHeadless"
DJANGODIR=/home/onesila/OneSilaHeadless/OneSila/
HOMEDIR=/home/onesila/
SOCKFILE=/home/onesila/hypercorn.sock
USER=onesila
NUM_WORKERS=1
DJANGO_SETTINGS_MODULE=OneSila.settings
DJANGO_WSGI_MODULE=OneSila.asgi
LOGFILE=/var/log/OneSilaHeadless/hypercorn.log

echo "Starting $NAME as `whoami`"

# Activate the virtual environment
cd $HOMEDIR
source venv/bin/activate
export DJANGO_SETTINGS_MODULE=$DJANGO_SETTINGS_MODULE
export PYTHONPATH=$DJANGODIR:$PYTHONPATH

# Create the run directory if it doesn't exist
RUNDIR=$(dirname $SOCKFILE)
test -d $RUNDIR || mkdir -p $RUNDIR

cd $DJANGODIR
hypercorn  ${DJANGO_WSGI_MODULE}:application \
  --workers $NUM_WORKERS \
  --bind=unix:$SOCKFILE \
  --log-level=debug \
  --log-file=$LOGFILE
```

1. Create a supervisorctl config file `hypercornctl.conf`. Run: `sudo nano /etc/supervisor/conf.d/hypercornctl.conf`

```python
[program:hypercornctl]
command = /home/onesila/hypercorn_start ; Command to start app
user = onesila 
stdout_logfile = /var/log/OneSilaHeadless/hypercornctl.log  ; Where to write log messages
redirect_stderr = true ; Save stderr in the same log
environment=LANG=en_US.UTF-8,LC_ALL=en_US.UTF-8
stopsignal = TERM
stopasgroup = true
```

1. Create a supervisorctl config file for huey `huey.conf`. Run: `sudo nano /etc/supervisor/conf.d/huey.conf`

We use stopsignal = INT for graceful shutdown
```python
[program:huey]
command = /home/onesila/OneSilaHeadless/run_huey.sh ; Command to start app
user = onesila 
stdout_logfile = /var/log/OneSilaHeadless/huey.log  ; Where to write log messages
redirect_stderr = true ; Save stderr in the same log
environment=LANG=en_US.UTF-8,LC_ALL=en_US.UTF-8
stopsignal = INT
stopasgroup = true
stopwaitsecs = 300
```

1. Make your supervisorctl file discoverable, and the hypercorn file executable

```python
sudo chmod +x /home/onesila/hypercorn_start
sudo supervisorctl reread
sudo supervisorctl update
```

### Setup Nginx

1.  Create a nginx config file `onesila`. Run: `sudo nano /etc/nginx/sites-available/onesila`

```
upstream OneSilaHeadless_app_server {
  # fail_timeout=0 means we always retry an upstream even if it failed
  # to return a good HTTP response (in case the Unicorn master nukes a
  # single worker for timing out).

  server unix:/home/onesila/hypercorn.sock fail_timeout=0;
}

server {
    listen 80;
    server_name myonesilaserver.com;
    return 301 https://myonesilaserver.com$request_uri;
}

server {

    listen   443;
    server_name myonesilaserver.com;

    ssl on;
    ssl_certificate /etc/letsencrypt/live/myonesilaserver.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/myonesilaserver.com/privkey.pem;

    ssl_session_timeout  10m;

    # https://raymii.org/s/tutorials/Strong_SSL_Security_On_nginx.html
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers "ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES128-SHA256:DHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:DES-CBC3-SHA:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!MD5:!PSK:!RC4";
    ssl_prefer_server_ciphers on;
    ssl_session_cache shared:SSL:10m;

    ssl_dhparam /etc/ssl/certs/dhparam.pem;

    add_header Strict-Transport-Security max-age=63072000;
    add_header X-Frame-Options DENY;
    add_header X-Content-Type-Options nosniff;

    client_max_body_size 4G;

    access_log /var/log/OneSilaHeadless/nginx-access.log;
    error_log /var/log/OneSilaHeadless/nginx-error.log;

    location /static/ {
        alias   /home/onesila/static/;
    }

    location /media/ {
        alias   /home/onesila/media/;
    }

    location / {
        if (-f /home/onesila/maintenance.flag) {
            return 503;
        }
        # an HTTP header important enough to have its own Wikipedia entry:
        #   http://en.wikipedia.org/wiki/X-Forwarded-For
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

        # enable this if and only if you use HTTPS, this helps Rack
        # set the proper protocol for doing redirects:
        proxy_set_header X-Forwarded-Proto https;

        # pass the Host: header from the client right along so redirects
        # can be set properly within the Rack application
        proxy_set_header Host $http_host;

        # we don't want nginx trying to do something clever with
        # redirects, we set the Host: header above already.
        proxy_redirect off;

        # set "proxy_buffering off" *only* for Rainbows! when doing
        # Comet/long-poll stuff.  It's also safe to set if you're
        # using only serving fast clients with Unicorn + nginx.
        # Otherwise you _want_ nginx to buffer responses to slow
        # clients, really.
        # proxy_buffering off;

        # Try to serve static files from nginx, no point in making an
        # *application* server like Unicorn/Rainbows! serve static files.
        if (!-f $request_filename) {
            proxy_pass http://OneSilaHeadless_app_server;
            break;
        }
        # auth_basic "Restricted";
        # auth_basic_user_file /etc/nginx/.htpasswd;
	  # include /etc/nginx/allowed-countries.conf;
    }

    # Error pages
    # FIXME: Fallback template paths should relly be created
    # error_page 403 404 405 /404.html;
    # location = /404.html {
    #     root /home/onesila/OneSilaHeadless/OneSila/templates/;
    # }
    # error_page 500 501 502 504 /500.html;
    # location = /500.html {
    #     root /home/onesila/OneSilaHeadless/OneSila/templates/;
    # }
    # 
    # error_page 503 /503.html;
    # location = /503.html {
    #     root /home/onesila/OneSilaHeadless/OneSila/templates/;
    # }
}
```

1. Enable your newly created config-file:

```python
sudo ln -s /etc/nginx/sites-available/onesila /etc/nginx/sites-enabled/onesila
```

### Adding the OneSila configuration file

Use the template settings file `local_template.py` to make a `local.py` file.

```commandline
cp /home/onesila/OneSilaHeadless/OneSila/OneSila/settings/local_template.py /home/onesila/OneSilaHeadless/OneSila/OneSila/settings/local.py
```

Then we can:

```commandline
nano /home/onesila/OneSilaHeadless/OneSila/OneSila/settings/local.py
```

Edit the file and adjust at a minimumm  ALLOWED_HOST, DATABASE and SECRET_KEY.
Use the database settings you used earliers.

Now we can finally run the services:
```
sudo supervisorctl start hypercornctl
sudo supervisorctl start huey
```

and run migrations

```
source /home/onesila/venv/bin/activate
cd /home/onesila/OneSilaHeadless/OneSila
./manage.py migrate
./manage.py collectstatic
```

1. Restart nginx:  `sudo /etc/init.d/nginx restart`

If all was setup correctly, you should now be able to access your app via https://myonesilaserver.com/


# @FIXME Show the actual changes

## Auto deployment:

### Add your deployment keys to bitbucket of github

```python
cat /home/onesila/.ssh/id_rsa.pub
```

### Prepping the variables in your fork.

First of all, in order to auto-deploy we will need a new pair of SSH keys. You can generate them by running `ssh-keygen -t rsa` and specifying a new folder.  You'll need the later.

Next, you can specify both your master and development servers by creating the secrets in github.

DEVELOPMENT_HOSTNAME = dev.myonesilaserver.com
DEVELOPMENT_USERNAME = onesila
DEVELOPMENT_SECRET_KEY_SSH = {the contents of your new rsa private key.}


MASTER_HOSTNAME = myonesilaserver.com
MASTER_USERNAME = onesila

You can specify these under your repository settings where you can find `secrets and variables`.


### Adding your authorized keys

You want to add your new public key to your authorized keys as well on the server.

### Docker

A docker image needs to be created, and the config + steps how to do it should be listed here.