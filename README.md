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


![1] (https://github.com/BOSe1337/ELK/blob/main/1-1.JPG)


