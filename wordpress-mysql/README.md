# docker-compose

Build Wordpress with Mysql service
```
version: '3.8'

services: 
    db:
        image: mysql:5.7
        container_name: mysql_database
        volumes: 
            - db_data:/var/lib/mysql/
        restart: always
        
        environment: 
            MYSQL_ROOT_PASSWORD: word@press
            MYSQL_DATABASE: wordpress
            MYSQL_USER: wordpress
            MYSQL_PASSWORD: abc@123
    
    wordpress:
        depends_on: 
            - db
        image: wordpress:latest
        container_name: wp_frontend
        volumes: 
            - wordpress_files:/var/www/html
        
        ports: 
            - "8000:80"
        
        restart: always
        
        environment: 
            WORDPRESS_DB_HOST: db:3306
            WORDPRESS_DB_USER: wordpress
            WORDPRESS_DB_PASSWORD: abc@123

volumes: 
    wordpress_files:
    db_data:

```
# Run Mysql command to link mysqldatabase container with mysql

```
docker run -it --link mysql_database:mysql --rm mysql sh -c 'exec mysql -h "$MYSQL_PORT_TCP_ADDRESS" -u root -p"$MYSQL_ENV_MYSQL_ROOT_PASSWORD"'
```
or 
```
docker run -it --link mysql_database:mysql --rm mysql sh -c 'exec mysql -h "$MYSQL_PORT_TCP_ADDRESS" -P"$MYSQL_PORT_3306_TCP_PORT" -uroot -p"$MYSQL_ENV_MYSQL_ROOT_PASSWORD"'
```
