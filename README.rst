Python Flask Project
======
see `Tutorial <https://www.youtube.com/playlist?list=PL-osiE80TeTs4UjLw5MM6OjgkjFeUxCYH/>`_


DB changes
-------

    $ from app import create_app, db
    $ app = create_app()
    $ ctx = app.app_context()
    $ ctx.push()
    $ db.create_all()
    $ ctx.pop()
    $ exit()


Setup linux server
-------

    $ apt update && apt upgrade
    $ hostname set-hostname <hostname>
    $ nano /etc/hosts

    $ <public ip>   <hostname>

    $ adduser <username>
    $ adduser <username> sudo

    $ sudo apt install ufw
    $ sudo ufw default allow outgoing
    $ sudo ufw default deny incoming
    $ sudo ufw allow ssh
    $ sudo ufw allow <port>
    $ sudo ufw enable

Enable other relevant ports, or let Azure handle everything

Setup webserver
-------

    $ sudo rm /etc/nginx/sites-enabled/default
    $ sudo nano /etc/nginx/sites-enabled/<config-file name>

    Feks:
        server {
            listen 80;
            server_name 137.135.204.200;

            location /static {
                alias /home/performanceadmin/flask_project/app/static;
            }

            location / {
                proxy_pass http://localhost:8000;
                include /etc/nginx/proxy_params;
                proxy_redirect off;
            }
        }

    $ sudo systemctl restart ngninx
    $ gunicorn -w 3 run:app


Setup supervisor
-------

    $ sudo apt-install supervisor
    $ sudo nano /etc/supervisor/conf.d/flaskapp.conf


    Feks:
    [program:flaskapp]
    directory=/home/performanceadmin/flask_project
    command=/home/performanceadmin/flask_project/venv/bin/gunicorn -w 5 run:app
    user=performanceadmin
    autostart=true
    autorestart=true
    stopasgroup=true
    killasgroup=true
    stderr_logfile=/var/log/flaskapp/flaskapp.err.log
    stdout_logfile=/var/log/flaskapp/flaskapp.out.log

    $ sudo mkdir -p /var/log/flaskapp
    $ sudo touch /var/log/flaskblog/flaskapp.err.log
    $ sudo touch /var/log/flaskblog/flaskapp.out.log
    $ sudo supervisorctl reload

Credits:
-------

CoreyMS

https://youtube.com/watch?v=goToXTC96Co&list=PL-osiE80TeTs4UjLw5MM6OjgkjFeUxCYH&index=13
