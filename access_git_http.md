### Configuration to access your GIT server from outside through HTTP.

Assuming we already have GIT and Apache2 installed.

Install require module `git-http-backend`

> apt install git-http-backend


Put files and projects in `/var/www/git/`. Projects in here should end with `.git` extension
If we intend to put here only public project (just to share), we need to create bare projetcs here

> git init --bare myproject.git

Otherwise if it's a real, development project ignore the bare option. Since it's visible by everyone, we need to configure user/password later.


Edit apache conf to add a virtual host

> nano /etc/apache2/sites-available/000-default.conf

    <VirtualHost *:888>
        DocumentRoot /var/www/git

        <Directory "/var/www/git">
        Allow from All
        Options +ExecCGI
        AllowOverride All
        </Directory>

        SetEnv GIT_HTTP_EXPORT_ALL
        SetEnv GIT_PROJECT_ROOT /var/www/git
        ScriptAlias /git /usr/lib/git-core/git-http-backend

        <Location /git>
          AuthType Basic
          AuthName "Private Git Access"
          AuthUserFile /opt/git/.htpasswd
          Require valid-user
        </Location>
    </VirtualHost>

Here I used port 888 because I already used port 80 for my web server. Leave it port 80 for git server or choose any port you like.

Tell apache to listen to port 888 :

> nano /etc/apache2/ports.conf

    Listen 888

We configure to make apache read authentification info from the file `/opt/git/.htpasswd`. We need to generate this file  `htpasswd -c [any_location] [username]`

> htpasswd -c /opt/git/.htpasswd myid


That's all. Now any application can checkout from this url `http://[your_IP]/git/myproject.git`

The `/git` is kinda required. You cannot put in the root www folder.
