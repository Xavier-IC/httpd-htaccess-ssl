# httpd-htaccess-ssl

Apache httpd with SSL and .htaccess files support enabled.


## Docker run

    docker run -d --name my-apache-app -p=hostport:443 -v /path/to/your/files:/usr/local/apache2/htdocs/ -v /path/to/passwd/:/usr/local/apache2/passwd/ -v /path/to/server.crt:/usr/local/apache2/conf/server.crt -v /path/to/server.key:/usr/local/apache2/conf/server.key httpd-htaccess-ssl:2.4

Where:
* `hostport` - port on host machine
* `/path/to/your/files` - data root directory
* `/path/to/passwd` - passwd directory, see below
* `/path/to/server.crt`, `/path/to/server.key` - SSL keys

## Passwords
You can restrict directory access by putting a `.htaccess` file in it. For example, to only allow user `myusername` access a directory, create the following `.htaccess` file in there:

    AuthType Basic
    AuthName "Restricted Files"
    AuthBasicProvider file
    AuthUserFile /usr/local/apache2/passwd/passwords
    Require user myusername

Create a passwords file in the passwd directory:

    docker exec -it my-apache-app bash

    bin/htpasswd -c passwd/passwords myusername
