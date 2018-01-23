//Wordpress e mysql via Docker compose.
docker compose up 
docker-compose up --scale wordpress=2 -d //Scalar a aplicação

//Netdata
docker run -d --cap-add SYS_PTRACE -v /proc:/host/proc:ro -v /sys:/host/sys:ro -p 19999:19999 titpetric/netdata 

//Kibana+Elasticsearch
docker run --name some-kibana -e ELASTICSEARCH_URL=http://some-elasticsearch:9200 -p 5601:5601 -d kibana 

//Rancher Server
docker swarm init --advertise-addr ip
sudo docker run -d --restart=unless-stopped -p 7070:8080 rancher/server

