Simple docker environment for your local projects.
-------------------

**Which components it containing**

Nginx, PHP7.2+XDebug, Elasticsearch, MySQL, Redis, Node

**How to start**

1. You have to have docker and docker-compose on your local machine.
2. Clone this project into your work directory.
3. Make `docker-compose up --build -d` for build the containers.
3. Make `docker-compose up php-cli /bin/bash` for get into anyone container (just change some container name instead `php-cli`).
4. Enjoy your server `http://localhost:8080/` you can change port in `docker-compose.yml`, 
    also you can make alias in tour hosts file for another domain, 
    put your make files into `/public` directory.

**How use Xdebug in PhpStorm**

1. After building your containers go to File > Settings > Languages & Frameworks > PHP
    and chose your php-cli container as CLI Interpreter, if there is not it - create new 
    interpreter and chose it from Docker machine.
2. Change port Debug port in File > Settings > Languages & Frameworks > PHP > Debug to 9003 
    (you can change another port in `docker-compose.yml`)
3. Go to File > Settings > Languages & Frameworks > PHP > Servers
    and create new server call it as `docker` enter Host as `localhost`, choose checkbox `Use path mappings`
    and enter root path `/var/www`. 
4. That's all, take brake points and fpm and cli will be work with it

**SSL and HTTPS**

if You want to use https instead http you have to do a few simple steps.
1. Change param `listen 80;` as `listen 443 ssl` in `docker/nginx/default.conf`.
2. Add a few parameters into server{} body of file `docker/nginx/default.conf`:
    ```
    #ssl off;
    #ssl_certificate /etc/nginx/ssl/ssl-cert-snakeoil.pem;
    #ssl_certificate_key /etc/nginx/ssl/ssl-cert-snakeoil.key;
    ```
3. Change port in `docker-compose.yml` where nginx section from 80 to 443.
