//Wordpress e Mysql via Docker compose.<br>
docker compose up  <br>
docker-compose up --scale wordpress=2 -d //Scalar a aplicação

//Netdata <br>
docker run -d --cap-add SYS_PTRACE -v /proc:/host/proc:ro -v /sys:/host/sys:ro -p 19999:19999 titpetric/netdata 

//Kibana+Elasticsearch <br>
docker run --name some-kibana -e ELASTICSEARCH_URL=http://some-elasticsearch:9200 -p 5601:5601 -d kibana  <br>

//Rancher Server <br> 
docker swarm init --advertise-addr ip <br>
sudo docker run -d --restart=unless-stopped -p 7070:8080 rancher/server

