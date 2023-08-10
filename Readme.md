# How to use
1. generate SSL certificates by running cert-gen docker-compose container
```
docker-compose -f cert-gen/docker-compose.yml up && docker-compose -f cert-gen/docker-compose.yml down
```
2. Update secret for apm
- [docker-compose.yml](docker-compose.yml)
```
apm-server.secret_token="{very strong secret dont share with anyone}"
```
3. generate passwords
```
docker-compose up -d
docker-compose exec apm-elasticsearch ./bin/elasticsearch-setup-passwords auto -u "https://localhost:9200"
```
4. configure passwords for services
- [docker-compose.yml](docker-compose.yml)
```
output.elasticsearch.password={elastic user password}
apm-server.kibana.password={apm_system user password}
```
- [kibana.yml](kibana.yml)
```
elasticsearch.password: {kibana user password}
xpack.encryptedSavedObjects.encryptionKey: "{very strong secret dont share with anyonet}"
```
- [logstash.yml](logstash.yml)
```
xpack.monitoring.elasticsearch.password: '{elasticsearch user password}'
```
- [logstash/logstash.conf](logstash/logstash.conf)
```
password => "{elasticsearch user password}"
```
5. restart containers for changes to take effect
```
docker-compose down && docker-compose up -d
```
6. Navigate to [https://localhost:5601/](https://localhost:5601/) and login with elastic user credentials