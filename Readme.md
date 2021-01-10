How to use
1. generate SSL certificates by running cert-gen docker-compose container
2. generate passwords
docker-compose exec apm-elasticsearch bash
./bin/elasticsearch-setup-passwords auto -u "https://localhost:9200"
3. configure passwords for services
4. restart containers
