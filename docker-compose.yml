version: '2.2'

networks:
     laboi-network:
       driver: bridge

services:

  haproxy:
    restart: always
    mem_limit: 128m
    image: dockercloud/haproxy
    networks:
      - laboi-network
    ports:
      - 8888:80
      - 1937:1936
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - DEBUG=yes
      - MAXCONN=20000
      - BALANCE=roundrobin
      - MODE=tcp
      - OPTION=tcplog
      - EXCLUDE_PORTS=443
    links:
      - wordpress

  mysqlwp:
    image: 'mysql:latest'
    restart: always
    networks:
      - laboi-network
    mem_limit: 2g
    mem_reservation: 1g
    environment:
      - MYSQL_ROOT_PASSWORD=senha
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=senhawp
    volumes:
      - /devops/laboi/containers/mysql/logs:/var/log/mysql
      - /devops/laboi/containers/mysql/data:/var/lib/mysql

  wordpress:
    image: 'wordpress:latest'
    restart: always
    networks:
      - laboi-network
    mem_limit: 2g
    mem_reservation: 1g
    ports:
      - 80
    environment:
      - WORDPRESS_DB_HOST=mysqlwp
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=senhawp
      - WORDPRESS_DB_NAME=wordpress
    links:
      - mysqlwp
    depends_on:
      - mysqlwp
    volumes:
      - /devops/laboi/containers/wordpress:/var/www/html
