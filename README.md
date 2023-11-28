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
server.host: "10.22.97.56"

systemctl restart kibana.service


![2](https://github.com/BOSe1337/ELK/blob/main/2-2.JPG)


### Задание 3. Logstash

Установите и запустите Logstash и Nginx. С помощью Logstash отправьте access-лог Nginx в Elasticsearch. 

*Приведите скриншот интерфейса Kibana, на котором видны логи Nginx.*


apt install logstash
systemctl daemon-reload
systemctl enable logstash.service
systemctl start logstash.service

systemctl status logstash.service

nano /etc/logstash/conf.d/nginx_logstash.conf 

будет передавать логи из Nginx в Elasticsearch:


input {
  file {
    path => "/var/log/nginx/access.log"
    type => "nginx"
    start_position => "beginning"
  }
}

output {
  elasticsearch {
    hosts => ["localhost:9200"]
    data_stream => "true"
  }
}

![3](https://github.com/BOSe1337/ELK/blob/main/3-3.jpg)

### Задание 4. Filebeat. 

Установите и запустите Filebeat. Переключите поставку логов Nginx с Logstash на Filebeat. 

*Приведите скриншот интерфейса Kibana, на котором видны логи Nginx, которые были отправлены через Filebeat.*

apt install filebeat
systemctl daemon-reload
systemctl enable filebeat.service
systemctl start filebeat.service


systemctl status filebeat.service


![4](https://github.com/BOSe1337/ELK/blob/main/4-4.jpg)


nano /etc/logstash/conf.d/nginx_logstash.cput {
  beats {
    port => 5044
  }
}

nano /etc/filebeat/filebeat.yml


filebeat.inputs:
 type: log
  enabled: true
  paths:
    - /var/log/nginx/access.log
processors:
  drop_fields:
      fields: ["beat", "input_type", "prospector", "input", "host", "agent", "ecs"]
output.logstash:
  hosts: ["localhost:5044"]



![5](https://github.com/BOSe1337/ELK/blob/main/5-5.jpg)









