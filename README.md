### Задание 1. Elasticsearch 

Установите и запустите Elasticsearch, после чего поменяйте параметр cluster_name на случайный. 

*Приведите скриншот команды 'curl -X GET 'localhost:9200/_cluster/health?pretty', сделанной на сервере с установленным Elasticsearch. Где будет виден нестандартный cluster_name*.


apt update && apt install gnupg apt-transport-https

wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add

echo "deb [trusted=yes] https://mirror.yandex.ru/mirrors/elastic/7/ stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list

apt update && apt install elasticsearch

systemctl daemon-reload

systemctl enable elasticsearch.service

Изменим cluster_name в /etc/elasticsearch/elasticsearch.yml на netology_cluster

systemctl start elasticsearch.service

curl -X GET 'localhost:9200/_cluster/health?pretty


![1](https://github.com/BOSe1337/ELK/blob/main/1-1.JPG)



### Задание 2. Kibana

Установите и запустите Kibana.

*Приведите скриншот интерфейса Kibana на странице http://<ip вашего сервера>:5601/app/dev_tools#/console, где будет выполнен запрос GET /_cluster/health?pretty*.



apt install kibana
systemctl daemon-reload
systemctl enable kibana.service
systemctl start kibana.service

systemctl status kibana.service


nano /etc/kibana/kibana.yml

server.port: 5601
server.host: "0.0.0.0"

systemctl restart kibana.service


![2](https://github.com/BOSe1337/ELK/blob/main/2-2.JPG)



