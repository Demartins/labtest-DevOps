# Monitoring Tools Dockers  <br>


## Rancher Server <br> 
docker swarm init --advertise-addr [your ip]  <br>
sudo docker run -d --restart=unless-stopped -p 7070:8080 rancher/server

## Netdata <br>
docker run -d --cap-add SYS_PTRACE -v /proc:/host/proc:ro -v /sys:/host/sys:ro -p 19999:19999 titpetric/netdata 


## cAdvisor [Google]

docker run -d --name=cadvisor -p 8080:8080 --volume=/var/run:/var/run:rw --volume=/sys:/sys:ro --volume=/var/lib/docker/:/var/lib/docker:ro google/cadvisor:latest

## Kibana+Elasticsearch <br>
docker run --name some-kibana -e ELASTICSEARCH_URL=http://some-elasticsearch:9200 -p 5601:5601 -d kibana  <br>


## Zabbix 

//BD MariaDB 
docker run \ <br>
   -d \ 
   --name dockbix-db \
   -v /etc/localtime:/etc/localtime:ro \
   --env="MARIADB_USER=zabbix" \
   --env="MARIADB_PASS=my_password" \
   monitoringartist/zabbix-db-mariadb

## Zabbix Port 80, Server Port 10051
docker run \
   -d \
   --name dockbix \
   -p 80:80 \
   -p 10051:10051 \
   -v /etc/localtime:/etc/localtime:ro \
   --link dockbix-db:dockbix.db \
   --env="ZS_DBHost=dockbix.db" \
   --env="ZS_DBUser=zabbix" \
   --env="ZS_DBPassword=my_password" \
   --env="XXL_zapix=true" \
   --env="XXL_grapher=true" \
   monitoringartist/dockbix-xxl:latest

//login = "admin"  Password = "zabbix"

## Agent for Zabbix
docker run \
  --name=dockbix-agent-xxl \
  --net=host \
  --privileged \
  -v /:/rootfs \
  -v /var/run:/var/run \
  --restart unless-stopped \
  -e "ZA_Server=<ZABBIX SERVER IP/DNS NAME/IP_RANGE>" \
  -e "ZA_ServerActive=<ZABBIX SERVER IP/DNS NAME>" \
  -d monitoringartist/dockbix-agent-xxl-limited:latest

## Grafana 
//create /var/lib/grafana as persistent volume storage <br>
docker run -d -v /var/lib/grafana --name grafana-xxl-storage busybox:latest

## start grafana-xxl
docker run \
  -d \
  -p 3000:3000 \
  --name grafana-xxl \
  --volumes-from grafana-xxl-storage \
  monitoringartist/grafana-xxl:latest 

//Login ="admin" and Password ="admin" 

## Portainer 
 docker run  -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer
 
 ## Scale Docker
 Comando Scale Docker: \
 docker-compose -p labtestdocker -f ./docker-compose.yml up --scale wordpress=2 -d


